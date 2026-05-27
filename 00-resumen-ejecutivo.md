# Resumen Ejecutivo — Comercialización de PeopleFlow2

> **Fecha de análisis:** 2026-05-22
> **Contexto:** El cliente actual de PeopleFlow2 propuso comercializar el software a otras empresas, ofrecer un marketplace de CVs, y eventualmente integrarlo todo. Este doc consolida el análisis técnico, comercial y legal.

---

## TL;DR

Hay **3 ideas distintas** mezcladas en una sola propuesta. Hay que separarlas:

| Idea | Viabilidad | Tiempo estimado | Riesgo |
|---|---|---|---|
| **A. Fork de PeopleFlow como SaaS** | ✅ Viable | 2-4 meses (Modelo Vertical) | Bajo-medio |
| **B. Marketplace de CVs scrapeados** | ❌ Ilegal (LFPDPPP MX) | N/A | Alto (penal + reputacional) |
| **C. Plataforma pública con consentimiento** | ✅ Viable pero ambiciosa | 6-12 meses MVP completo | Medio-alto |

---

## Decisiones clave a tomar

1. **¿Quién es el comprador objetivo?**
   - Agencias de headhunting LATAM → recomendado, código actual encaja
   - Empresas con RRHH interno → falta 40% del producto
   - PYMEs en general → muerte por dispersión

2. **¿Modelo comercial?**
   - **Recomendado:** Vertical Specialist en headhunting LATAM
   - Pricing: $50-150 USD/usuario/mes
   - Target: agencias 5-50 reclutadores

3. **¿Qué hacer con el marketplace de CVs?**
   - **NO scrapear OCC** (ilegal + viola ToS)
   - **SÍ construir plataforma pública con consentimiento explícito**
   - Empezar como "página de captura" simple, NO marketplace completo

---

## El problema más importante que descubrimos

PeopleFlow2 NO es un ERP genérico con multi-tenancy.
Es **software de agencia de headhunting mexicana** con multi-tenancy técnico.

- Estados de vacantes (`HUNTING`, `PRE_PLACEMENT`, etc.) → hardcoded
- Workflow de leads termina en "POSICIONES_ASIGNADAS" → cableado a recruiting
- Facturación 100% CFDI/SAT México (IVA 16%, RFC, PUE/PPD)
- `Finanzas/Ingresos/` y `Finanzas/Egresos/` están **VACÍAS**
- 10+ Inngest functions específicas del flujo recruiting

**Esto NO es problema de calidad de código** (el código está excelente, 0 `@ts-ignore`, 3 `any` en todo el repo).
**Es problema de capa de configurabilidad.**

---

## Recomendación general

### Año 1
1. **Mes 1-3:** Fork de PeopleFlow → Vertical Specialist (agencias headhunting LATAM). Vender a 3-5 agencias.
2. **Mes 4-5:** Plataforma pública Fase 1 (landing + captura). Validar con audiencia LinkedIn del cliente.
3. **Mes 6-8:** Si Fase 1 funciona → Fase 2 (portal candidato). Integrar con PeopleFlow.

### Año 2
4. **Mes 9-14:** Marketplace completo (Fase 3) si los números justifican.
5. **Mes 15+:** Expansión geográfica/vertical.

---

## Mapa de documentos

| Doc | Contenido |
|---|---|
| [01-diagnostico-tecnico.md](./01-diagnostico-tecnico.md) | Análisis del código actual: acoplamiento al cliente + salud arquitectónica |
| [02-estrategia-comercial.md](./02-estrategia-comercial.md) | Modelos de negocio analizados, recomendación, pricing |
| [03-marketplace-cvs-legal.md](./03-marketplace-cvs-legal.md) | LFPDPPP, los 3 caminos, por qué scrapear OCC es delito |
| [04-plataforma-publica-roadmap.md](./04-plataforma-publica-roadmap.md) | Plataforma pública integrada a PeopleFlow, fases, arquitectura |
| [05-roadmap-integrado.md](./05-roadmap-integrado.md) | Plan año 1 + año 2 consolidado |

---

## Riesgos transversales

1. **Ejecutor único (vos).** Construir múltiples productos en paralelo = burnout asegurado.
2. **Compliance LFPDPPP serio.** Necesitás abogado, NO opcional.
3. **Dependencia de LinkedIn como canal.** No construir sobre arena.
4. **Equity/sociedad con tu cliente.** Negociar antes de empezar, no después.

---

## Disclaimer

- **No soy abogado.** Lo legal es conocimiento general, validar con especialista LFPDPPP MX.
- **No soy consultor de negocios.** El análisis comercial es lógica de producto + patrones de industria, no validación de mercado real.
- **Validación de mercado:** habla con compradores reales antes de construir cualquier cosa.
