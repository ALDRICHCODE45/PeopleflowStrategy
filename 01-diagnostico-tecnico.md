# Diagnóstico Técnico — PeopleFlow2

> **Análisis read-only del código actual.** Fuente: 2 exploraciones paralelas con contexto fresco (READ-ONLY, sin modificaciones).

---

## Veredicto principal

**El código está BIEN HECHO. El problema NO es calidad, es configurabilidad.**

- DDD real (no de cartón): 4/5
- Salud de código excepcional: **5/5** (0 `@ts-ignore`, 3 `any` en todo el repo, 14 TODO/FIXME)
- Multi-tenancy en schema: bien indexado
- Pero todo está **hardcoded a un cliente (headhunting MX)**

---

## Score arquitectónico por área

| Área | Score | Justificación |
|---|---|---|
| DDD real | 4/5 | Entidades puras, use cases con DI. `CheckAnyPermissonUseCase` rompe DI. |
| Multi-tenancy | 2/5 | Schema OK, pero `prismaWithTenant` NUNCA se usa. Depende de disciplina del dev. |
| Configurabilidad | 1/5 | Estados son enums Prisma. Sin `TenantSettings`/`FeatureFlag`/`WorkflowDefinition`. |
| Permisos escalables | 3/5 | 808 permisos hardcoded en español. Roles por tenant funcionan. |
| Acoplamiento features | 2/5 | `vacancy` importa de `Finanzas/Clientes`. `getActiveTenantId` duplicado 6 veces. |
| Modelo extensible | 1/5 | 0 custom fields. Todo columnas rígidas. |
| Frontend reusable | 3/5 | UI shadcn OK, pero páginas enormes (719-951 líneas). Rutas hardcoded en español. |
| Consistencia patrones | 4/5 | 11 de 14 features siguen DDD. Naming de folders inconsistente. |
| Salud código | 5/5 | Élite. |
| Onboarding tenant | 1/5 | `CreateTenantUseCase` solo inserta una fila. No provisiona NADA. |

**Promedio: 2.6/5 — Base decente pero NO lista para SaaS sin trabajo serio.**

---

## 🔴 Problemas críticos (impiden multi-cliente)

### 1. Workflow de Vacantes hardcoded
**Archivo:** `src/features/vacancy/server/domain/value-objects/VacancyStatus.ts:36-53`

Pipeline cableado: `QUICK_MEETING → HUNTING → FOLLOW_UP → PRE_PLACEMENT → PLACEMENT`. Es el flujo completo de agencia headhunting/staffing. Otra industria NO puede usar esto sin romper.

`VacancyStateMachine.ts:148-196` tiene guards específicos del negocio (HasJobDescriptionGuard, HasValidatedPerfilMuestraGuard, HasCandidatesInTernaGuard, HasFinalistInTernaGuard).

`prisma/schema.prisma:598-607` → enum `VacancyStatus` en DB. Cambiar = migración global.

**Esfuerzo para resolver: ALTO** (3-4 semanas para convertir a workflow engine configurable)

### 2. Workflow de Leads hardcoded + acoplamiento cross-módulo
**Archivos:**
- `src/features/Leads/server/domain/value-objects/LeadStatus.ts:20-36`
- `src/features/Leads/server/application/use-cases/UpdateLeadStatusUseCase.ts:120`

Estados: `CONTACTO → CONTACTO_CALIDO → ... → POSICIONES_ASIGNADAS`. El último estado **auto-crea un Client en Finanzas**. Para industrias no-headhunting esto rompe el CRM.

**🐛 BUG OCULTO:** `LeadStatus.ts:79-83` tiene `canTransitionTo` desactivado con TODO. Siempre retorna `true`. **Las transiciones de Lead NO se validan en backend.**

### 3. Facturación 100% México (CFDI/SAT)
**Archivos:**
- `src/features/Finanzas/Facturas/server/domain/services/InvoiceCalculationService.ts:60-62`
- `prisma/schema.prisma:1084-1118`

Hardcoded:
- IVA 16% (México), USD asume 0%
- Sin IVA 8% (frontera), exento, IEPS
- Enum `Currency { MXN, USD }` — solo 2 monedas
- `InvoicePaymentType { PUE, PPD }` — códigos SAT mexicanos (CFDI 4.0)
- Campos `rfc`, `razonSocial`, `regimenFiscal`, `figura`, `codigoPostalFiscal`

**Vender a Argentina/Chile/Colombia = rediseño completo del módulo Finanzas.**

### 4. Multi-tenancy es defensa de papel
**Archivos:**
- `src/core/lib/prisma.ts:84`
- `src/core/lib/prisma-tenant.ts`

`prismaWithTenant` existe (extension que inyecta `tenantId` automáticamente) pero **NUNCA se usa** en features. `grep prismaWithTenant src/features` = 0 resultados.

Patrón frágil en `PrismaLeadRepository.ts:103-110, 197-202, 226-232, 460`:
```ts
const lead = await prisma.lead.findUnique({ where: { id } });
if (lead.tenantId !== tenantId) return null; // Check posterior
```

**Algunas queries en Inngest functions ni siquiera tienen el check.** Esto es bomba de tiempo con 5+ clientes.

### 5. CreateTenantUseCase no provisiona nada
**Archivo:** `src/features/tenants/server/application/use-cases/CreateTenantUseCase.ts:21-77`

Solo inserta `tenantRepository.create({ name, slug })`. **No crea:**
- Roles
- Admin user
- Catálogos (sectores, orígenes)
- `VacancyConfig`
- `NotificationConfig`

**Onboarding actual = scripts manuales.** Imposible escalar.

### 6. Permisos hardcoded + en español + industria-specific
**Archivo:** `src/core/shared/constants/permissions.ts` (806 líneas)

808 permisos como `vacantes:validar-terna`, `leads:acceder`, `candidatos:crear`. Atados a industria recruiting. Seedeados globalmente.

---

## 🟡 Problemas medios (necesitan refactor)

### 7. Templates de email branded como PeopleFlow
**Path:** `src/features/Notifications/server/infrastructure/templates/*.ts` (22 archivos)

- Logo Cloudinary hardcoded: `res.cloudinary.com/dpvxqsf6s/.../logo-principal_b47vfa.webp`
- Footer "© 2025 PeopleFlow"
- Color brand `#9333ea` hardcoded
- `APP_URL = "https://www.peopleflow.tech"` (functions.ts:100)
- Email from `noreply@peopleflow.com` hardcoded

### 8. Timezone México hardcoded
**Archivo:** `src/core/shared/helpers/timezone.ts:14`

`MEXICO_TZ = "America/Mexico_City"` cableado en helpers + crons Inngest.

### 9. Comisión cliente-specific
**Archivo:** `src/features/vacancy/server/application/use-cases/ConfirmPlacementUseCase.ts:45-46`

`commissionDate = new Date(today.getFullYear(), today.getMonth() + 1, 15)` — día 15 del mes siguiente. Es política comercial del cliente actual.

### 10. Defaults UI cableados a MX
- 10+ componentes con `defaultCountry="MX"`
- 12+ usos de `toLocaleString("es-MX")`

### 11. Acoplamiento cross-feature
- `PrismaVacancyRepository.ts:29` importa de `Finanzas/Clientes`
- `Leads/UpdateLeadStatusUseCase.ts:3` importa `prismaClientRepository`
- `Finanzas/Clientes/UpdateClientFiscalDataUseCase.ts:1` importa `RFCVO` de Leads
- 4 templates importan tipos de `vacancy`

### 12. Páginas frontend enormes
- `VacancyListPage` — 719 líneas
- `VacancyDetailSheet` — 951 líneas
- `CreateInvoiceForm` — 850 líneas

---

## 🟢 Lo que SÍ funciona (reusable tal cual)

### Componentes reusables

| Feature/Componente | Por qué sirve |
|---|---|
| `src/features/Auth/` | Better Auth, password reset, OTP, agnóstico |
| `src/features/auth-rbac/` | RBAC genérico, roles por tenant |
| `src/features/tenants/` | Multi-tenant estándar |
| `src/features/super-admin/` | Gestión global tenants |
| `Sistema/configuracion/NotificationConfig` | Bien diseñado, configurable por tenant |
| `VacancyConfig` | Campos requeridos configurables por tenant |
| `Sector`, `Subsector`, `LeadOrigin` | Catálogos con `tenantId?` opcional |
| `InvoiceFolioCounter` | Prefijo y contador por tenant |
| Pattern DDD | Entidades puras, use cases con DI |
| TanStack Query + Server Actions | Patrón moderno consistente |
| Inngest infra | Durable execution lista |

### Veredicto por feature

| Feature | Veredicto | Razón |
|---|---|---|
| `Auth/` | ✅ REUSABLE | Agnóstico |
| `auth-rbac/` | ✅ REUSABLE | Sistema RBAC genérico |
| `tenants/` | ✅ REUSABLE | Multi-tenant estándar |
| `super-admin/` | ✅ REUSABLE | Gestión global |
| `Sistema/configuracion/` | ✅ REUSABLE | NotificationConfig bien hecho |
| `Administracion/` | 🟡 REFACTOR LIGERO | i18n permisos/UI |
| `Leads/` | 🟠 REFACTOR FUERTE | Workflow hardcoded + auto-conversión a Client |
| `vacancy/` | 🔴 TIRAR Y REHACER | Todo asume agencia recruiting |
| `Finanzas/Clientes/` | 🟠 REFACTOR FUERTE | Datos fiscales MX |
| `Finanzas/Facturas/` | 🔴 TIRAR Y REHACER multi-país | CFDI/SAT, IVA 16% |
| `Finanzas/Ingresos/`, `Egresos/` | ⚠️ VACÍO | Carpetas existen pero no implementadas |
| `Notifications/` | 🟠 REFACTOR FUERTE | 22 templates branded |
| `InAppNotifications/` | 🟡 REFACTOR LIGERO | Sistema OK, tipos enum cableados |

---

## Quick wins (refactors baratos con alto impacto)

| Cambio | Esfuerzo | Impacto |
|---|---|---|
| Borrar 5 copias de `getActiveTenant.helper.ts` | 30 min | Limpieza |
| Reemplazar `findUnique + check` por `findFirst({where:{id, tenantId}})` | 1h | Seguridad |
| DI en `CheckAnyPermissonUseCase` (recibir repo por constructor) | 30 min | Testabilidad |
| Modularizar `permissions.ts` | 1h | Mantenimiento |
| POC `prismaWithTenant` en `vacancy` y `Leads` | 4h | Seguridad multi-tenant |
| `Tenant.brand` (brandName, logoUrl, emailFromAddress) | 2h | Multi-cliente básico |
| Eliminar `Finanzas/Egresos` y `Finanzas/Ingresos` vacíos | 15 min | Honestidad |
| Normalizar naming de folders | 2h | Consistencia |

---

## Refactors mayores necesarios

1. **Workflow engine configurable** — Tablas `WorkflowDefinition`/`WorkflowState`/`WorkflowTransition` por tenant. **3-4 semanas.**
2. **Custom fields system** — `CustomFieldDefinition` + `CustomFieldValue`, o `entity.customFields Json`. **2-3 semanas.**
3. **`TenantSettings` unificado** — branding, features, fiscal, currency, locale, timezone. **1-2 semanas.**
4. **Event bus interno** — Romper acoplamiento cross-feature. **3-4 semanas.**
5. **Rediseño Finanzas multi-país** — Perfiles fiscales por país. **4+ semanas.**
6. **Tenant provisioning + onboarding wizard.** **2-3 semanas.**
7. **i18n real + rutas semánticas.** **2-3 semanas.**
8. **Split páginas enormes** (<300 líneas). **1-2 semanas.**

---

## Hallazgos sorprendentes

1. 🐛 **Bug oculto:** `LeadStatusVO.canTransitionTo` desactivado con TODO hace tiempo. Validaciones de Lead no funcionan en backend.

2. 🔗 **Acoplamiento sorpresa:** Lead → Cliente (auto-crea Client al cambiar a POSICIONES_ASIGNADAS). Rompe el CRM para industrias no-recruiting.

3. 📁 **Carpetas vacías:** `Finanzas/Ingresos/` y `Finanzas/Egresos/`. El módulo "Finanzas" en realidad es solo facturación de placements.

4. 🛡️ **`prismaWithTenant` código muerto:** Defensa multi-tenant existe pero no se usa.

5. ✅ **Multi-tenant en schema está bien:** 107 referencias a `tenantId`, índices compuestos OK. El problema no es la arquitectura de datos, es la lógica de negocio.

6. 🎯 **VacancyStateMachine es excelente diseño** (guards funcionales puros) — base perfecta para convertirla en motor configurable por tenant.

---

## Referencias en Engram

- `fork-analysis/client-coupling` (obs 1623) — Mapeo de acoplamiento al cliente
- `fork-analysis/architectural-health` (obs 1624) — Salud arquitectónica
