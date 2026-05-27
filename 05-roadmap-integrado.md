# Roadmap Integrado — Año 1 y Año 2

> Plan ordenado y secuencial para los 3 productos relacionados:
> 1. **PeopleFlow Fork** (SaaS B2B para agencias headhunting)
> 2. **Plataforma Pública** (marketplace candidatos con consentimiento)
> 3. **Sistema de Backup interno** (urgencia del cliente)

---

## Principio rector

**HACER UNA COSA POR VEZ.** Construir múltiples productos en paralelo siendo una sola persona = burnout asegurado + ningún producto bien hecho.

**Validar con datos REALES antes de construir el siguiente.**

---

## Año 1

### Q1 (Mes 1-3): PeopleFlow Fork → MVP Vertical Specialist

**Objetivo:** producto comercializable a agencias de headhunting LATAM.

**Sprint 1-2 (Sem 1-3): Foundations**
- ✅ Crear repositorio fork
- ✅ Activar `prismaWithTenant` (defensa multi-tenant real)
- ✅ Implementar `ProvisionTenantUseCase` atómico
- ✅ Tenant branding mínimo: logoUrl, brandName, emailFromAddress, primaryColor
- ✅ Fix bug `LeadStatus.canTransitionTo` (está desactivado en producción)
- ✅ Borrar duplicados `getActiveTenant.helper.ts` (5 copias)
- ✅ DI en `CheckAnyPermissonUseCase`

**Sprint 3-4 (Sem 4-6): Configurabilidad**
- ✅ Workflow customization por tenant (estados + transiciones de vacantes)
- ✅ Workflow customization para Leads (resolver acoplamiento auto-Client)
- ✅ Templates de email editables
- ✅ Custom fields básicos (Lead, Vacancy, Candidate)
- ✅ Feature flags por tenant

**Sprint 5-6 (Sem 7-9): Multi-país**
- ✅ TenantFiscalProfile (sacar RFC/CFDI del schema base)
- ✅ Multi-currency real (no solo MXN/USD)
- ✅ Multi-timezone (sacar Mexico_City hardcoded)
- ✅ i18n base (es-MX, es-LATAM, es-ES)

**Sprint 7-8 (Sem 10-13): Onboarding & Polish**
- ✅ Wizard de onboarding tenant (UI)
- ✅ Splittear páginas enormes (VacancyListPage 719 líneas, etc.)
- ✅ Testing manual exhaustivo (recordar: 0 tests automatizados)
- ✅ Documentación de onboarding

**Entregables Q1:**
- Producto listo para vender a 3-5 agencias
- Landing page comercial
- Pricing definido y publicado
- Proceso de onboarding documentado

**Tareas paralelas (NO técnicas):**
- 🤝 Definir contrato/equity con el cliente actual
- 🤝 Conseguir 3-5 leads de agencias headhunting LATAM
- 🤝 Definir términos de servicio + privacidad del SaaS

### Q2 (Mes 4-5): Sistema de Backup interno (cliente actual)

**Objetivo:** resolver el problema urgente del cliente sin scraping.

**Sprint 1-2 (Sem 14-15): Captura legal**
- ✅ Email parser: cuando OCC manda email de postulación → extracta datos
- ✅ Importador manual asistido (botón/extensión navegador)
- ✅ Almacenamiento en PeopleFlow del cliente (no plataforma separada)
- ✅ Compliance LFPDPPP básico para uso interno

**Sprint 3 (Sem 16-17): Polish**
- ✅ Dashboard de "candidatos respaldados"
- ✅ Búsqueda interna de CVs
- ✅ Auto-deduplicación

**Entregables Q2 (parte 1):**
- Cliente actual deja de depender de OCC
- Sistema funcional 100% interno
- Compliance LFPDPPP aprobado por abogado

### Q2 (Mes 5-6): Plataforma Pública - Fase 1 (Validación)

**Objetivo:** validar si la audiencia LinkedIn del cliente convierte.

**Sprint 1-2 (Sem 18-19): Landing + Captura**
- ✅ Diseño landing (con copywriter idealmente)
- ✅ Formulario consentido
- ✅ Aviso privacidad bien hecho (con abogado)
- ✅ Dominio propio + setup técnico

**Sprint 3-4 (Sem 20-22): Integración**
- ✅ Email parser / webhook hacia PeopleFlow del cliente
- ✅ Sistema básico ARCO (eliminar datos)
- ✅ Analytics (visitas, conversiones)

**Sprint 5 (Sem 23-24): Launch + medición**
- ✅ Launch con cliente en LinkedIn
- ✅ Iteración basada en data
- ✅ Decisión Go/No-Go Fase 2

**Entregables Q2 (parte 2):**
- Landing pública en producción
- Mínimo 200-500 CVs capturados en 2 meses (criterio éxito)
- Data real sobre conversión LinkedIn → CV

### Q3 (Mes 7-8): Plataforma Pública - Fase 2 (Portal candidato)

⚠️ **Solo SI Fase 1 fue exitosa.**

**Sprint 1-2 (Sem 25-27): Auth + Dashboard**
- ✅ Better Auth para candidatos
- ✅ Dashboard candidato (mi CV, mis postulaciones)
- ✅ Actualización de CV

**Sprint 3-4 (Sem 28-30): Matching + Notif**
- ✅ Vacantes activas de la red (solo del cliente al inicio)
- ✅ Sistema básico de matching (sector, experiencia)
- ✅ Notificaciones email de matches

**Sprint 5 (Sem 31-32): Engagement**
- ✅ Stats: "X reclutadores vieron tu perfil"
- ✅ Re-engagement campaigns
- ✅ Métricas para Go/No-Go Fase 3

**Entregables Q3:**
- 1000+ candidatos activos (criterio éxito)
- 30%+ engagement mensual
- Data para decidir Fase 3

### Q4 (Mes 9-12): Crecimiento PeopleFlow + Pre-Fase 3

**Objetivo paralelo:**

**A. Vender PeopleFlow a más agencias**
- Marketing del producto
- Onboarding de clientes nuevos
- Soporte
- Iteraciones basadas en feedback real
- Meta: 10 agencias pagantes = $10K USD/mes recurrente

**B. Si Fase 2 fue exitosa → preparar Fase 3 (Marketplace)**
- Diseño UX de portal empresas
- Investigación de pagos (Stripe + Mercado Pago)
- Investigación legal específica para marketplace
- Definición de pricing por reclutador

---

## Año 2

### Q1 (Mes 13-15): Plataforma Pública - Fase 3 (Marketplace real)

**Objetivo:** convertir plataforma en marketplace abierto.

**Sprint 1-2: Portal empresas**
- ✅ Registro y verificación de empresas
- ✅ Dashboard empresa
- ✅ Postear vacantes
- ✅ Plan freemium (1-2 vacantes gratis)

**Sprint 3-4: Pagos + Suscripciones**
- ✅ Stripe + Mercado Pago
- ✅ Planes Growth y Agencia
- ✅ Billing automático
- ✅ Acceso pagado a CVs

**Sprint 5-6: Integración bidireccional con PeopleFlow**
- ✅ API entre ambos sistemas
- ✅ Auth federada (SSO)
- ✅ Vacantes de plataforma → PeopleFlow del tenant
- ✅ Pipeline desde plataforma se sincroniza

### Q2-Q3 (Mes 16-21): Crecimiento + Optimización

- Marketing growth en ambos productos
- Iteraciones basadas en data
- Anti-fraude y moderación
- Mejorar matching con IA (embeddings + LLMs)
- Expansión geográfica (otros países LATAM)

### Q4 (Mes 22-24): Nuevos Verticales

- Si negocio sostenible → considerar Modelo 2 (Modular por Industria)
- Workflow engine genérico
- Vertical adicional (legal, salud, marketing, etc.)

---

## Decisiones Go/No-Go

### Después de Q1 (PeopleFlow Fork)
**Go si:**
- Producto técnicamente listo
- 2+ agencias dispuestas a probar (no necesariamente pagar todavía)

**No-Go si:**
- Cliente no consigue compradores reales
- Mercado no responde

### Después de Q2 parte 2 (Fase 1 Plataforma)
**Go a Fase 2 si:**
- 200-500 CVs en 2 meses
- Calidad razonable (rating cliente)
- CAC sostenible

**No-Go si:**
- <100 CVs en 2 meses
- Calidad pobre
- Audiencia LinkedIn no convierte

### Después de Q3 (Fase 2 Portal)
**Go a Fase 3 si:**
- 1000+ candidatos activos
- 30%+ engagement mensual
- Empresas externas mostrando interés orgánico

**No-Go si:**
- <500 candidatos activos
- Engagement bajo
- Solo el cliente usándolo

---

## Inversión estimada (en tiempo)

| Quarter | Producto principal | Producto secundario | Horas estimadas |
|---|---|---|---|
| Q1 | PeopleFlow Fork | - | 480 hs (40 hs/sem) |
| Q2 | Backup interno + Plataforma Fase 1 | - | 480 hs |
| Q3 | Plataforma Fase 2 | PeopleFlow soporte | 480 hs |
| Q4 | PeopleFlow growth | Pre-Fase 3 prep | 480 hs |
| Año 2 Q1 | Plataforma Fase 3 | - | 480 hs |
| Año 2 Q2-Q3 | Growth ambos | Optimización | 960 hs |
| Año 2 Q4 | Nuevos verticales | - | 480 hs |

**Total año 1:** ~1920 horas (~40 hs/semana sostenido)
**Total año 2:** ~1920 horas

---

## Revenue projection (escenario conservador)

| Período | PeopleFlow MRR | Plataforma MRR | Total MRR |
|---|---|---|---|
| Q1 (cierre) | $0 (en desarrollo) | $0 | $0 |
| Q2 (cierre) | $500 (1 agencia early) | $0 | $500 |
| Q3 (cierre) | $2K (3-4 agencias) | $0 (Fase 2 no monetiza) | $2K |
| Q4 (cierre) | $5K (8-10 agencias) | $0 | $5K |
| Año 2 Q2 | $10K | $2K (Fase 3 launch) | $12K |
| Año 2 Q4 | $15K | $8K | $23K |

**Importante:** estos números son hipótesis, NO promesas. Validá con tu cliente y compradores reales.

---

## Riesgos a monitorear

| Riesgo | Impacto | Cuándo revisar |
|---|---|---|
| Burnout del dev (vos) | Crítico | Mensual |
| Cliente pierde tracción LinkedIn | Alto | Mensual |
| Competidor agresivo aparece | Medio | Trimestral |
| LFPDPPP cambia | Alto | Anual + cambios legislativos |
| Capital insuficiente | Crítico | Mensual |
| Mercado no responde | Crítico | Q1 y Q3 |

---

## Checklist antes de empezar (ANTES del Q1)

### Legal
- [ ] Abogado especializado en LFPDPPP contratado/asesor
- [ ] Aviso de privacidad para SaaS definido
- [ ] Términos de servicio del SaaS definidos
- [ ] Contrato de socio/equity con cliente firmado

### Comercial
- [ ] Lista de 3-5 compradores potenciales del cliente (con nombres)
- [ ] 1+ llamada de validación con un comprador potencial
- [ ] Pricing tentativo definido
- [ ] Propuesta de valor escrita

### Técnico
- [ ] Repositorio fork creado
- [ ] Decidido stack de la plataforma pública
- [ ] Decidido dominio de la plataforma pública
- [ ] Backup del proyecto del cliente actual

### Personal
- [ ] Runway financiero personal definido (de qué vivís 6+ meses)
- [ ] Tu cliente sabe que esto es 12+ meses, no 1 mes
- [ ] Negociación de equity/revenue share clara y por escrito

---

## Lo más importante

**No empezar SIN tener el checklist de "antes de empezar" completo.**

El error más caro no es construir mal, es construir LO INCORRECTO bien hecho.
