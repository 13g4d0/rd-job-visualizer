**Análisis Técnico de Fuentes de Datos de Empleo en la República Dominicana y Arquitectura de Datos para un MVP de Visualización basado en el Modelo de Karpathy**

El ecosistema de datos laborales en la República Dominicana se encuentra en una fase de transición crítica, impulsada por la Política Nacional de Datos Abiertos y la digitalización de los servicios gubernamentales. Al analizar la iniciativa de Andrej Karpathy, el \"US Job Market Visualizer\", se observa un paradigma replicable que utiliza la inteligencia artificial para interpretar la complejidad de las descripciones ocupacionales y transformarlas en métricas accionables. Este informe detalla una investigación profunda sobre las fuentes de datos dominicanas, los mecanismos de acceso técnico, los obstáculos institucionales y la propuesta de arquitectura para un Producto Mínimo Viable (MVP) que pueda ser desarrollado de manera acelerada utilizando Claude Code antes de la fecha límite establecida.

**El Referente Técnico: El Sistema de Karpathy y su Pipeline de Datos**

El repositorio karpathy/jobs no es simplemente una herramienta de visualización; es un pipeline de ingeniería de datos de extremo a extremo que demuestra cómo tratar información gubernamental semiestructurada. Su arquitectura se desglosa en capas de adquisición, normalización, análisis cualitativo y representación visual.

**Estructura de la Ingesta y el Scraping de Alta Resistencia**

La adquisición de datos en el proyecto de Karpathy se realiza mediante scrape.py, un script que emplea Playwright para interactuar con el Occupational Outlook Handbook de la Oficina de Estadísticas Laborales de EE. UU. (BLS). El análisis del código revela que el uso de Playwright en modo \"no-headless\" es una respuesta directa a los sistemas de detección de bots que emplean los portales oficiales. Esta es una lección fundamental para el contexto dominicano, donde portales como \"RD Trabaja\" presentan dependencias dinámicas de JavaScript que bloquean los extractores de datos tradicionales.

| **Componente del Pipeline** | **Herramienta Utilizada** | **Función Técnica**                                                   |
|-----------------------------|---------------------------|-----------------------------------------------------------------------|
| **Extracción**              | Playwright (Chromium)     | Navegación dinámica y descarga de HTML en modo no-headless.           |
| **Limpieza**                | BeautifulSoup             | Conversión de HTML ruidoso (\~40MB) a Markdown estructurado.          |
| **Análisis**                | OpenRouter (Gemini Flash) | Puntuación de \"Exposición a la IA\" mediante prompts especializados. |
| **Persistencia**            | Archivos JSON y CSV       | Almacenamiento de metadatos ocupacionales y estadísticas base.        |
| **Visualización**           | HTML/JS (Treemap)         | Renderizado estático basado en el volumen de empleo y capas de color. |

**La Lógica de Puntuación de IA y Enriquecimiento Cualitativo**

El núcleo analítico reside en score.py, que utiliza modelos de lenguaje (LLM) para asignar una puntuación de 0 a 10 a cada ocupación. La lógica subyacente no busca predecir el reemplazo del trabajador, sino el grado en que la naturaleza de las tareas será \"reformada\" por herramientas digitales. El sistema clasifica las tareas según su producto final: si el producto es fundamentalmente digital (informes, código, análisis), la exposición es intrínsecamente alta.

Esta distinción es vital para la República Dominicana, donde una gran parte de la fuerza laboral se encuentra en sectores de servicios y turismo. Estos sectores, según la rúbrica de Karpathy, poseen un \"amortiguador\" natural contra la IA debido a la necesidad de presencia física y habilidades manuales en entornos impredecibles.

**Ecosistema de Datos Laborales en la República Dominicana: Instituciones y Acceso**

La investigación identifica tres grandes pilares de datos en el país: el repositorio central de datos abiertos, los portales transaccionales del Ministerio de Trabajo y la infraestructura de las cámaras de comercio y tecnología.

**El Portal Nacional de Datos Abiertos (datos.gob.do)**

Bajo la rectoría de la Dirección General de Ética e Integridad Gubernamental (DIGEIG) y el apoyo técnico de la OGTIC, este portal centraliza los conjuntos de datos de 210 instituciones certificadas bajo la norma NORTIC A3.

| **Institución Fuente**                         | **Tipos de Datos Disponibles**                                   | **Formatos de Acceso** |
|------------------------------------------------|------------------------------------------------------------------|------------------------|
| **Ministerio de Trabajo**                      | Datos sobre registro de empresas y estadísticas de empleo.       | CSV, JSON, XLSX.       |
| **Oficina Nacional de Estadística (ONE)**      | Demografía empresarial formal, proyecciones de población y ENFT. | CSV, ODS, XLSX.        |
| **Ministerio de Administración Pública (MAP)** | Vacantes de carrera administrativa y nómina pública.             | JSON, CSV, XML.        |
| **Tesorería de la Seguridad Social (TSS)**     | Empleadores cotizantes y trabajadores activos por sector.        | ODS, CSV.              |

El acceso a través de datos.gob.do es generalmente abierto y sin paywalls, cumpliendo con la Ley 200-04 de Libre Acceso a la Información Pública. Sin embargo, la actualización de los datos es trimestral en muchos casos, lo que representa un obstáculo para un visualizador que requiera datos en tiempo real.

**El Ministerio de Trabajo y el Sistema RD Trabaja**

El portal \"RD Trabaja\" (antiguo Empléate Ya) es la fuente más granular para vacantes activas del sector privado. Con más de 13,000 empresas y 690,000 candidatos, es el termómetro directo del mercado laboral.

El análisis técnico de este portal revela una arquitectura de Aplicación de Página Única (SPA). La dependencia de JavaScript para renderizar las vacantes implica que un MVP debe integrar herramientas de automatización de navegador en su capa de ingesta. Aunque existe una referencia a una API de intercambio (webapi.mt.gob.do), su acceso parece estar restringido a integraciones institucionales, obligando a los desarrolladores independientes a recurrir a técnicas de scraping ético bajo las normativas de la OGTIC.

**Organizaciones Gremiales y la Cámara TIC RD**

La Cámara Dominicana de las Tecnologías de la Información y Comunicación (Cámara TIC) representa un punto de acceso estratégico para datos sobre empresas tecnológicas. Aunque su sitio web no ofrece un API de empleos, su red de 102 empresas asociadas y su participación en la Agenda Digital 2030 los posiciona como proveedores de perfiles de alta demanda tecnológica.

La investigación sobre otras \"Cámaras\" arroja resultados diversos:

- **Cámara de Comercio y Producción de Santo Domingo (CCPSD):** Gestiona el Registro Mercantil y posee directorios de empresas formales, incluyendo un directorio especializado de \"Empresas Mujer\". El acceso a datos detallados a menudo requiere membresía o trámites administrativos, aunque la consulta de transacciones es pública.

- **Fedocámaras:** Centraliza la información de las cámaras provinciales, permitiendo mapear la distribución geográfica de la actividad comercial.

- **Adofintech:** Agrupa a 95 entidades del sector financiero tecnológico, proveyendo una lista curada de empresas donde la exposición a la IA es máxima.

**Obstáculos Técnicos, Paywalls y Barreras de Datos**

A pesar del marco legal favorable, la implementación de un sistema automatizado enfrenta barreras técnicas y operativas significativas en el contexto dominicano.

**Desafíos de Extracción y Formato**

Muchos de los datos más valiosos sobre el mercado laboral rural y las pymes se encuentran atrapados en informes PDF o documentos de \"memoria institucional\". Por ejemplo, los estudios sectoriales de minería y construcción de la ONE o el Ministerio de Educación requieren una capa de procesamiento de lenguaje natural (NLP) avanzada para extraer tablas y perfiles de competencias.

| **Obstáculo Detectado**  | **Descripción del Problema**                                            | **Impacto en el MVP**                                              |
|--------------------------|-------------------------------------------------------------------------|--------------------------------------------------------------------|
| **Renderizado SPA**      | RD Trabaja requiere JavaScript activo para mostrar vacantes.            | Inhabilita el uso de librerías simples como Requests.              |
| **Bot Detection**        | Los sitios gubernamentales bloquean el acceso masivo automatizado.      | Obliga al uso de proxies rotativos y modos no-headless.            |
| **Fragmentación**        | Los datos de nómina, vacantes y demografía están en portales distintos. | Aumenta la complejidad de la lógica de agregación.                 |
| **Paywalls de LinkedIn** | LinkedIn DR restringe la exportación masiva de datos laborales.         | Limita la profundidad de los insights sobre salarios competitivos. |

**Barreras Éticas y Legales en el Scraping**

El scraping de portales como Aldaba o Buscojobs debe realizarse respetando el archivo robots.txt y los términos de servicio para evitar riesgos legales. Aldaba, en particular, ofrece un feed RSS que constituye un método de acceso \"amigable\" y legal para capturar vacantes recientes sin sobrecargar sus servidores.

**Arquitectura de Datos Propuesta para el MVP mediante Claude Code**

Para cumplir con el plazo de entrega del viernes, se propone una arquitectura ágil que apalanque las capacidades de generación de código y orquestación de Claude Code.

**El Proceso de Desarrollo con Claude Code y MCP**

El uso de Claude Code, integrado con Model Context Protocol (MCP), permite una velocidad de desarrollo sin precedentes al conectar el terminal con herramientas como GitHub, Figma y bases de datos en la nube.

**Cronograma de Implementación (Sprint de 5 Días)**

1.  **Día 1: Definición y Scaffolding.** Utilizar Claude para generar el Documento de Requisitos del Producto (PRD) y configurar el entorno de desarrollo con uv.

2.  **Día 2: Ingesta de Datos Abiertos.** Automatizar la descarga de datasets de datos.gob.do (ONE y MAP) para establecer la base demográfica.

3.  **Día 3: Scraping Dinámico y RSS.** Implementar los extractores para \"RD Trabaja\" (usando Playwright) y el parser de RSS para \"Aldaba\".

4.  **Día 4: Enriquecimiento con Claude API.** Enviar las descripciones de puestos a Claude para la puntuación de exposición a la IA, adaptando la rúbrica de Karpathy al español y al contexto local.

5.  **Día 5: Frontend de Visualización y Despliegue.** Generar el treemap interactivo en React/D3.js y desplegar el MVP.

**Componentes de la Arquitectura del Sistema**

La arquitectura propuesta es modular y desacoplada, siguiendo las mejores prácticas de ingeniería de software para proyectos impulsados por IA.

**Capa de Adquisición (Ingestión)**

Se utilizarán dos vías: una pasiva para archivos estáticos de la ONE y una activa mediante Playwright para sitios dinámicos. La integración con MCP permitirá a Claude Code monitorear el estado de los scripts de ingesta y corregir fallos en los selectores CSS de forma automática.

**Capa de Procesamiento y Análisis**

Los datos recolectados se normalizarán a un formato Markdown antes de ser procesados por el motor de scoring. A diferencia del modelo original, se incluirá una métrica de \"Brecha Lingüística\", dado que el dominio del inglés es un factor determinante en la empleabilidad tecnológica dominicana.

| **Capa de Arquitectura** | **Tecnología**         | **Justificación Técnica**                                          |
|--------------------------|------------------------|--------------------------------------------------------------------|
| **Backend de Control**   | Claude Code CLI        | Orquestación rápida y manejo de contexto de todo el repositorio.   |
| **Runtime de Python**    | uv                     | Gestión de dependencias ultra-rápida y entornos aislados.          |
| **Agente de Scraping**   | Playwright             | Capacidad de navegar SPAs y evadir bloqueos básicos.               |
| **Motor de Análisis**    | Claude 3.5 Sonnet      | Superioridad en razonamiento cualitativo y generación de racional. |
| **Base de Datos MVP**    | Archivos JSON / SQLite | Simplicidad para un despliegue antes del viernes.                  |
| **Interfaz de Usuario**  | React + V0.dev         | Generación acelerada de UI basada en el prototipo de Karpathy.     |

**Análisis Profundo de las Fuentes de Datos del Gobierno Dominicano**

La robustez del MVP dependerá de la calidad de la integración con los datos oficiales. La República Dominicana posee un marco institucional sólido para la producción de estas estadísticas.

**La Oficina Nacional de Estadística (ONE) y la Demografía Laboral**

La ONE es el cimiento de cualquier análisis de mercado. Sus datos permiten ponderar el área de los mosaicos en el treemap. La Encuesta Nacional de Fuerza de Trabajo (ENFT), realizada desde 1986, provee la serie histórica necesaria para entender los ciclos de empleo.

Un insight crítico derivado de los microdatos de la ONE es la prevalencia de la informalidad (58%), lo que sugiere que los portales de empleo solo capturan una fracción del mercado total. El MVP debe aclarar en sus notas que la visualización se refiere principalmente al mercado formal, que es donde la IA tendrá un impacto directo inicial.

**El Ministerio de Administración Pública y el Portal Concursa**

El portal Concursa es la ventana a la burocracia estatal. Sus anuncios de vacantes son extremadamente detallados y ofrecen un excelente material para el análisis de IA, ya que incluyen descripciones de cargos, responsabilidades y competencias específicas. Estos documentos, a menudo en formato PDF, pueden ser procesados eficientemente por Claude para extraer las tareas que son susceptibles de automatización administrativa.

**El Rol de las Cámaras en el Ecosistema Tecnológico**

Las cámaras no son solo fuentes de datos, sino validadores de las tendencias que el visualizador intentará mapear.

**Cámara TIC: El Catalizador del Sector Digital**

La Cámara TIC ha sido vocal sobre el impacto de la automatización y la robótica en la fuerza laboral dominicana. Su involucramiento en el V Plan de Acción de Gobierno Abierto subraya su compromiso con la transparencia y la apertura de datos. Para el MVP, la Cámara TIC puede proveer el \"Directorio de Socios\", permitiendo crear una capa de visualización específica para las empresas que lideran la transformación digital en el país.

**Cámaras de Comercio y el Registro Mercantil**

La Cámara de Comercio de Santo Domingo es el epicentro de la información corporativa. Su base de datos del Registro Mercantil permite identificar el tamaño de las empresas por capital social y sector, lo cual es una variable de entrada crucial para el visualizador. Aunque el acceso masivo está limitado, los extractos públicos y los directorios temáticos (como el de empresas de mujeres) ofrecen puntos de datos valiosos para el enriquecimiento del mapa.

**Factores Críticos para el Éxito del MVP antes del Viernes**

El desarrollo de este sistema bajo presión de tiempo requiere una simplificación estratégica sin sacrificar la integridad técnica.

**Estrategia de Ingesta Acelerada**

En lugar de intentar scrapear todos los portales simultáneamente, el MVP debe centrarse en:

1.  **Datos Abiertos del MAP:** Por su alta estructuración y disponibilidad en JSON/CSV.

2.  **Feed RSS de Aldaba:** Para obtener una muestra representativa de vacantes del sector privado de forma inmediata.

3.  **Datasets Históricos de la ONE:** Para establecer el peso visual del treemap basándose en la última Encuesta de Fuerza de Trabajo.

**Implementación de la Capa de IA con Claude Code**

Claude Code facilita la creación de la lógica de \"Model-as-a-Judge\". Se puede programar a Claude para que lea los archivos Markdown generados por BeautifulSoup y devuelva un objeto JSON con la puntuación de exposición y el racional técnico. Esta técnica reduce el tiempo de desarrollo de la lógica de negocio de días a horas.

**Visualización Adaptada al Contexto Dominicano**

El treemap no debe limitarse a las categorías de la BLS de EE. UU. Se debe adaptar a la Clasificación Nacional de Ocupaciones (CNO) de la República Dominicana. El MVP presentará capas de:

- **Sector Económico:** Turismo, Agroindustria, Servicios, TIC.

- **Ubicación Geográfica:** Concentración en el Gran Santo Domingo vs. Provincias.

- **Riesgo de IA:** Basado en la digitalización de la tarea.

**Consideraciones sobre la Calidad y Veracidad de los Datos**

Es fundamental comunicar al usuario final que las puntuaciones de exposición a la IA son estimaciones de modelos de lenguaje y no predicciones económicas definitivas. La brecha entre la capacidad técnica de la IA y su adopción real en las empresas dominicanas puede ser amplia, debido a factores de infraestructura y costos de cómputo.

Un insight de segundo orden es que, mientras los desarrolladores de software tienen una alta exposición teórica (9/10), el mercado dominicano muestra una demanda creciente por estos perfiles, lo que sugiere que la IA está expandiendo las posibilidades del rol en lugar de eliminarlo.

**Conclusiones y Recomendaciones para la Ejecución del MVP**

La construcción de un visualizador del mercado laboral dominicano inspirado en Karpathy es una meta ambiciosa pero lograble para este viernes mediante el uso de Claude Code. La clave reside en la integración inteligente de fuentes gubernamentales de datos abiertos con técnicas de captura de vacantes en tiempo real.

**Pasos Inmediatos para el Equipo de Desarrollo**

1.  **Activación de Claude Code:** Iniciar el scaffolding del proyecto React/Next.js y conectar los MCP de GitHub y base de datos.

2.  **Priorización de Fuentes:** Centrarse en datos.gob.do para la estructura y el feed RSS de Aldaba para la frescura de los datos.

3.  **Configuración de Playwright:** Implementar el scraper para RD Trabaja utilizando el modo no-headless para asegurar la persistencia de la conexión.

4.  **Calibración del Rubric de IA:** Ajustar el prompt de Claude para considerar las particularidades del mercado laboral dominicano, como la informalidad y la brecha digital.

Al finalizar la semana, el MVP proporcionará una herramienta visual poderosa para que tanto buscadores de empleo como analistas de políticas públicas comprendan cómo la revolución de la inteligencia artificial está reconfigurando el tejido productivo de la República Dominicana.
