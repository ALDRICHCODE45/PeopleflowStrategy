# PeopleFlow Strategy — Análisis de Comercialización

> **Contexto:** El cliente actual de PeopleFlow2 propuso comercializar el software a otras empresas, ofrecer un marketplace de CVs, y eventualmente integrarlo todo. Esta carpeta consolida el análisis técnico, comercial y legal de esa propuesta.
>
> **Fecha del análisis:** 2026-05-22
> **Proyecto base:** ~/Desktop/workspace/next/peopleflow2 (NO TOCAR — es del cliente)

---

## 🗺️ Orden de lectura recomendado

### Si tenés 5 minutos:
👉 **[00-resumen-ejecutivo.md](./00-resumen-ejecutivo.md)** — TL;DR de todo

### Si tenés 30 minutos (lectura completa):
1. **[00-resumen-ejecutivo.md](./00-resumen-ejecutivo.md)** — Vista general
2. **[01-diagnostico-tecnico.md](./01-diagnostico-tecnico.md)** — Estado real del código
3. **[02-estrategia-comercial.md](./02-estrategia-comercial.md)** — Modelos de negocio + recomendación
4. **[03-marketplace-cvs-legal.md](./03-marketplace-cvs-legal.md)** — Análisis LFPDPPP del scraping
5. **[04-plataforma-publica-roadmap.md](./04-plataforma-publica-roadmap.md)** — Plataforma con consentimiento
6. **[05-roadmap-integrado.md](./05-roadmap-integrado.md)** — Plan año 1+2 ordenado

---

## 🎯 Conclusiones más importantes

1. **PeopleFlow2 NO es ERP genérico.** Es software de agencia headhunting MX con multi-tenancy técnico. Refactor estimado ~60% del backend.

2. **Recomendación comercial:** Fork como **Vertical Specialist** (agencias headhunting LATAM). Pricing $50-150 USD/usuario/mes. 2-4 meses al MVP.

3. **NO scrapear OCC.** Es delito federal en México (LFPDPPP). En su lugar: backup interno con captura legal.

4. **Plataforma pública SÍ es viable** con consentimiento explícito de candidatos. Construir en 3 fases progresivas validando con datos.

5. **No construir todo en paralelo.** Burnout asegurado siendo 1 dev. Plan secuencial con decisiones Go/No-Go entre fases.

---

## ⚠️ Disclaimers importantes

- **No soy abogado.** Análisis legal es conocimiento general, NO asesoría. Consultar especialista LFPDPPP MX.
- **No soy consultor de negocios.** Análisis comercial es lógica de producto + patrones de industria. Validar con compradores reales.
- **Validación de mercado:** habla con compradores reales antes de construir cualquier cosa.

---

## 🧠 Persistencia en Engram

Este análisis también está guardado en Engram con los siguientes topic_keys:

- `peopleflow-strategy/overview` (obs 1625)
- `peopleflow-strategy/cv-marketplace-legal` (obs 1626)
- `peopleflow-strategy/commercial-model` (obs 1627)
- `peopleflow-strategy/roadmap` (obs 1628)

Reportes técnicos previos (exploración):
- `fork-analysis/client-coupling` (obs 1623)
- `fork-analysis/architectural-health` (obs 1624)

Para recuperar en futuras sesiones:
```
mem_search query: "peopleflow-strategy"
```

---

## ✅ Checklist crítico antes de empezar

### Legal
- [ ] Abogado LFPDPPP contratado/asesor
- [ ] Aviso de privacidad SaaS definido
- [ ] Términos de servicio SaaS definidos
- [ ] Contrato equity/sociedad con cliente firmado

### Comercial
- [ ] Lista de 3-5 compradores con nombres
- [ ] 1+ llamada validación willingness to pay
- [ ] Pricing tentativo definido
- [ ] Propuesta de valor escrita

### Técnico
- [ ] Repositorio fork creado
- [ ] Stack plataforma pública decidido
- [ ] Dominio plataforma pública decidido
- [ ] Backup del proyecto del cliente actual

### Personal
- [ ] Runway financiero personal (6+ meses)
- [ ] Cliente sabe que esto es 12+ meses
- [ ] Equity/revenue share por escrito

---

## 🔄 Cómo retomar

Cuando vuelvas a este tema, ya sea en esta sesión o en futuras:

1. Leer este README primero
2. Leer 00-resumen-ejecutivo.md para refrescar
3. Saltar al doc específico del tema que querés trabajar
4. Si trabajás con un agente IA: `mem_search query: "peopleflow-strategy"` recupera todo el contexto
