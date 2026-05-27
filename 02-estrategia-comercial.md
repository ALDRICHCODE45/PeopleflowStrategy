# Estrategia Comercial — PeopleFlow2 como SaaS

> **Disclaimer:** No soy consultor de negocios. Este análisis es lógica de producto + patrones de industria que he visto. La validación REAL viene de hablar con compradores reales. Tu cliente, que tiene los compradores en mente, debe validar willingness to pay con llamadas concretas antes de construir.

---

## La pregunta más importante (sin esto, todo lo demás es al aire)

**¿Quién es el comprador objetivo?**

| Comprador | Implicación |
|---|---|
| Agencias de headhunting | Recruiting es core, código actual encaja |
| Empresas con RRHH interno | Falta 40% del producto (ATS, onboarding, etc.) |
| Empresas comerciales con vendedores | Leads/CRM debería ser core (pero leads no compite con HubSpot) |
| PYMEs en general | Muerte por dispersión |

**Sin definir esto, NO se puede hacer pricing ni roadmap.**

---

## Análisis honesto de los 3 módulos actuales

### 🟢 Reclutamiento — La fortaleza REAL del producto

**Está bueno. Es el módulo más completo:**
- Pipeline configurable de vacantes
- Sistema de garantías
- State machine bien diseñada
- Commitments + reportes
- Validación de ternas
- Asignación de reclutadores con historial

**PERO está hecho para agencias de headhunting, NO para RRHH interno.**

| Producto | Quién lo usa | Qué necesita |
|---|---|---|
| Agencia headhunting (LO QUE TENÉS) | Vende reclutamiento a clientes | Fees, garantías, ternas, placements |
| ATS empresarial (LO QUE NO TENÉS) | Depto RRHH interno | Onboarding, performance reviews, payroll integration |

**Mercado para "headhunting agencies":** sí, viable.
**Mercado para "RRHH interno":** te falta mucho producto.

### 🟡 Generación de Leads — Decente pero NO standalone

**Lo que tiene:**
- Pipeline de leads (8 estados)
- Citas
- Origen de leads
- Sectores/subsectores

**Lo que NO tiene (que CRM serios SÍ tienen):**
- ❌ Email marketing / sequences
- ❌ Tracking de actividad (calls, emails, abrir emails)
- ❌ Forecasting / probabilidad de cierre
- ❌ Pipeline de OPORTUNIDADES separado de Leads
- ❌ Reportes comerciales (funnel, ratios)
- ❌ Integraciones (Gmail, Outlook, WhatsApp, Google Calendar)
- ❌ Lead scoring automático

**Frente a HubSpot, Pipedrive, Zoho NO compite.** Está pensado como CRM ligero para alimentar el módulo de recruiting (Lead → Cliente → Vacantes), no como CRM standalone.

**Veredicto:** se vende como "CRM básico incluido", NO como módulo estrella.

### 🔴 Finanzas — Hay que ser MUY honesto

**Las carpetas `Finanzas/Ingresos/` y `Finanzas/Egresos/` están VACÍAS.**

Solo existe Facturación, y 100% atada a CFDI/SAT México.

**Para que "Finanzas" sea módulo VENDIBLE multi-país habría que construir:**
- Cuentas por cobrar / por pagar
- Conciliación bancaria
- Flujo de caja proyectado
- Presupuestos
- Reportes financieros (P&L, balance)
- Multi-moneda real
- Multi-país fiscal

**Esto son 4-6 meses solo de Finanzas.**

**Competidores regionales (gigantes):** Contpaqi, Aspel, Bind ERP, Alegra, Siigo. Pelear acá es suicidio sin diferencial fuerte.

**Veredicto:** vender como **"Facturación de servicios"** (lo que ya hace), NO prometer ERP financiero.

---

## El error típico que evitar

> "Vender TODOS los módulos para que TODOS tengan fortaleza"

Esto es la receta del fracaso. Productos exitosos hacen UNA cosa excepcionalmente bien antes de expandirse:

- Salesforce empezó como CRM
- Slack empezó como chat
- Notion empezó como notas
- Pipedrive empezó como pipeline visual

Si salís diciendo "tenemos recruiting + leads + finanzas + IA + todo modular":
- El comprador no entiende qué sos
- Competís contra especialistas en cada módulo
- Marketing genérico
- Pricing confuso

---

## Los 3 modelos comerciales analizados

### **Modelo 1: Vertical Specialist** ⭐ RECOMENDADO

**"El ATS/CRM para agencias de headhunting LATAM"**

- UN producto, UN target
- Recruiting + CRM ligero + Facturación de servicios
- Multi-país fiscal LATAM
- Branding configurable por agencia

**Pricing sugerido:**
- Starter: $50 USD/usuario/mes (hasta 5 usuarios)
- Pro: $100 USD/usuario/mes (hasta 20 usuarios, custom fields)
- Enterprise: $150+ USD/usuario/mes (white-label, API, soporte)

**Mercado:** agencias 5-50 reclutadores en LATAM.

**Diferencial:**
- Hispanohablante nativo (no traducción mediocre)
- Soporte en español
- Multi-país fiscal LATAM (vs Bullhorn que es gringo)
- Precio accesible (vs Bullhorn $99+ por usuario)

**Tiempo al MVP:** 2-4 meses.

**Por qué funciona:**
- Mercado nicho pero claro
- Competidores grandes (Bullhorn, Vincere) son caros y en inglés
- El cliente actual YA tiene compradores ahí
- 10 agencias × 10 usuarios × $100 USD = **$10K USD/mes recurrente**

**Riesgo:** mercado limitado en tamaño absoluto, pero suficiente para negocio sano.

### **Modelo 2: Modular por Industria**

**"ERP modular con plantillas por industria"**

- Mismo software, templates por industria
- Cada industria habilita módulos preconfigurados
- Pricing: $30 USD/usuario por módulo activo

**Por qué es riesgoso:**
- Necesita workflow engine configurable (6+ meses)
- Soporte caótico (cada cliente es distinto)
- Sales complejo (cada demo es distinta)
- Difícil posicionarse en marketing

**Tiempo al MVP:** 9-12 meses.

### **Modelo 3: ERP Genérico Modular**

**"Como Odoo pero mejor"**

- ❌ **NO recomendado.**
- Odoo lleva 20 años, 1000+ módulos, comunidad enorme
- Pelear acá es suicidio sin $5M+ de inversión

---

## Recomendación final

### Apostar por **Modelo 1 (Vertical Specialist)**

**Por qué:**

1. ✅ **El código YA ESTÁ HECHO para esto.** No peleás contra el producto.
2. ✅ **El cliente conoce el mercado**, tiene network, tiene credibilidad.
3. ✅ **2-4 meses al MVP comercializable.** Inversión chica, riesgo bajo.
4. ✅ **Cash flow:** si pegás 10 agencias = $10K USD/mes recurrente. Negocio sano.
5. ✅ **Te deja la puerta abierta** a expandir DESPUÉS con feedback real.

**Lo que NO recomiendo:**
- ❌ Prometer "ERP completo" → no lo es
- ❌ Vender Finanzas como módulo robusto → no lo es
- ❌ Posicionar Leads como CRM standalone → no compite
- ❌ Venderle a todas las industrias desde día 1 → muerte por dispersión

---

## Lo que el cliente NO está viendo (advertencias para conversaciones)

1. **No es "le cambio el logo y listo".** Es ~60% refactor del backend.
2. **El módulo Finanzas que quiere vender NO existe.** Solo hay facturación.
3. **Scraping de OCC es delito federal MX** (ver doc 03).
4. **0 tests + 5 clientes = ruleta rusa.** Necesitás cobertura mínima antes de escalar.

---

## Tareas previas a desarrollo

### Para el cliente (antes de pedir desarrollo)

1. **Listar los 3-5 compradores concretos** con nombres y datos. Si no los tiene, NO es tan seguro como dice.
2. **Validar willingness to pay** con 1 llamada a uno: "Si tuvieras herramienta X, Y, Z, ¿cuánto pagarías por usuario/mes?"
3. **Definir presupuesto** para 6-9 meses de desarrollo.
4. **Equity/sociedad:** definir qué te corresponde a vos como ejecutor técnico.

### Para vos (antes de construir)

1. **Definir TU norte personal:**
   - ¿Negocio chico estable ($10-30K/mes)?
   - ¿Startup ambiciosa ($1M+/año)?
   - Los caminos son MUY distintos.
2. **Negociar contrato/equity ANTES** de poner meses de trabajo.
3. **Validar runway:** ¿de qué vivís durante los 4 meses de desarrollo?

---

## Preguntas críticas sin responder

- ¿Cuánto capital tenés (cliente + tuyo) para invertir?
- ¿En cuánto tiempo necesitan facturar? 6 meses, 1 año, 2 años?
- ¿Qué % del proyecto te corresponde como ejecutor?
- ¿Tu cliente está dispuesto a invertir o solo aporta network?
- ¿Hay un tercero que invierte capital?

**Estas decisiones deben tomarse antes de la primera línea de código del fork.**
