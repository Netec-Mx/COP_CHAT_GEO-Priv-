# Creación de un agente (GPT/Persona) especializado en estándares geológicos. Configuración de instrucciones para que el agente valide informes contra normativas específicas.

## 1. Metadatos

| Atributo | Detalle |
|---|---|
| **Duración estimada** | 100 minutos |
| **Complejidad** | Alta (Hard) |
| **Nivel Bloom** | Crear (Create) |
| **Módulo** | Módulo 3 — Agentes de IA para Geociencias |
| **Práctica número** | 03-00-01 |
| **Modalidad** | Individual con revisión en pares al final |

---

## 2. Descripción General

En esta práctica construirás un agente de IA personalizado —denominado **"Consultor Geológico Copilot"**— dentro del ecosistema Microsoft Copilot Chat, configurando sus instrucciones de sistema, dominio de conocimiento normativo y comportamiento de validación. El agente será entrenado para evaluar informes técnicos geológicos contra los estándares **NI 43-101** y **Código JORC (2012)**, produciendo reportes estructurados de cumplimiento con citas normativas trazables.

La práctica se estructura en tres fases secuenciales: **Diseño** del agente (instrucciones, rol, alcance), **Configuración e implementación** en Copilot Chat, y **Validación en acción** sobre un informe técnico de muestra deliberadamente incompleto. Al concluir, reflexionarás sobre las limitaciones del agente y estrategias de mejora iterativa.

> ⚠️ **AVISO DE CONFIDENCIALIDAD:** Durante toda esta práctica utiliza **exclusivamente** los datasets y documentos de muestra proporcionados por el instructor. **NO cargues datos geológicos reales, confidenciales o propietarios de tu empresa** en Copilot Chat. Los datos reales pueden estar sujetos a acuerdos de confidencialidad y regulaciones de seguridad corporativa.

---

## 3. Objetivos de Aprendizaje

Al finalizar esta práctica serás capaz de:

- [ ] **Diseñar** instrucciones de sistema detalladas para un agente Copilot especializado en estándares geológicos internacionales (NI 43-101, JORC, PRMS), definiendo su rol, tono técnico, restricciones y políticas de citación obligatoria.
- [ ] **Configurar e implementar** el agente "Consultor Geológico Copilot" en Microsoft Copilot Chat, cargando instrucciones de sistema y documentos normativos de referencia como base de conocimiento contextual.
- [ ] **Aplicar** el agente creado para ejecutar una validación automatizada de un informe técnico geológico de muestra, identificando no conformidades, secciones faltantes y datos insuficientes según los estándares de referencia.
- [ ] **Evaluar** la efectividad del agente comparando su reporte de validación con una lista de verificación manual de cumplimiento normativo, identificando fortalezas, limitaciones y oportunidades de mejora iterativa.

---

## 4. Prerrequisitos

### 4.1 Conocimiento Previo

| Requisito | Nivel Mínimo |
|---|---|
| Uso de Microsoft Copilot Chat (Prácticas 1 y 2 completadas) | Competente |
| Concepto de prompt de sistema vs. prompt de usuario en IA conversacional | Básico |
| Conocimiento de al menos uno de: NI 43-101, JORC Code, SPE-PRMS | Básico–Intermedio |
| Redacción de instrucciones técnicas estructuradas en español con terminología geológica | Básico |
| Familiaridad con formatos JSON y Markdown para salida estructurada | Básico |

### 4.2 Acceso y Recursos

| Recurso | Estado Requerido |
|---|---|
| Cuenta corporativa Microsoft 365 activa con Copilot Chat habilitado | ✅ Verificado con TI |
| Permisos para crear agentes / acceso a Copilot Studio (según licencia) | ✅ Confirmado |
| Archivos de práctica en OneDrive/SharePoint compartido por instructor | ✅ Descargados |
| Acceso a carpeta de materiales del curso (48 h antes de la sesión) | ✅ Confirmado |

> 📋 **Nota para el instructor:** Si la licencia corporativa no incluye creación de agentes en Copilot Studio, se activará el **Plan B pedagógico**: simulación del agente mediante un prompt de sistema extenso en conversación estándar de Copilot Chat (ver Sección 6.2, Paso 2B como alternativa).

---

## 5. Entorno de Laboratorio

### 5.1 Hardware Recomendado

| Componente | Mínimo | Recomendado |
|---|---|---|
| Procesador | Intel Core i5 8ª gen / AMD Ryzen 5 | Intel Core i7 / AMD Ryzen 7 |
| Memoria RAM | 8 GB | 16 GB |
| Almacenamiento disponible | 2 GB | 5 GB |
| Resolución de pantalla | 1366 × 768 px | 1920 × 1080 px |
| Conexión a internet | 10 Mbps estable | 25 Mbps o superior |

### 5.2 Software Requerido

| Software | Versión | Uso en esta práctica |
|---|---|---|
| Microsoft Copilot Chat (empresarial) | Vigente (Microsoft 365) | Plataforma principal del agente |
| Microsoft Edge o Google Chrome | Edge 120+ / Chrome 120+ | Navegador para Copilot Chat |
| Microsoft Word (Microsoft 365) | 2301 o superior | Redacción de instrucciones de sistema |
| Microsoft Excel (Microsoft 365) | 2301 o superior | Lista de verificación de cumplimiento |
| Bloc de Notas / Notepad++ | Cualquier versión reciente | Diseño previo de instrucciones |
| OneDrive / SharePoint | Versión empresarial | Acceso a materiales de práctica |

### 5.3 Archivos de Práctica Requeridos

Verifica que tienes los siguientes archivos en tu carpeta local de práctica (descargados desde OneDrive/SharePoint del curso):

```
/Practica_03/
├── INSTRUCCIONES_SISTEMA_Plantilla.txt       ← Plantilla editable de instrucciones
├── EXTRACTO_NI43101_Muestra.pdf              ← Extracto ficticio del estándar NI 43-101
├── EXTRACTO_JORC2012_Muestra.pdf             ← Extracto ficticio del Código JORC 2012
├── INFORME_TECNICO_MUESTRA_v1.docx           ← Informe técnico con desviaciones intencionales
├── CHECKLIST_Cumplimiento_NI43101_JORC.xlsx  ← Lista de verificación manual (Paso 7)
└── PLANTILLA_REPORTE_Validacion.docx         ← Plantilla para reporte final de validación
```

> ⚠️ Si algún archivo no está disponible, notifica al instructor **antes** de comenzar la práctica.

### 5.4 Configuración Inicial del Entorno

Antes de iniciar los pasos, ejecuta las siguientes verificaciones:

**Verificación 1 — Acceso a Copilot Chat:**
1. Abre Microsoft Edge o Chrome.
2. Navega a: `https://m365.cloud.microsoft/chat` (o la URL corporativa de Copilot Chat).
3. Inicia sesión con tu cuenta corporativa Microsoft 365.
4. Confirma que el banner superior muestra **"Microsoft Copilot"** con el indicador de versión empresarial (ícono de escudo o etiqueta "Trabajo").

**Verificación 2 — Acceso a creación de agentes:**
1. En la interfaz de Copilot Chat, busca en el panel lateral izquierdo la opción **"Agentes"**, **"Copilot Studio"** o el ícono ✨ de personalización.
2. Si no visualizas estas opciones, navega a: `https://copilotstudio.microsoft.com` con tu cuenta corporativa.
3. Si ninguna opción está disponible → Notifica al instructor para activar el **Plan B**.

**Verificación 3 — Archivos de práctica:**
```
Confirma en el Explorador de archivos que la carpeta /Practica_03/ 
contiene los 6 archivos listados en la Sección 5.3.
```

---

## 6. Procedimiento Paso a Paso

> 🕐 **Distribución de tiempo sugerida:**
> - Fase 1 — Diseño del agente: 30 minutos (Pasos 1–3)
> - Fase 2 — Configuración e implementación: 25 minutos (Pasos 4–5)
> - Fase 3 — Validación en acción: 30 minutos (Pasos 6–7)
> - Reflexión y evaluación comparativa: 15 minutos (Paso 8)

---

### FASE 1: Diseño del Agente

---

### Paso 1 — Definición del Rol y Alcance del Agente

**Objetivo:** Establecer con precisión el propósito, nombre, tono y restricciones del agente antes de redactar sus instrucciones técnicas.

**Instrucciones:**

1. Abre **Notepad++** o el Bloc de Notas en tu computadora.

2. Crea un nuevo archivo y guárdalo como:
   ```
   /Practica_03/DISENO_Agente_TuNombre.txt
   ```

3. En el archivo, redacta las respuestas a las siguientes preguntas de diseño (usa el formato indicado):

   ```
   === FICHA DE DISEÑO DEL AGENTE ===
   
   NOMBRE DEL AGENTE: Consultor Geológico Copilot
   
   ROL PRINCIPAL: 
   [Experto técnico en estándares internacionales de reporte geológico-minero
   y de petróleo y gas, especializado en validación de informes técnicos.]
   
   ESTÁNDARES DE REFERENCIA PRIMARIOS:
   - NI 43-101 (Canadian Securities Administrators, 2011)
   - Código JORC 2012 (Australasian Joint Ore Reserves Committee)
   - SPE-PRMS (Society of Petroleum Engineers, 2018) [referencia secundaria]
   
   ESTÁNDARES DE DATOS TÉCNICOS:
   - CWLS LAS 2.0 (registros de pozo)
   - ICS 2023 (nomenclatura cronoestratigráfica)
   
   TONO DE COMUNICACIÓN:
   [Técnico, preciso, conciso. Usa terminología geológica estándar.
   Evita ambigüedades. Siempre cita norma, sección y año.]
   
   TIPOS DE TAREAS PRINCIPALES:
   1. Validar cumplimiento de informes técnicos contra NI 43-101 y JORC
   2. Identificar secciones faltantes o incompletas según la norma
   3. Emitir recomendaciones de corrección con citas normativas
   4. Responder consultas técnicas sobre clasificación de recursos/reservas
   
   RESTRICCIONES EXPLÍCITAS:
   - NO proporcionar asesoría legal
   - NO inventar secciones normativas inexistentes
   - NO extrapolar sin respaldo documental
   - SIEMPRE declarar supuestos y advertir incertidumbres
   - SIEMPRE indicar que los resultados no sustituyen la revisión 
     por una Persona Calificada (Qualified Person / Competent Person)
   
   FORMATO DE SALIDA PREFERIDO PARA VALIDACIONES:
   [Tabla Markdown + JSON estructurado con campos: 
   estandar, criterio, veredicto, evidencia, citas, riesgos]
   ```

4. Revisa que todos los campos estén completos y guarda el archivo.

**Resultado Esperado:**
Un archivo `.txt` con la ficha de diseño completa del agente, con todos los campos definidos con precisión técnica.

**Verificación:**
- [ ] El archivo contiene nombre, rol, estándares, tono, tareas y restricciones definidos.
- [ ] Las restricciones incluyen explícitamente la mención a Persona Calificada/Competent Person.
- [ ] El formato de salida especifica tanto Markdown como JSON.

---

### Paso 2 — Redacción de las Instrucciones de Sistema del Agente

**Objetivo:** Redactar el prompt de sistema completo y detallado que configurará el comportamiento persistente del agente, incorporando todos los elementos definidos en el Paso 1.

**Instrucciones:**

1. Abre el archivo **`INSTRUCCIONES_SISTEMA_Plantilla.txt`** desde tu carpeta de práctica.

2. Observa la estructura de la plantilla. Contiene secciones marcadas con `[COMPLETAR]` que deberás rellenar.

3. Redacta las instrucciones de sistema completas. A continuación se proporciona el texto base que **debes personalizar** con tu criterio técnico (añade, ajusta o amplía según lo aprendido en la lección):

   ```text
   ========================================================
   INSTRUCCIONES DE SISTEMA — CONSULTOR GEOLÓGICO COPILOT
   Versión: 1.0 | Fecha: [FECHA DE HOY] | Autor: [TU NOMBRE]
   ========================================================
   
   ## ROL Y PROPÓSITO
   Eres "Consultor Geológico Copilot", un asistente técnico especializado 
   en la evaluación y validación de informes geológicos y de recursos 
   minerales conforme a estándares internacionales reconocidos. Tu objetivo 
   es ayudar a geólogos, ingenieros y equipos técnicos a verificar que sus 
   informes cumplen con los requisitos mínimos normativos antes de su 
   presentación formal o divulgación pública.
   
   ## ESTÁNDARES DE REFERENCIA AUTORIZADOS
   Basas todas tus evaluaciones en los siguientes estándares. Cita siempre 
   la norma específica, número de sección y año de publicación:
   
   MINERÍA Y RECURSOS MINERALES:
   - NI 43-101 (National Instrument 43-101, CSA, versión vigente 2011)
     Secciones clave: 2.1 (Persona Calificada), 3.1 (Requisitos del informe 
     técnico), 5.1–5.4 (Contenido mínimo), 6.1 (QA/QC)
   - Código JORC 2012 (Australasian JORC Code, edición 2012)
     Secciones clave: Tabla 1 (Criterios de reporte), Sección 9 (Recursos 
     Minerales), Sección 10 (Reservas de Mineral)
   
   PETRÓLEO Y GAS (referencia secundaria):
   - SPE-PRMS 2018 (Petroleum Resources Management System, SPE/WPC/AAPG/SPEE)
     Secciones clave: Sección 2 (Clasificación), Sección 3 (Definiciones)
   
   DATOS TÉCNICOS:
   - CWLS LAS 2.0 (Canadian Well Log Society, actualización 2017)
   - ICS Carta Cronoestratigráfica 2023 (International Commission on 
     Stratigraphy)
   
   ## COMPORTAMIENTO OBLIGATORIO
   1. CITACIÓN: Para CADA afirmación normativa que realices, incluye al 
      final de la oración la referencia en formato: 
      [Estándar, Sección X.X, Año]
   
   2. UNIDADES: Usa preferentemente el Sistema Internacional (SI). 
      Si el usuario provee unidades imperiales, convierte y muestra ambas: 
      "1.524 m (5 ft)".
   
   3. DECLARACIÓN DE SUPUESTOS: Cuando hagas inferencias, precede con: 
      "SUPUESTO: [descripción]".
   
   4. SOLICITUD DE INFORMACIÓN FALTANTE: Si el informe o consulta no 
      provee datos mínimos requeridos por la norma aplicable, solicita 
      explícitamente esos datos antes de emitir veredicto.
   
   5. SALIDA ESTRUCTURADA PARA VALIDACIONES: Cuando el usuario solicite 
      validar un informe, produce SIEMPRE:
      a) Una tabla Markdown resumen con columnas: 
         | Criterio | Veredicto | Evidencia | Cita Normativa | Riesgo |
      b) Un bloque JSON con el esquema CumplimientoNormativoInforme 
         (ver estructura al final de estas instrucciones)
      c) Una sección narrativa de "Recomendaciones de Corrección" 
         ordenadas por prioridad (CRÍTICO / IMPORTANTE / MENOR)
   
   ## RESTRICCIONES Y SALVAGUARDAS
   - NO proporciones asesoría legal ni financiera. Si la consulta tiene 
     implicaciones legales, indica: "Consulta con asesor legal especializado."
   - NO inventes secciones, criterios o requisitos normativos. Si no tienes 
     certeza, indica: "No tengo información suficiente sobre este punto en 
     mi base de conocimiento actual."
   - NO extrapoles resultados más allá de los datos provistos sin advertir 
     explícitamente la limitación.
   - SIEMPRE incluye al final de cualquier validación la siguiente 
     declaración de limitación:
     "⚠️ AVISO: Esta evaluación es de carácter orientativo y NO sustituye 
     la revisión formal por una Persona Calificada (Qualified Person) 
     certificada según NI 43-101 o un Competent Person según el Código JORC."
   
   ## ALCANCE DE CONOCIMIENTO
   - Dominio: Geociencias aplicadas, exploración y evaluación de recursos 
     minerales, petróleo y gas, formatos de datos de pozo.
   - Fuera de alcance: Geotecnia de obras civiles, sismología de terremotos, 
     climatología, geología ambiental (excepto cuando se mencione en el 
     contexto de informes de recursos).
   
   ## ESQUEMA JSON DE SALIDA PARA VALIDACIONES
   Cuando produzcas validaciones, usa esta estructura:
   
   {
     "agente": "Consultor Geológico Copilot",
     "version_instrucciones": "1.0",
     "estandar_evaluado": "[NI 43-101 | JORC 2012 | SPE-PRMS 2018]",
     "fecha_evaluacion": "[FECHA]",
     "resultados": [
       {
         "criterio": "[Nombre del criterio normativo]",
         "seccion_norma": "[Sección X.X]",
         "veredicto": "[CUMPLE | FALTA | INCOMPLETO | NO APLICA]",
         "evidencia": "[Descripción de lo encontrado o no encontrado]",
         "citas": [
           {
             "estandar": "[Nombre]",
             "seccion": "[X.X]",
             "anio": [XXXX],
             "url": "[URL oficial si disponible]"
           }
         ],
         "riesgo": "[CRÍTICO | IMPORTANTE | MENOR]",
         "recomendacion": "[Acción correctiva específica]"
       }
     ],
     "resumen_ejecutivo": "[Párrafo de síntesis con veredicto global]",
     "aviso_limitacion": "Esta evaluación NO sustituye la revisión por QP/CP."
   }
   ```

4. Personaliza el texto donde corresponda (fecha, autor) y añade al menos **3 criterios adicionales** de tu conocimiento de NI 43-101 o JORC que consideres importantes incluir en el esquema de validación.

5. Guarda el archivo como:
   ```
   /Practica_03/INSTRUCCIONES_SISTEMA_Final_TuNombre.txt
   ```

**Resultado Esperado:**
Un archivo de instrucciones de sistema completo, con rol definido, estándares citados, comportamientos obligatorios, restricciones y esquema JSON de salida. El archivo debe tener entre 400 y 700 palabras de contenido técnico sustantivo.

**Verificación:**
- [ ] Las instrucciones incluyen los 5 comportamientos obligatorios (citación, unidades, supuestos, solicitud de datos, salida estructurada).
- [ ] El esquema JSON contiene todos los campos: criterio, veredicto, evidencia, citas, riesgo, recomendación.
- [ ] La declaración de limitación (QP/CP) está incluida.
- [ ] Se añadieron al menos 3 criterios adicionales propios.

---

### Paso 3 — Revisión de los Extractos Normativos de Referencia

**Objetivo:** Familiarizarse con el contenido de los extractos de NI 43-101 y JORC 2012 proporcionados, identificando los criterios de cumplimiento más críticos que el agente deberá verificar.

**Instrucciones:**

1. Abre el archivo **`EXTRACTO_NI43101_Muestra.pdf`** desde tu carpeta de práctica.

2. Lee las secciones disponibles y completa la siguiente tabla en tu archivo de diseño (añádela al final de `DISENO_Agente_TuNombre.txt`):

   ```
   === CRITERIOS CLAVE IDENTIFICADOS PARA VALIDACIÓN ===
   
   NI 43-101 — Criterios Críticos:
   1. [Criterio 1 — Sección X.X — Descripción breve]
   2. [Criterio 2 — Sección X.X — Descripción breve]
   3. [Criterio 3 — Sección X.X — Descripción breve]
   4. [Criterio 4 — Sección X.X — Descripción breve]
   5. [Criterio 5 — Sección X.X — Descripción breve]
   
   JORC 2012 — Criterios Críticos:
   1. [Criterio 1 — Sección/Tabla X — Descripción breve]
   2. [Criterio 2 — Sección/Tabla X — Descripción breve]
   3. [Criterio 3 — Sección/Tabla X — Descripción breve]
   4. [Criterio 4 — Sección/Tabla X — Descripción breve]
   5. [Criterio 5 — Sección/Tabla X — Descripción breve]
   ```

3. Abre el archivo **`EXTRACTO_JORC2012_Muestra.pdf`** y completa la sección JORC de la tabla anterior.

4. Compara ambas listas: identifica **2 criterios que aparezcan en ambos estándares** (criterios equivalentes) y anótalos con el siguiente formato:
   ```
   === CRITERIOS EQUIVALENTES NI 43-101 ↔ JORC 2012 ===
   1. NI 43-101 Sec. X.X [Nombre] ↔ JORC Tabla 1 [Nombre]
      Diferencia clave: [descripción breve]
   2. NI 43-101 Sec. X.X [Nombre] ↔ JORC Tabla 1 [Nombre]
      Diferencia clave: [descripción breve]
   ```

**Resultado Esperado:**
La ficha de diseño actualizada con 5 criterios identificados por cada estándar y 2 pares de criterios equivalentes con sus diferencias clave documentadas.

**Verificación:**
- [ ] Se identificaron al menos 5 criterios por cada estándar.
- [ ] Se documentaron 2 criterios equivalentes entre ambos estándares.
- [ ] Cada criterio incluye referencia a sección/tabla específica.

> 💡 **Nota pedagógica:** Algunos criterios clave de NI 43-101 que deberías encontrar incluyen: declaración de Persona Calificada (Sec. 2.1), descripción de metodología de estimación de recursos (Sec. 3.1), procedimientos de QA/QC de muestreo (Sec. 6.1), y declaraciones de incertidumbre. En JORC, busca en la Tabla 1 los criterios de Geología y Contexto Geológico, Muestreo y Datos de Perforación, y Estimación y Reporte de Recursos.

---

### FASE 2: Configuración e Implementación del Agente

---

### Paso 4 — Creación del Agente en Microsoft Copilot Chat

**Objetivo:** Implementar el agente diseñado en la plataforma Microsoft Copilot Chat, configurando sus instrucciones de sistema y parámetros de comportamiento.

> 📌 **Bifurcación de procedimiento:** Sigue el **Plan A** si tienes acceso a creación de agentes en Copilot Studio. Si no tienes acceso, sigue el **Plan B** (prompt de sistema en conversación estándar). Tu instructor habrá indicado cuál plan seguir en la verificación inicial.

---

#### Plan A — Creación de Agente en Copilot Studio (Licencia con acceso a agentes)

**Instrucciones Plan A:**

1. Navega a **Microsoft Copilot Studio**: `https://copilotstudio.microsoft.com`

2. Inicia sesión con tu cuenta corporativa Microsoft 365.

3. En el panel principal, selecciona **"Crear"** → **"Nuevo agente"** (o "New agent" si la interfaz está en inglés).

4. En el asistente de creación, cuando se te solicite describir el agente, ingresa:
   ```
   Nombre del agente: Consultor Geológico Copilot
   
   Descripción: Agente especializado en validación de informes técnicos 
   geológicos contra estándares NI 43-101 y Código JORC 2012. Evalúa 
   cumplimiento normativo, identifica no conformidades y genera reportes 
   estructurados con citas a secciones específicas de cada norma.
   ```

5. Una vez creado el agente base, navega a la sección **"Instrucciones"** o **"System prompt"** del agente.

6. **Borra** el contenido predeterminado y **pega** el contenido completo de tu archivo `INSTRUCCIONES_SISTEMA_Final_TuNombre.txt`.

7. En la sección **"Conocimiento"** o **"Knowledge"**, selecciona **"Agregar conocimiento"** → **"Archivos"** y carga los siguientes documentos:
   - `EXTRACTO_NI43101_Muestra.pdf`
   - `EXTRACTO_JORC2012_Muestra.pdf`

8. Espera a que los documentos sean procesados (puede tomar 2–5 minutos). Verifica que aparezcan con estado **"Listo"** o **"Ready"**.

9. En la sección de **configuración de respuestas**, verifica que:
   - El nivel de creatividad/temperatura esté configurado en **"Preciso"** o el valor más bajo disponible (para minimizar variabilidad en respuestas normativas).
   - La opción de citar fuentes esté **habilitada** si está disponible.

10. Selecciona **"Guardar"** o **"Publicar"** el agente.

11. En la interfaz de Copilot Chat principal (`https://m365.cloud.microsoft/chat`), busca tu agente en la sección **"Agentes"** del panel lateral y selecciónalo para iniciar una conversación con él.

---

#### Plan B — Simulación mediante Prompt de Sistema en Conversación Estándar

**Instrucciones Plan B:**

1. Navega a **Microsoft Copilot Chat**: `https://m365.cloud.microsoft/chat`

2. Inicia una **nueva conversación** (botón "Nueva conversación" o equivalente).

3. Como **primer mensaje** de la conversación, ingresa el siguiente prompt de inicialización. Este mensaje establece el "rol" del agente para toda la sesión:

   ```
   Quiero que actúes como "Consultor Geológico Copilot" durante toda esta 
   conversación. A continuación te proporciono tus instrucciones de sistema 
   completas. Confirma que las has recibido y que estás listo para operar 
   bajo este rol respondiendo con: "Consultor Geológico Copilot activado. 
   Listo para evaluar informes técnicos."
   
   === INICIO DE INSTRUCCIONES DE SISTEMA ===
   [PEGA AQUÍ EL CONTENIDO COMPLETO DE TU ARCHIVO 
   INSTRUCCIONES_SISTEMA_Final_TuNombre.txt]
   === FIN DE INSTRUCCIONES DE SISTEMA ===
   ```

4. Envía el mensaje y espera la confirmación del agente.

5. A continuación, carga los documentos de referencia adjuntando los archivos PDF directamente en el chat (usando el ícono de clip 📎 o "Adjuntar archivo"):
   - `EXTRACTO_NI43101_Muestra.pdf`
   - `EXTRACTO_JORC2012_Muestra.pdf`

6. Después de cargar los archivos, envía el siguiente mensaje:
   ```
   He cargado los extractos normativos de NI 43-101 y JORC 2012 como 
   documentos de referencia. Por favor confirma que puedes acceder a su 
   contenido y resume en 3 puntos clave de cada estándar lo que has 
   identificado como criterios de validación más importantes.
   ```

7. Verifica que la respuesta del agente cite secciones específicas de los documentos cargados.

> ⚠️ **Nota sobre variabilidad de IA:** Si el agente no confirma correctamente el rol o produce una respuesta genérica sin citar los documentos, repite el Paso 3 con mayor especificidad. Esta variabilidad es normal en modelos de lenguaje. Intenta añadir al inicio del prompt: "Responde ÚNICAMENTE en el rol de Consultor Geológico Copilot conforme a las instrucciones de sistema que te proporcioné."

---

**Resultado Esperado (ambos planes):**
El agente "Consultor Geológico Copilot" está activo y responde en el rol definido, citando los estándares de referencia y confirmando su disponibilidad para validar informes técnicos.

**Verificación:**
- [ ] El agente responde con el nombre correcto "Consultor Geológico Copilot".
- [ ] La respuesta de confirmación cita al menos un criterio de NI 43-101 con número de sección.
- [ ] La respuesta de confirmación cita al menos un criterio de JORC 2012 con referencia a sección o Tabla 1.
- [ ] El agente menciona la restricción de no sustituir a una Persona Calificada/Competent Person.

---

### Paso 5 — Prueba de Funcionamiento Básico del Agente

**Objetivo:** Verificar que el agente responde correctamente a consultas técnicas simples antes de enfrentarlo al informe de validación completo.

**Instrucciones:**

1. Con el agente activo, envía el siguiente **prompt de prueba de rol**:
   ```
   Define brevemente qué es una "Persona Calificada" según NI 43-101 
   y qué es un "Competent Person" según el Código JORC 2012. 
   ¿Cuáles son las diferencias principales entre ambas figuras?
   ```

2. Evalúa la respuesta verificando que:
   - Cite NI 43-101 Sección 2.1 (o equivalente en el extracto).
   - Cite JORC 2012 con referencia específica.
   - Identifique al menos 2 diferencias entre QP y CP.
   - Use formato técnico y conciso.

3. Envía el siguiente **prompt de prueba de formato de salida**:
   ```
   Genera un ejemplo de validación en formato JSON para UN solo criterio: 
   "Declaración de Persona Calificada" según NI 43-101, asumiendo que 
   el informe NO contiene esta declaración. Usa el esquema JSON que tienes 
   configurado en tus instrucciones de sistema.
   ```

4. Verifica que el JSON producido contenga todos los campos requeridos: `criterio`, `seccion_norma`, `veredicto`, `evidencia`, `citas`, `riesgo`, `recomendacion`.

5. Envía el siguiente **prompt de prueba de conversión de unidades**:
   ```
   Un informe menciona una potencia de veta de 2.5 ft y una ley de oro 
   de 0.15 oz/t. Convierte estos valores al Sistema Internacional y 
   confirma qué unidades son las requeridas por NI 43-101.
   ```

6. Documenta las tres respuestas en un nuevo documento Word:
   ```
   /Practica_03/PRUEBAS_Agente_TuNombre.docx
   ```
   Incluye: el prompt enviado, la respuesta completa del agente, y tu evaluación breve (¿cumplió lo esperado? ¿qué mejorarías?).

**Resultado Esperado:**
El agente responde correctamente a las tres pruebas: definición con citas, JSON estructurado completo, y conversión de unidades con referencia normativa.

**Verificación:**
- [ ] Prueba 1: Respuesta cita NI 43-101 Sec. 2.1 y JORC con sección específica.
- [ ] Prueba 2: JSON contiene los 7 campos requeridos del esquema.
- [ ] Prueba 3: Conversión correcta (2.5 ft = 0.762 m; 0.15 oz/t ≈ 4.72 g/t) con referencia normativa.
- [ ] Las tres respuestas documentadas en `PRUEBAS_Agente_TuNombre.docx`.

> 💡 **Referencia de conversión:** 1 pie (ft) = 0.3048 m; 1 onza troy/tonelada corta (oz/short ton) ≈ 34.28 g/t; 1 oz/t (tonelada métrica) = 31.10 g/t. Verifica cuál convención usa el informe de muestra.

---

### FASE 3: Validación en Acción

---

### Paso 6 — Validación del Informe Técnico de Muestra con el Agente

**Objetivo:** Aplicar el agente creado para ejecutar una validación completa del informe técnico de muestra, identificando todas las no conformidades, secciones faltantes y datos insuficientes según NI 43-101 y JORC 2012.

**Instrucciones:**

1. Abre el archivo **`INFORME_TECNICO_MUESTRA_v1.docx`** desde tu carpeta de práctica. Lee el documento completo (aproximadamente 10–15 minutos). Mientras lees, toma nota mental de las secciones que parezcan incompletas o ausentes.

   > 📋 **Nota:** Este informe ha sido diseñado con **desviaciones normativas intencionales** para el ejercicio. Incluye al menos: ausencia de declaración de Persona Calificada, metodología de estimación de recursos incompleta, datos de QA/QC insuficientes, unidades inconsistentes, y al menos una categoría de recursos clasificada incorrectamente. Tu agente debe identificar estas y otras desviaciones.

2. Regresa a la conversación con tu agente "Consultor Geológico Copilot".

3. Adjunta el archivo `INFORME_TECNICO_MUESTRA_v1.docx` usando el ícono de adjuntar archivo (📎).

4. Envía el siguiente **prompt de validación completa**:
   ```
   Adjunto el informe técnico de recursos minerales "INFORME_TECNICO_MUESTRA_v1" 
   para su validación normativa completa.
   
   Por favor realiza las siguientes tareas:
   
   1. VALIDACIÓN NI 43-101: Evalúa el informe contra los requisitos mínimos 
      del estándar NI 43-101. Para cada criterio, indica: veredicto 
      (CUMPLE/FALTA/INCOMPLETO), evidencia específica del texto del informe, 
      cita normativa con sección y año, nivel de riesgo (CRÍTICO/IMPORTANTE/MENOR) 
      y recomendación de corrección.
   
   2. VALIDACIÓN JORC 2012: Repite el proceso anterior usando los criterios 
      de la Tabla 1 del Código JORC 2012.
   
   3. TABLA RESUMEN MARKDOWN: Produce una tabla comparativa con columnas: 
      | Criterio | NI 43-101 | JORC 2012 | Riesgo | Recomendación |
   
   4. REPORTE JSON: Genera el JSON completo de validación usando el esquema 
      CumplimientoNormativoInforme de tus instrucciones de sistema.
   
   5. RECOMENDACIONES PRIORIZADAS: Lista las correcciones necesarias 
      ordenadas por prioridad: primero CRÍTICO, luego IMPORTANTE, luego MENOR.
   
   6. DECLARACIÓN DE LIMITACIÓN: Incluye la declaración estándar de limitación 
      al final del reporte.
   
   Formato de respuesta: usa encabezados Markdown claros para cada sección.
   ```

5. Espera la respuesta completa del agente (puede tomar 30–60 segundos dependiendo de la longitud del informe y la velocidad de la conexión).

6. Si la respuesta es muy extensa y Copilot la trunca, envía el siguiente mensaje de continuación:
   ```
   Continúa con la sección [nombre de la sección que quedó incompleta]. 
   No repitas lo ya generado.
   ```

7. **Copia toda la respuesta del agente** y pégala en el archivo:
   ```
   /Practica_03/REPORTE_Validacion_Agente_TuNombre.docx
   ```
   Usa la plantilla `PLANTILLA_REPORTE_Validacion.docx` como estructura base.

8. Si detectas que el agente omitió algún criterio importante que identificaste durante tu lectura del informe (Paso 1), envía un **prompt de seguimiento**:
   ```
   Durante mi revisión manual identifiqué que el informe también presenta 
   [describe el problema específico]. ¿Cómo evalúas esto según [NI 43-101 / 
   JORC 2012]? ¿Qué sección normativa aplica?
   ```

**Resultado Esperado:**
Un reporte de validación completo generado por el agente que incluye: tabla Markdown de cumplimiento, JSON estructurado con todos los criterios evaluados, y lista priorizada de recomendaciones de corrección. El reporte debe identificar un mínimo de 6–8 criterios evaluados por cada estándar.

**Verificación:**
- [ ] La tabla Markdown contiene al menos 6 criterios evaluados para NI 43-101.
- [ ] La tabla Markdown contiene al menos 6 criterios evaluados para JORC 2012.
- [ ] El JSON producido sigue el esquema definido en las instrucciones de sistema.
- [ ] Las recomendaciones están ordenadas por nivel de riesgo (CRÍTICO primero).
- [ ] La declaración de limitación (QP/CP) aparece al final del reporte.
- [ ] El reporte está guardado en `REPORTE_Validacion_Agente_TuNombre.docx`.

---

### Paso 7 — Evaluación Comparativa: Agente vs. Lista de Verificación Manual

**Objetivo:** Evaluar la efectividad del agente comparando su reporte de validación con la lista de verificación manual de cumplimiento normativo, calculando métricas de precisión y cobertura.

**Instrucciones:**

1. Abre el archivo **`CHECKLIST_Cumplimiento_NI43101_JORC.xlsx`** desde tu carpeta de práctica.

2. El archivo contiene dos hojas:
   - **Hoja 1 "NI 43-101"**: Lista de 15 criterios de cumplimiento con una columna "Resultado Esperado" (pre-completada por el instructor con las desviaciones intencionales del informe).
   - **Hoja 2 "JORC 2012"**: Lista de 12 criterios equivalentes con su resultado esperado.

3. En la columna **"Resultado Agente"** de cada hoja, ingresa el veredicto que produjo tu agente para cada criterio (CUMPLE / FALTA / INCOMPLETO / NO APLICA / NO EVALUADO).

4. En la columna **"Coincidencia"**, ingresa una fórmula Excel para comparar automáticamente:
   ```excel
   =SI(C2=D2,"✅ COINCIDE","❌ DIFIERE")
   ```
   Donde C2 = "Resultado Esperado" y D2 = "Resultado Agente".

5. Al final de cada hoja, calcula las siguientes métricas en celdas designadas:

   ```excel
   Total criterios evaluados por el agente:
   =CONTAR.SI(D2:D16,"<>NO EVALUADO")
   
   Criterios con coincidencia exacta:
   =CONTAR.SI(E2:E16,"✅ COINCIDE")
   
   Tasa de precisión del agente (%):
   =(F_coincidencias / F_total_evaluados) * 100
   
   Criterios NO detectados por el agente (falsos negativos):
   =CONTAR.SI(D2:D16,"NO EVALUADO")
   ```

6. En la hoja **"Análisis Comparativo"** (Hoja 3), completa la tabla de resumen:

   | Métrica | NI 43-101 | JORC 2012 | Promedio |
   |---|---|---|---|
   | Total criterios en checklist | 15 | 12 | — |
   | Criterios evaluados por agente | ? | ? | ? |
   | Criterios con veredicto correcto | ? | ? | ? |
   | Tasa de precisión (%) | ? | ? | ? |
   | Criterios no detectados | ? | ? | ? |
   | Criterios mal clasificados | ? | ? | ? |

7. En la misma hoja, responde las siguientes preguntas de análisis (en celdas de texto o un documento Word adjunto):

   ```
   ANÁLISIS DE EFECTIVIDAD DEL AGENTE:
   
   a) ¿Qué tipos de criterios identificó mejor el agente? 
      (ej., criterios estructurales vs. técnicos vs. cuantitativos)
   
   b) ¿Qué criterios NO detectó o evaluó incorrectamente? 
      ¿A qué atribuyes estas omisiones?
   
   c) ¿Las instrucciones de sistema diseñadas fueron suficientes? 
      ¿Qué añadirías o modificarías para mejorar la cobertura?
   
   d) ¿Observaste variabilidad en las respuestas del agente? 
      ¿Cómo afectó esto la confiabilidad de la validación?
   
   e) ¿Qué limitaciones fundamentales tiene este enfoque 
      comparado con una revisión por un QP/CP real?
   ```

**Resultado Esperado:**
El archivo Excel completado con métricas calculadas y una tasa de precisión del agente documentada. Las preguntas de análisis respondidas con criterio técnico reflexivo.

**Verificación:**
- [ ] Todas las columnas "Resultado Agente" completadas en ambas hojas.
- [ ] Fórmulas de coincidencia funcionando correctamente.
- [ ] Métricas calculadas en la Hoja 3.
- [ ] Las 5 preguntas de análisis respondidas con al menos 2–3 oraciones cada una.

---

## 7. Validación y Pruebas Finales

Una vez completados los 7 pasos, realiza las siguientes verificaciones de cierre para confirmar que los entregables de la práctica están completos y correctos:

### Lista de Verificación Final de Entregables

| # | Entregable | Archivo | Estado |
|---|---|---|---|
| 1 | Ficha de diseño del agente con criterios normativos | `DISENO_Agente_TuNombre.txt` | ☐ |
| 2 | Instrucciones de sistema completas del agente | `INSTRUCCIONES_SISTEMA_Final_TuNombre.txt` | ☐ |
| 3 | Documentación de pruebas de funcionamiento básico | `PRUEBAS_Agente_TuNombre.docx` | ☐ |
| 4 | Reporte de validación generado por el agente | `REPORTE_Validacion_Agente_TuNombre.docx` | ☐ |
| 5 | Análisis comparativo con checklist manual | `CHECKLIST_Cumplimiento_NI43101_JORC.xlsx` (completado) | ☐ |

### Prueba de Calidad del Reporte de Validación

Revisa tu `REPORTE_Validacion_Agente_TuNombre.docx` y confirma que cumple los siguientes criterios de calidad mínimos:

- [ ] **Cobertura:** El reporte evalúa un mínimo de 10 criterios combinados entre NI 43-101 y JORC 2012.
- [ ] **Trazabilidad:** Cada veredicto incluye al menos una cita normativa con nombre del estándar, número de sección y año.
- [ ] **Estructura:** El reporte contiene tabla Markdown, bloque JSON y sección de recomendaciones priorizadas.
- [ ] **Rigor:** Las recomendaciones de corrección son específicas y accionables (no genéricas).
- [ ] **Salvaguardas:** La declaración de limitación QP/CP está presente al final del documento.
- [ ] **Formato JSON:** El JSON producido es sintácticamente válido (puedes verificarlo en `https://jsonlint.com`).

### Prueba de Robustez del Agente (Opcional — si hay tiempo disponible)

Si completaste los pasos anteriores con tiempo de sobra, realiza esta prueba adicional de robustez:

```
Envía al agente el siguiente prompt de "estrés normativo":

"El informe indica que los recursos se clasifican como 'Recursos Medidos' 
con una densidad de muestreo de 1 sondaje por km². ¿Es esta clasificación 
consistente con los criterios de confianza geológica requeridos por JORC 2012 
para la categoría Measured Resources? Cita la sección específica."

Evalúa si el agente: (a) cuestiona la clasificación, (b) cita JORC Tabla 1 
o Sección 9, (c) solicita información adicional antes de emitir veredicto.
```

---

## 8. Solución de Problemas

### Problema 1 — El agente no mantiene el rol entre mensajes y responde de forma genérica

**Síntoma:** Después de los primeros 2–3 intercambios, el agente deja de identificarse como "Consultor Geológico Copilot", omite las citas normativas obligatorias, o produce respuestas genéricas sin estructura JSON ni referencias a NI 43-101 / JORC.

**Causa:** Los modelos de lenguaje en conversaciones largas pueden experimentar "deriva de contexto" (context drift), donde las instrucciones de sistema iniciales pierden peso relativo a medida que la conversación crece. En el Plan B (simulación), este efecto es más pronunciado porque las instrucciones no están verdaderamente fijadas como system prompt persistente, sino como texto en el historial de conversación. En el Plan A, puede ocurrir si las instrucciones son muy extensas y exceden la ventana de contexto efectiva del modelo.

**Solución:**
1. **Solución inmediata:** Envía un prompt de "re-anclaje de rol" al inicio del siguiente mensaje:
   ```
   Recuerda: debes responder SIEMPRE como "Consultor Geológico Copilot" 
   siguiendo las instrucciones de sistema que te proporcioné al inicio. 
   Esto incluye: citar norma+sección+año, producir salida JSON cuando 
   corresponda, y declarar la limitación QP/CP. Retoma el análisis del 
   informe desde [punto donde quedaste].
   ```
2. **Solución estructural (Plan B):** Divide el análisis en conversaciones más cortas. En lugar de pedir toda la validación en un solo prompt, divide por estándar: primero NI 43-101 (nueva conversación con instrucciones), luego JORC (nueva conversación con instrucciones).
3. **Solución estructural (Plan A):** En Copilot Studio, verifica que las instrucciones de sistema estén en el campo correcto de "System prompt" y no en el historial de conversación. Reduce la longitud de las instrucciones eliminando redundancias y manteniendo solo los elementos esenciales (máximo 800 tokens recomendado).
4. **Prevención:** Añade al inicio de cada prompt de validación la frase: `[Actuando como Consultor Geológico Copilot]:` para reforzar el rol en cada turno.

---

### Problema 2 — El agente produce JSON con errores de sintaxis o estructura incompleta

**Síntoma:** El bloque JSON generado por el agente contiene errores de sintaxis (comillas faltantes, comas incorrectas, corchetes sin cerrar), campos faltantes del esquema definido, o el JSON está mezclado con texto narrativo sin delimitadores claros, impidiendo su uso programático.

**Causa:** Los modelos de lenguaje generan JSON como texto, no mediante un generador de JSON real. La probabilidad de errores de sintaxis aumenta cuando: (a) el JSON es muy largo (más de 50 criterios), (b) los valores de los campos contienen caracteres especiales o comillas anidadas, (c) las instrucciones de sistema no especificaron con suficiente precisión el formato exacto esperado, o (d) el modelo priorizó completar el contenido sobre mantener la sintaxis correcta.

**Solución:**
1. **Validación inmediata:** Copia el JSON producido y pégalo en `https://jsonlint.com`. El validador indicará exactamente la línea y tipo de error.
2. **Corrección por prompt:** Si hay errores de sintaxis, envía:
   ```
   El JSON que generaste contiene errores de sintaxis en [descripción del 
   error según JSONLint]. Por favor regenera SOLO el bloque JSON corregido, 
   asegurándote de que sea JSON válido. Usa comillas dobles para todas las 
   claves y valores de texto. Cierra correctamente todos los corchetes y llaves.
   ```
3. **Prevención por diseño de prompt:** Añade a tu prompt de validación la instrucción explícita:
   ```
   IMPORTANTE: El bloque JSON debe ser sintácticamente válido. 
   Delimítalo con ```json al inicio y ``` al final. 
   No incluyas comentarios dentro del JSON. 
   Si el JSON es muy extenso, divídelo en bloques separados por estándar.
   ```
4. **Alternativa para JSON largo:** Solicita el JSON en partes separadas:
   ```
   Genera el JSON SOLO para los criterios con veredicto "FALTA" o "INCOMPLETO". 
   Omite los criterios que "CUMPLEN" para reducir la longitud.
   ```
5. **Verificación de campos:** Si faltan campos del esquema, envía:
   ```
   El JSON producido no incluye el campo "recomendacion" en algunos criterios. 
   Por favor añade ese campo para todos los criterios donde el veredicto 
   no sea "CUMPLE", con una acción correctiva específica.
   ```

---

## 9. Limpieza del Entorno

Al finalizar la práctica, realiza las siguientes acciones de limpieza para mantener el entorno ordenado y proteger la confidencialidad:

### 9.1 Archivos Locales

1. Verifica que todos tus archivos de entregable estén guardados en tu carpeta local:
   ```
   /Practica_03/
   ├── DISENO_Agente_TuNombre.txt               ✅ Guardado
   ├── INSTRUCCIONES_SISTEMA_Final_TuNombre.txt  ✅ Guardado
   ├── PRUEBAS_Agente_TuNombre.docx              ✅ Guardado
   ├── REPORTE_Validacion_Agente_TuNombre.docx   ✅ Guardado
   └── CHECKLIST_Cumplimiento_NI43101_JORC.xlsx  ✅ Guardado (completado)
   ```

2. Sube los archivos de entregable a la carpeta de entrega del curso en OneDrive/SharePoint indicada por el instructor.

### 9.2 Copilot Chat — Historial de Conversación

1. En la interfaz de Copilot Chat, localiza la conversación de esta práctica en el historial.
2. Verifica que no hayas cargado datos reales o confidenciales (solo los archivos de muestra del curso).
3. Si deseas eliminar el historial por razones de privacidad corporativa, selecciona la conversación → **"Eliminar conversación"** (o equivalente según la versión de la interfaz).

### 9.3 Copilot Studio — Agente Creado (Solo Plan A)

1. Navega a `https://copilotstudio.microsoft.com`.
2. Localiza el agente "Consultor Geológico Copilot" que creaste.
3. **Opción A (conservar):** Si tu organización lo permite y el agente podría ser útil para trabajo real futuro, puedes conservarlo. Asegúrate de que el agente esté en estado **"No publicado"** o con acceso restringido a tu usuario.
4. **Opción B (eliminar):** Si el instructor indica que los agentes de práctica deben eliminarse, selecciona el agente → **"Configuración"** → **"Eliminar agente"** y confirma la eliminación.
5. Documenta la decisión tomada en tu reporte final.

### 9.4 Cierre de Sesión

1. Cierra todas las pestañas de Copilot Chat y Copilot Studio en tu navegador.
2. Si estás en una computadora compartida o de sala de cómputo, cierra completamente la sesión de Microsoft 365: `https://login.microsoftonline.com/logout`.
3. Limpia el caché del navegador si la política corporativa lo requiere.

---

## 10. Resumen

### Lo que Construiste en esta Práctica

En esta práctica de nivel **Crear** completaste el ciclo completo de diseño, implementación y evaluación de un agente de IA especializado en estándares geológicos:

| Fase | Lo que hiciste | Habilidad desarrollada |
|---|---|---|
| **Diseño** | Definiste rol, alcance, estándares, tono, restricciones y esquema de salida JSON | Ingeniería de prompts de sistema avanzada |
| **Implementación** | Configuraste el agente en Copilot Chat con instrucciones y documentos de referencia | Configuración de agentes de IA corporativos |
| **Validación** | Aplicaste el agente sobre un informe técnico real con desviaciones normativas | Automatización de procesos de QA/QC geológico |
| **Evaluación** | Comparaste resultados del agente con checklist manual y calculaste métricas de precisión | Pensamiento crítico sobre capacidades y límites de la IA |

### Conceptos Clave Aplicados

- **Grounding documental:** La efectividad del agente depende directamente de la calidad y especificidad de los documentos de referencia cargados. Un agente sin grounding en los estándares oficiales produce respuestas genéricas no trazables.
- **Instrucciones de sistema como contrato de comportamiento:** Las instrucciones de sistema no son sugerencias; son el contrato que define el comportamiento persistente del agente. La precisión terminológica y la especificidad de los comportamientos obligatorios determinan la confiabilidad del agente.
- **Salida estructurada para auditoría:** El uso de JSON con esquema predefinido transforma las respuestas del agente de texto narrativo a datos procesables, habilitando dashboards de cumplimiento, flujos de aprobación automatizados y trazabilidad de decisiones.
- **Limitaciones inherentes:** Ningún agente de IA reemplaza el juicio profesional de un Qualified Person (NI 43-101) o Competent Person (JORC). El agente es una herramienta de pre-validación que aumenta la eficiencia pero requiere supervisión humana experta para validación regulatoria formal.

### Recursos Adicionales

| Recurso | URL | Relevancia |
|---|---|---|
| Microsoft Copilot Studio — Documentación oficial | [learn.microsoft.com/es-es/microsoft-copilot-studio/](https://learn.microsoft.com/es-es/microsoft-copilot-studio/) | Creación y configuración de agentes |
| NI 43-101 — Texto completo | [bcsc.bc.ca](https://www.bcsc.bc.ca/securities-law/law-and-policy/instruments-and-policies/4/43-101) | Estándar de referencia primario (minería) |
| JORC Code 2012 — Texto completo | [jorc.org](https://www.jorc.org) | Estándar de referencia primario (minería) |
| SPE-PRMS 2018 | [spe.org/en/industry/petroleum-resources-management-system-prms/](https://www.spe.org/en/industry/petroleum-resources-management-system-prms/) | Estándar de referencia (petróleo y gas) |
| JSONLint — Validador JSON en línea | [jsonlint.com](https://jsonlint.com) | Verificación de JSON producido por el agente |
| ICS Carta Cronoestratigráfica 2023 | [stratigraphy.org/chart](https://stratigraphy.org/chart) | Nomenclatura estratigráfica de referencia |
| CWLS LAS 2.0 Specification | [cwls.org](https://www.cwls.org/wp-content/uploads/2017/02/Las2_Update_Feb2017.pdf) | Formato de registros de pozo |

### Próximos Pasos Sugeridos

Tras completar esta práctica, considera las siguientes extensiones para profundizar tu dominio:

1. **Ampliar el corpus normativo:** Añade extractos de SPE-PRMS 2018 al agente para cubrir también validaciones de recursos de petróleo y gas.
2. **Añadir validadores cuantitativos:** Diseña prompts que verifiquen umbrales numéricos específicos (ej., densidad mínima de muestreo para cada categoría JORC, intervalos de confianza requeridos).
3. **Integrar con flujos de trabajo:** Explora cómo el JSON producido por el agente podría alimentar automáticamente un dashboard de cumplimiento en Power BI o una lista de tareas en Microsoft Planner.
4. **Evaluación iterativa:** Usa el análisis comparativo del Paso 7 como línea base y refina las instrucciones de sistema en 2–3 iteraciones, midiendo la mejora en tasa de precisión con cada versión.
5. **Extensión a PRMS:** Diseña un segundo agente especializado exclusivamente en SPE-PRMS para validación de informes de recursos de petróleo y gas, aplicando la misma metodología de esta práctica.

---

> 📌 **Recordatorio final:** Los agentes de IA son herramientas de productividad y pre-validación. En contextos regulatorios reales (divulgación pública de recursos, reportes a bolsas de valores), la validación final **siempre** debe ser realizada y firmada por un profesional certificado como Qualified Person (NI 43-101) o Competent Person (JORC Code). El valor del agente está en acelerar la preparación del informe y detectar omisiones antes de la revisión formal, no en reemplazar el juicio profesional.

---
