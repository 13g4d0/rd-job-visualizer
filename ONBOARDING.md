# Guía de Contribución — Día 2

> RD Job Visualizer | Challenge de 7 Días | jobs.sanba.dev

---

## Tareas Técnicas del Día 2

Estas son las tareas del backlog para hoy. Puedes tomar cualquiera:

| # | Tarea | Descripción |
|---|-------|-------------|
| 2.1 | **Fetch de RD Trabaja API** | Descargar las 249 vacantes activas desde `empleateya.mt.gob.do/api/puestos?PageSize=500`. Simple script de fetch. |
| 2.3 | **Script de normalización** | Tomar los CSV crudos (436K filas) y convertirlos al schema en `data/schemas/normalized-job.schema.json`. |
| 2.4 | **Validación cruzada** | ¿Los sectores de las fuentes coinciden con nuestra taxonomía de 12 sectores? |
| 2.5 | **Prototipo del treemap** | Primer treemap D3.js con datos dummy. Ya tenemos el wireframe en `wireframes/treemap-wireframe.html`. |
| 2.6 | **Paleta de colores** | Los colores están en `SECTOR_TAXONOMY.md` — integrarlos al código D3.js. |

---

## Contribuciones No-Técnicas

No necesitas escribir código para aportar. Ideas:

- **Contenido para redes** — Post del Día 2, stories, hilos explicativos
- **Narrativa del proyecto** — ¿Por qué importa visualizar el empleo en RD? Nota de prensa, artículo
- **Análisis sectorial** — ¿Tienen sentido los 12 sectores? ¿Falta alguno? ¿Sobra alguno?
- **Perspectiva de política pública** — ¿Cómo se usa esta data en decisiones de gobierno?
- **Perspectiva educativa** — ¿Qué habilidades demanda el mercado? ¿Qué brechas hay?
- **Conexiones** — ¿Conoces a alguien que debería estar en este challenge?
- **Revisión** — Entra a jobs.sanba.dev, navega, y danos feedback

---

## Cómo Configurar Tu Ambiente

### 1. Clona el repositorio

```bash
git clone https://github.com/Sanba-Development/rd-job-visualizer.git
cd rd-job-visualizer
```

### 2. Sirve la página localmente

```bash
npx serve .
# Abre http://localhost:3000
```

### 3. Activa Claude Code

Si tienes Claude Code instalado ([claude.ai/code](https://claude.ai/code)), ábrelo en el directorio del proyecto. Claude leerá automáticamente el `CLAUDE.md` y entenderá todo el contexto.

### Cosas que puedes pedirle a Claude Code

- "Muéstrame las tareas pendientes del backlog"
- "¿En qué puedo aportar hoy?"
- "Quiero trabajar en la tarea 2.3"
- "Crea un branch y ayúdame con el PR"
- "Ayúdame a escribir un post para redes sobre el proyecto"
- "Dame contexto sobre los datos que tenemos"
- "Quiero revisar el treemap wireframe"

---

## Reglas Simples

1. **No se hace push directo a master** — siempre crear branch + PR
2. **Cualquiera puede revisar y aprobar un PR** de otra persona
3. **Si dos personas trabajan en lo mismo, no pasa nada** — hablamos en el grupo y vemos cómo combinar
4. **Todo aporte cuenta** — código, análisis, contenido, feedback, conexiones
5. **Prefijos de branch:** `feat/` para features, `fix/` para correcciones, `data/` para datos

---

## Recursos Clave

| Recurso | Enlace |
|---------|--------|
| **Página en vivo** | [jobs.sanba.dev](https://jobs.sanba.dev) |
| **Repositorio** | [github.com/Sanba-Development/rd-job-visualizer](https://github.com/Sanba-Development/rd-job-visualizer) |
| **Data Explorer** | [jobs.sanba.dev/explorer.html](https://jobs.sanba.dev/explorer.html) |
| **Wireframe Treemap** | [jobs.sanba.dev/wireframes/treemap-wireframe.html](https://jobs.sanba.dev/wireframes/treemap-wireframe.html) |
| **Backlog de tareas** | `BACKLOG.md` en el repo |
| **Guía detallada** | `CONTRIBUTING.md` en el repo |
