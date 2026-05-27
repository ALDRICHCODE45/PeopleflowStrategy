# Marketplace de CVs — Análisis Legal y Estratégico

> ⚠️ **Disclaimer importante:** No soy abogado. Este documento es **conocimiento general de industria + patrones legales públicos**. NO es asesoría legal. Para decisiones reales necesitás:
> - Abogado especializado en LFPDPPP (Ley Federal de Protección de Datos Personales en Posesión de los Particulares — México)
> - Abogado de propiedad intelectual / términos de servicio digitales
>
> Esto es CRÍTICO. No avances sin consulta legal.

---

## La idea original del cliente (lo que NO se puede hacer)

> "Scrapeamos los CVs de mi cuenta de OCC, armamos una base de datos, y cuando un cliente quiera reclutar pero no tiene presupuesto, le vendemos acceso a esa data. Ve experiencia pero no contacto. Si quiere contacto, paga."

**Esto es ilegal en México. Punto.**

---

## Por qué es ilegal: los 3 problemas

### Problema #1: Falta de consentimiento para transferencia a terceros

Cuando un candidato postula a una vacante en OCC, está dando consentimiento para que:
- ✅ **El reclutador de esa vacante específica** evalúe su CV

NO está consintiendo:
- ❌ Que su CV sea vendido a otros reclutadores desconocidos
- ❌ Que sus datos circulen como producto comercial
- ❌ Que terceros accedan a su información sin permiso

**Vender ese CV = violación directa de LFPDPPP México.**

### Problema #2: Es DOXING comercial

> "El cliente ve experiencia pero no contacto, si quiere ver contacto paga"

Esto es vender **datos de contacto de personas físicas que NO consintieron ser vendidas**. Es modelo de mercado negro de bases de datos.

**LinkedIn lo hace, sí. Pero LinkedIn tiene consentimiento explícito en sus ToS** que cada usuario aceptó al registrarse. Tu cliente NO tiene eso.

### Problema #3: Viola ToS de OCC

OCC promete a sus candidatos (en su política de privacidad) que sus datos solo serán vistos por el reclutador de la vacante específica. Si extraés y revendés esos CVs:
- OCC puede demandarte civilmente
- OCC puede banear la cuenta (perdés acceso a TODO el flujo de candidatos)
- Caso similar: hiQ Labs vs LinkedIn (jurisprudencia en EEUU sobre scraping)

---

## Sanciones reales LFPDPPP (México)

**Art. 64 — Multas:**
- De **100 a 320,000 días de salario mínimo** (~$30K - $90M MXN)
- Si hay datos sensibles (etnia, salud, religión que aparecen en CVs) → multas **se duplican**

**Art. 67 — Penal:**
- En casos graves → **prisión de 3 meses a 3 años**
- En datos sensibles → hasta **5 años de prisión**

**Esto no es exageración. Es delito federal.**

---

## Para vos como dev: corresponsabilidad

**Si construís algo ilegal, sos responsable.**

El argumento "yo solo programé lo que me pidieron" NO te salva. Si las autoridades investigan, vos como arquitecto del sistema podés ser señalado como cómplice (Art. 7 Código Penal Federal sobre participación).

**Tu reputación profesional es tu activo más valioso. No vale la pena.**

---

## Los 3 caminos posibles

### **Camino A: Solo backup defensivo** ✅ SEGURO

**Qué resuelve:** el problema real del cliente ("OCC se cae, nos quitan candidatos").

**Cómo se hace LEGAL:**
- NO scrapear OCC
- Capturar datos de candidatos que YA postularon a las vacantes del cliente
- Usar **uno o varios** de estos métodos:

| Método | Cómo funciona | Legalidad |
|---|---|---|
| API oficial de OCC | Si la tienen y se paga | ✅ Limpio |
| Email forwarding parser | OCC manda email de postulación → parser → BD propia | ✅ Limpio (son emails dirigidos al cliente) |
| Importador manual asistido | Botón/extensión que copia datos cuando el reclutador revisa CV | ✅ Limpio (es la decisión humana del reclutador) |
| Formulario propio paralelo | En vacantes nuevas, además de OCC, formulario propio con consentimiento | ✅ Limpio |

**Compliance LFPDPPP mínimo requerido:**
- ✅ Aviso de privacidad publicado y aceptado
- ✅ Finalidad declarada del tratamiento
- ✅ Derecho ARCO funcional (botón "darme de baja")
- ✅ Responsable de datos personales designado
- ✅ Plazo de conservación definido
- ✅ Si hay transferencia a terceros → consentimiento expreso

**Uso permitido:** 100% interno para el cliente. NO se venden los datos a nadie.

**Tiempo desarrollo:** 2-3 semanas.

**Riesgo legal:** bajo (si se hace con consultoría legal).

### **Camino B: Marketplace con consentimiento explícito** ✅ VIABLE (ver doc 04)

Es construir una plataforma propia donde candidatos suben CV **voluntariamente** sabiendo a qué se exponen.

Este camino merece su propio documento → ver [04-plataforma-publica-roadmap.md](./04-plataforma-publica-roadmap.md).

### **Camino C: Scrapear y vender CVs sin consentimiento** ❌ NO HACER

- Ilegal en México (LFPDPPP)
- Viola ToS de OCC (demanda civil casi segura)
- Riesgo penal real
- Destrucción reputacional si se filtra
- **Como arquitecto responsable, no se construye.**

---

## Compliance LFPDPPP — Checklist obligatorio

Para cualquiera de los caminos A o B:

### Documentación

- [ ] **Aviso de privacidad simplificado** (visible al recolectar datos)
- [ ] **Aviso de privacidad integral** (link al doc completo)
- [ ] **Finalidades primarias y secundarias** distinguidas
- [ ] **Designación de responsable de datos personales** (RDP)

### Sistemas técnicos

- [ ] **Consentimiento granular** (checkboxes separados por finalidad)
- [ ] **Derecho ARCO** funcional:
  - Acceso (descargar mis datos)
  - Rectificación (editar)
  - Cancelación (borrar)
  - Oposición (limitar uso)
- [ ] **Log de consentimientos** (cuándo aceptó, qué versión del aviso)
- [ ] **Cifrado de datos sensibles**
- [ ] **Plazo de retención automático** (auto-delete después de X tiempo)
- [ ] **Trazabilidad de accesos** (quién vio qué CV cuándo)

### Procesos

- [ ] **Procedimiento de respuesta a solicitudes ARCO** (máx 20 días hábiles)
- [ ] **Notificación de incidentes** (data breach)
- [ ] **Política de retención de datos**
- [ ] **Acuerdo de confidencialidad** con empleados que acceden

---

## Conversación recomendada con el cliente

> "Mira, entiendo el problema de OCC y el potencial comercial. Pero hay un tema legal serio que debemos manejar bien para no exponernos.
>
> Te propongo dos fases:
>
> **Fase 1 (3 semanas):** Sistema de backup interno. Resuelve tu problema de no depender de OCC. Captura legal por email parsing y/o botón importador. Cero riesgo.
>
> **Fase 2 (3-6 meses):** Si querés marketplace, lo construimos BIEN. Plataforma propia donde candidatos suban su CV consentido. Más tiempo, pero es un negocio sostenible y legal.
>
> Lo que NO te puedo hacer es scrapear OCC y revender CVs. Eso es delito federal en México (LFPDPPP, Art. 64-67) y te puede hundir el negocio principal. Como tu desarrollador, mi recomendación profesional es NO ir por ese camino."

---

## Preguntas para validar con el cliente

1. **¿Sabe sobre LFPDPPP?** Muchos empresarios no la conocen.
2. **¿Tiene asesor legal?** Si no, esta conversación tiene que pasar ANTES de cualquier línea de código.
3. **¿Está dispuesto a invertir en compliance** (abogado, aviso de privacidad serio, etc.)?
4. **¿Acepta la limitación legal o insiste en el camino C?** Si insiste, considerar declinar el proyecto.

---

## Próximo paso

Si el cliente acepta el Camino A o B → ver [04-plataforma-publica-roadmap.md](./04-plataforma-publica-roadmap.md) para el roadmap técnico.
