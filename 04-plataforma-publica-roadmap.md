# Plataforma Pública de Postulación + Integración PeopleFlow

> **Idea original:** Aprovechar la reputación en LinkedIn del cliente para construir una plataforma propia de postulación. Candidatos consienten voluntariamente. Reclutadores pagan por contacto. Las vacantes se sincronizan con PeopleFlow.

---

## Por qué esta idea SÍ tiene sentido (a diferencia del scraping)

### ✅ Resuelve el problema legal de raíz
Candidatos suben CV voluntariamente con consentimiento explícito. Modelo legal (similar a OCC, Bumeran, Indeed).

### ✅ Cliente tiene ACTIVO REAL: audiencia en LinkedIn
El **90% de marketplaces fracasan por chicken & egg** (no candidatos sin reclutadores, no reclutadores sin candidatos). Tu cliente tiene tracción orgánica. **Eso vale ORO.**

### ✅ Sinergia real con PeopleFlow
```
LinkedIn (audiencia del cliente)
  ↓ posts virales
Plataforma pública (capta candidatos consentidos)
  ↓ API/webhooks
PeopleFlow (agencias gestionan pipeline)
```

**Flywheel real**, no marketing.

### ✅ Múltiples capas de monetización
1. Reclutadores pagan ver CVs (modelo original del cliente, pero LEGAL)
2. Empresas pagan por destacar vacantes
3. Cliente vende PeopleFlow a esas mismas empresas/agencias
4. Datos agregados anonimizados (tendencias salariales) → reportes
5. Premium para candidatos (CV destacado, alertas)

---

## Las preguntas DURAS (sin estas, no avanzar)

### Pregunta dura #1: ¿Contra QUIÉN competís?

| Competidor | Tiene | Tu desventaja |
|---|---|---|
| **OCC Mundial** | 20+ años, base masiva MX | Ellos YA están |
| **Indeed** | Gratis, masivo | Imposible competir en escala |
| **LinkedIn Jobs** | Donde está la audiencia del cliente | Plataforma matriz |
| **Bumeran/Computrabajo** | Brand LATAM establecido | Recognition |
| **GetOnBoard** (tech) | Nicho técnico bien hecho | Si vas a tech, ellos lideran |

**Pregunta brutal:** ¿Por qué un candidato se inscribiría en TU plataforma vs OCC/Indeed/LinkedIn?

**Posicionamiento diferencial sugerido:**
> "Red exclusiva de headhunters profesionales — solo reclutadores verificados ven tu CV, no spammers ni scrapers"

Esto SÍ es diferencial.

### Pregunta dura #2: ¿LinkedIn no te banea?

LinkedIn **penaliza posts con enlaces externos**:
- Algoritmo reduce alcance dramáticamente
- Si detectan que sos competencia (LinkedIn Jobs) → más reducción
- Si crece mucho → posible suspensión de cuenta

**Mitigación:**
- Postear contenido valioso SIN link, link en primer comentario
- Carrousels con vacantes en imagen, link en bio
- LinkedIn Newsletter (menos penalizada)
- Mensajes directos para casos puntuales

**Pero NO podés depender de UNA plataforma. Trabajar SEO + email desde día 1.**

### Pregunta dura #3: ¿Cuánto cuesta el primer candidato?

**Métrica clave:** CAC por lado del marketplace.

- **Candidatos:** asumir viral en LinkedIn = $0 al inicio, pero NO escala. Después de 1000-5000 candidatos vas a necesitar paid ads.
- **Reclutadores:** ¿pagan $100/mes? ¿Cómo los conseguís? CAC esperado $300-500.

Si pricing = $100/mes y CAC = $500 → 5 meses solo para recuperar.
**¿Tenés runway para eso?**

### Pregunta dura #4: ¿Propuesta de valor REAL para el candidato?

¿Por qué un candidato sube CV ahí en vez de LinkedIn?

| Opción | Fuerza |
|---|---|
| "Vacantes exclusivas del cliente" | 🟡 Solo si volumen alto y constante |
| "Headhunters premium te ven" | 🟢 Bueno para senior, no para entry-level |
| "Match con tu industria" | 🟡 Necesita IA decente |
| "Aplicación 1-click" | 🔴 Débil, lo hacen todos |
| "Privacidad: solo reclutadores verificados" | 🟢 DIFERENCIAL INTERESANTE |

### Pregunta dura #5: ¿Cuánto tiempo para validar?

Esta idea es AMBICIOSA. Construir:
- Plataforma pública (frontend nuevo)
- SEO desde cero
- Sistema matching candidato-vacante
- Mensajería in-platform
- Verificación de empresas (anti-fraude)
- Moderación contenido
- Compliance LFPDPPP serio
- Integración bidireccional con PeopleFlow

= **6-12 meses mínimo.**

---

## ✅ MVP en 3 fases progresivas (minimizar riesgo)

### **Fase 1: Página de captura** — 2-3 semanas 🎯 VALIDACIÓN

**NO construir plataforma todavía. Construir esto:**

```
Landing page simple:
  ↓
"Únete a la red de talento exclusiva de [Cliente]"
  ↓
Formulario consentido (CV + datos + ToS claros)
  ↓
CVs entran directo al PeopleFlow del cliente
```

**Lo que validás:**
- ¿La audiencia del cliente realmente convierte? (cuántos suben CV)
- ¿Qué tipo de candidatos llegan? (perfil, calidad)
- ¿Cuál es el CAC real? ($0 viral o necesita ads)

**Costo:** 2-3 semanas, low-tech.
- Landing simple (Next.js, dominio propio)
- Formulario con consentimiento
- Email parser / webhook hacia PeopleFlow
- Aviso de privacidad bien hecho
- Sistema básico de derecho ARCO

**Por qué es genial:** en 2 meses tenés data REAL sobre si la idea funciona ANTES de invertir 6 meses en plataforma completa.

**Métricas a medir:**
- Visitantes desde LinkedIn
- Tasa de conversión visita → CV
- Calidad de CVs recibidos (rating manual del cliente)
- Costo por CV adquirido

**Criterio de éxito Fase 1:** 200-500 CVs en 2 meses, con calidad razonable.

### **Fase 2: Portal de candidato** — 4-6 semanas

**Si Fase 1 funciona:**

- Login para candidatos (Better Auth)
- Pueden actualizar su CV
- Pueden ver "vacantes activas de la red" (SOLO las del cliente al inicio)
- Notificaciones por email de matches
- Sistema básico de matching (filtros por sector, experiencia)
- Dashboard personal: "X reclutadores vieron tu perfil esta semana"

**Aún NO es marketplace.** Es la "red privada de talento del cliente".

**Lo que validás:**
- Engagement de candidatos (LTV)
- Re-engagement (actualizan CV, postulan repetidamente)
- ¿Crece orgánico o cae?

**Criterio de éxito Fase 2:** 1000+ candidatos activos, 30%+ engagement mensual.

### **Fase 3: Marketplace real** — 4-6 meses

**Si Fase 2 funciona:**

- Otras empresas/agencias se registran
- Postean sus vacantes (planes pagos)
- Pagan por acceso a CVs / contacto
- Integración con PeopleFlow (sus vacantes se sincronizan)
- Sistema pagos (Stripe / Mercado Pago)
- Billing, suscripciones, facturas
- Verificación de empresas (anti-fraude)
- Sistema mensajería in-platform

**Criterio de éxito Fase 3:** 10+ empresas pagantes, MRR $5K+ USD.

---

## 🏗️ Arquitectura técnica

### Principio rector: SEPARAR de PeopleFlow

```
┌─────────────────────────────────────────────────────┐
│  PLATAFORMA PÚBLICA (NUEVO proyecto)                │
│  - Frontend público (Next.js, dominio propio)       │
│  - Auth de candidatos                               │
│  - API pública para postulaciones                   │
│  - SEO optimizado (Schema.org JobPosting)           │
│  - Compliance LFPDPPP (aviso, ARCO)                 │
│  - Sistema de pagos (Stripe/MP)                     │
└─────────────────────────────────────────────────────┘
                       ↕ API / Webhook / Event
┌─────────────────────────────────────────────────────┐
│  PEOPLEFLOW FORK (SaaS multi-tenant)                │
│  - Pipeline de reclutamiento                        │
│  - Gestión candidatos recibidos                     │
│  - Workflow para reclutadores                       │
└─────────────────────────────────────────────────────┘
```

### Por qué SEPARADOS (no en el mismo monolito)

1. **Compliance distinto:**
   - Plataforma pública = riesgo LFPDPPP alto (datos personales B2C)
   - PeopleFlow = SaaS B2B (datos profesionales B2B)
   - Mezclarlos = pesadilla legal

2. **Escala distinta:**
   - Plataforma puede tener tráfico viral (10K candidatos/día)
   - PeopleFlow es CRUD interno (low req/seg)

3. **Deploy distinto:**
   - La plataforma puede caerse y NO tirar PeopleFlow

4. **Equipos distintos:**
   - Algún día equipo dedicado a la plataforma

5. **Modelo negocio distinto:**
   - Plataforma = B2C/freemium
   - PeopleFlow = B2B SaaS

6. **Pricing distinto:**
   - Mezclarlos confunde al cliente

### Cómo se comunican

- **API REST/GraphQL** entre ambos
- **Webhook eventos:** nueva postulación → notifica al PeopleFlow del tenant correspondiente
- **Auth federada:** SSO entre ambos
- **Tenant linking:** cada empresa en PeopleFlow tiene "perfil de empresa" en plataforma pública

### Stack sugerido (plataforma pública)

- **Frontend:** Next.js 16 (mismo stack que PeopleFlow, reusar conocimiento)
- **Backend:** Next.js API routes + Server Actions
- **DB:** PostgreSQL separada (no compartir con PeopleFlow)
- **Auth:** Better Auth (mismo)
- **Pagos:** Stripe (internacional) + Mercado Pago (LATAM)
- **Email:** Resend / Postmark
- **Hosting:** Vercel (frontend) + Railway/Neon (DB)
- **CDN/Assets:** Cloudinary (CVs como PDFs)

---

## Riesgos críticos

| Riesgo | Probabilidad | Mitigación |
|---|---|---|
| **Dependencia LinkedIn** | Alta | SEO + email marketing desde día 1 |
| **Chicken & egg** | Alta | Fase 1 con vacantes solo del cliente |
| **Compliance LFPDPPP** | Media | Abogado especializado, NO opcional |
| **Burnout (vos solo)** | Alta | Priorizar 1 producto por vez, no paralelo |
| **Capital insuficiente** | Media | Validar runway 12+ meses antes de Fase 3 |
| **OCC/Indeed mejoran y absorben** | Baja | Diferencial nicho (headhunters verificados) |
| **CAC > LTV** | Media | Medir desde Fase 1 |

---

## Modelo de negocio integrado (sinergia con PeopleFlow)

### Producto 1: Plataforma pública (freemium)

| Plan | Precio | Para |
|---|---|---|
| Candidato Gratis | $0 | Subir CV, postular |
| Candidato Premium | $5-10 USD/mes | CV destacado, alertas |
| Empresa Starter | Gratis | 1-2 vacantes/mes (lead magnet) |
| Empresa Growth | $200-500 USD/mes | Vacantes ilimitadas + acceso CVs |
| Agencia | $500-1500 USD/mes | CV search avanzado + filtros + IA |

### Producto 2: PeopleFlow SaaS

| Plan | Precio | Para |
|---|---|---|
| Starter | $50 USD/usuario/mes | Hasta 5 usuarios |
| Pro | $100 USD/usuario/mes | Hasta 20 usuarios, custom fields |
| Enterprise | $150+ USD/usuario/mes | White-label, API, soporte |

### Bundling / cross-sell

> "Comprá el plan Agencia en nuestra plataforma de talento y obtené 30% OFF en PeopleFlow para tu equipo"

**Esto es defensible.** El cliente acaba teniendo:
- Marketplace de talento (revenue)
- SaaS B2B (revenue recurrente)
- Su propio negocio de headhunting (operativo, usando ambas herramientas)

---

## Compliance LFPDPPP — Imperdible

Ver checklist completo en [03-marketplace-cvs-legal.md](./03-marketplace-cvs-legal.md).

**Mínimo absoluto Fase 1:**

1. Aviso de privacidad simplificado (visible al subir CV)
2. Aviso integral (link al doc completo)
3. Consentimiento granular (checkboxes separados):
   - ☐ Acepto que mi CV sea visible para reclutadores de la red
   - ☐ Acepto recibir notificaciones de vacantes que matcheen mi perfil
   - ☐ Acepto que mis datos de contacto sean compartidos con empresas (solo si paga acceso)
4. Botón "Eliminar mi cuenta y datos" (derecho ARCO)
5. Log de consentimientos (cuándo aceptó, qué versión)
6. Designación de responsable de datos personales

---

## Roadmap concreto (si se valida)

### Quarter 1 — Fase 1 (Validación)
- Semana 1-2: Diseño UX + legal (aviso privacidad)
- Semana 3-4: Desarrollo landing + formulario + parser
- Semana 5-6: Beta privada con audiencia LinkedIn del cliente
- Semana 7-8: Iteración + decisión Go/No-Go

### Quarter 2-3 — Fase 2 (Portal candidato)
- Mes 3-4: Auth + dashboard candidato + matching básico
- Mes 5: Notifications + engagement features
- Mes 6: Decisión Go/No-Go Fase 3

### Quarter 4 — Fase 3 (Marketplace)
- Mes 7-8: Portal empresas + pagos
- Mes 9-10: Integración bidireccional PeopleFlow
- Mes 11-12: Verificación + moderación + launch público

**Total estimado:** 12 meses al producto completo.

---

## Lo más importante

**No construir Fase 2 hasta validar Fase 1.**
**No construir Fase 3 hasta validar Fase 2.**

Cada fase debe tener métricas claras de éxito ANTES de avanzar.

**El error típico:** construir todo de una vez basado en suposiciones. Resultado: 12 meses sin facturar y sin saber si funciona.
