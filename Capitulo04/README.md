---LAB_START---
LAB_ID: 04-00-01
---MARKDOWN---
# Uso de Copilot para transformar datos tabulares en descripciones para mapas o perfiles. Generación de alertas de riesgo geológico, evaluación predictiva de escenarios de fallas en modelos de trituración según tipos de formación, y preparación de presentaciones técnicas para comités.

## Metadatos

| Campo | Detalle |
|---|---|
| **Duración estimada** | 70 minutos |
| **Complejidad** | Media |
| **Nivel Bloom** | Aplicar |
| **Módulo / Práctica** | Módulo 4 — Práctica de Cierre Integradora |
| **Modalidad** | Individual con revisión grupal al final de cada bloque |
| **Versión del documento** | 1.0 |

---

## Descripción General

Esta práctica de cierre integra todas las competencias desarrolladas durante el curso en un flujo de trabajo geológico completo de mayor complejidad. Partiendo de un dataset tabular geológico y geotécnico ficticio pero realista, los participantes utilizarán Microsoft Copilot Chat para transformar datos crudos en descripciones narrativas de facies, generar un sistema de alertas de riesgo categorizadas, explorar escenarios conceptuales de falla en equipos de trituración según el tipo de formación, y finalmente consolidar todos los productos en una presentación técnica ejecutiva de 8 a 10 diapositivas lista para presentar ante un comité técnico. La práctica se organiza en cuatro bloques temáticos interconectados de creciente complejidad comunicativa y analítica.

> ⚠️ **Aviso de confidencialidad:** Durante toda la práctica utilice **únicamente** los datasets de muestra proporcionados por el instructor. **No cargue datos geológicos reales, confidenciales o propietarios de su empresa en Copilot Chat.**

> 💡 **Variabilidad de respuestas:** Copilot Chat puede generar respuestas diferentes en distintas sesiones para el mismo prompt. Esto es normal e inherente a los modelos de lenguaje. Si su respuesta difiere de los ejemplos mostrados, evalúe el contenido técnico, no la redacción exacta.

---

## Objetivos de Aprendizaje

Al finalizar esta práctica, el participante será capaz de:

- [ ] Aplicar Microsoft Copilot Chat para transformar datos tabulares geológicos crudos en descripciones narrativas estructuradas aptas para mapas geológicos y perfiles estratigráficos interpretados.
- [ ] Utilizar Copilot Chat para generar un sistema de alertas de riesgo geológico categorizadas (bajo / medio / alto / crítico) con justificación técnica por zona identificada.
- [ ] Aplicar Copilot Chat para realizar una evaluación predictiva conceptual de escenarios de falla en modelos de trituración según los tipos de formación geológica procesados, comprendiendo las limitaciones de la IA en este contexto.
- [ ] Crear con asistencia de Copilot Chat una presentación técnica ejecutiva para comité, integrando perfiles geológicos, alertas de riesgo y evaluaciones de escenarios en un formato profesional y comunicativamente efectivo.

---

## Prerrequisitos

### Conocimientos previos

| Área | Nivel requerido |
|---|---|
| Uso de Microsoft Copilot Chat (interfaz web) | Básico-intermedio (Prácticas 1 y 2 completadas) |
| Geología aplicada a minería: RQD, clasificación geomecánica, resistencia de roca | Básico |
| Procesos de trituración en minería: tipos de trituradores, relación con dureza del mineral | Deseable (no excluyente) |
| Microsoft Excel: apertura, visualización y edición básica de hojas de cálculo | Básico |
| Microsoft PowerPoint: creación y edición de diapositivas | Básico |

### Acceso y materiales

| Recurso | Estado requerido |
|---|---|
| Cuenta corporativa Microsoft 365 con Copilot Chat empresarial habilitado | ✅ Verificado por TI antes de la sesión |
| Archivo **`Lab04_Dataset_Geologico.xlsx`** (descargado desde OneDrive/SharePoint del curso) | ✅ Disponible localmente o en OneDrive |
| Archivo **`Lab04_Plantilla_Presentacion.pptx`** (plantilla corporativa) | ✅ Disponible localmente o en OneDrive |
| Microsoft Edge 120+ o Chrome 120+ | ✅ Instalado y actualizado |
| Microsoft Excel y PowerPoint (Microsoft 365, versión 2301 o superior) | ✅ Instalados |

---

## Entorno de Laboratorio

### Hardware mínimo recomendado

| Componente | Mínimo | Recomendado |
|---|---|---|
| Procesador | Intel Core i5 8ª gen / AMD Ryzen 5 | Intel Core i7 / AMD Ryzen 7 |
| Memoria RAM | 8 GB | 16 GB |
| Almacenamiento libre | 2 GB | 5 GB |
| Resolución de pantalla | 1366 × 768 px | 1920 × 1080 px |
| Conexión a internet | 10 Mbps | 25 Mbps o superior |

### Software requerido

| Aplicación | Versión mínima | Uso en esta práctica |
|---|---|---|
| Microsoft Copilot Chat (empresarial) | Vigente (M365 corporativo) | Todos los bloques |
| Microsoft Excel | M365 v2301+ | Visualización del dataset tabular |
| Microsoft PowerPoint | M365 v2301+ | Construcción de la presentación |
| Microsoft Edge / Chrome | 120+ | Acceso a Copilot Chat web |
| OneDrive / SharePoint | Vigente | Acceso a archivos de práctica |

### Configuración inicial (antes de comenzar)

Ejecute los siguientes pasos de configuración una sola vez al inicio de la sesión:

1. Abra su navegador (Edge o Chrome) y navegue a [https://m365.cloud.microsoft/chat](https://m365.cloud.microsoft/chat). Inicie sesión con su cuenta corporativa Microsoft 365.
2. Verifique que la interfaz muestre el indicador **"Trabajo"** o **"Work"** en la parte superior, confirmando que está en la versión empresarial con protección de datos.
3. Descargue desde la carpeta compartida de OneDrive/SharePoint del curso los archivos:
   - `Lab04_Dataset_Geologico.xlsx`
   - `Lab04_Plantilla_Presentacion.pptx`
4. Guarde ambos archivos en una carpeta local de fácil acceso, por ejemplo: `C:\Labs\Lab04\` o `~/Labs/Lab04/`.
5. Abra `Lab04_Dataset_Geologico.xlsx` en Microsoft Excel para familiarizarse con su estructura antes de comenzar.
6. Cree una nueva conversación en Copilot Chat haciendo clic en **"Nueva conversación"** (o el ícono de lápiz/papel). Mantenga esta pestaña abierta durante toda la práctica.

> 📋 **Nota del instructor:** El archivo `Lab04_Dataset_Geologico.xlsx` debe contener las dos hojas descritas en esta práctica: `Datos_Litologicos` y `Datos_Geotecnicos`. Los datos deben ser ficticios pero geológicamente consistentes. Consulte el Anexo de Materiales del curso para la especificación completa del dataset.

---

## Procedimiento Paso a Paso

La práctica se divide en **cuatro bloques temáticos**. Trabaje los bloques en orden secuencial, ya que cada uno genera insumos para el siguiente.

---

### Bloque 1: Transformación de Datos Tabulares en Descripciones Narrativas de Facies (15 minutos)

**Objetivo del bloque:** Convertir las filas de la tabla litológica del dataset en descripciones narrativas de facies geológicas aptas para leyendas de perfiles estratigráficos e informes de mapeo, aplicando el flujo de trabajo de transformación tabular estudiado en la Lección 4.1.

---

#### Paso 1.1: Revisión y comprensión del dataset litológico

**Objetivo:** Familiarizarse con la estructura del dataset antes de interactuar con Copilot.

**Instrucciones:**

1. En Excel, active la hoja **`Datos_Litologicos`** del archivo `Lab04_Dataset_Geologico.xlsx`. Observe que contiene las siguientes columnas:

   | Columna | Descripción |
   |---|---|
   | `Prof_Top_m` | Profundidad al tope del intervalo (metros) |
   | `Prof_Base_m` | Profundidad a la base del intervalo (metros) |
   | `Litologia` | Tipo litológico principal (ej. SAND, SHALE, LIMESTONE, DOLOMITE) |
   | `Estructuras_Sed` | Estructuras sedimentarias observadas |
   | `Contenido_Fosil` | Presencia y tipo de fósiles |
   | `Color_Munsell` | Color en notación Munsell |
   | `GR_api_prom` | Valor promedio de Gamma Ray (API) para el intervalo |
   | `RHOB_gcc_prom` | Densidad bulk promedio (g/cc) |
   | `Dureza_MPa` | Dureza de la roca (MPa) |
   | `Abrasividad_AI` | Índice de abrasividad (Cerchar Abrasivity Index) |

2. Identifique cuántas filas (intervalos) contiene la hoja. El dataset de práctica tiene **10 intervalos** que van de 100 m a 200 m de profundidad.
3. Seleccione y copie **todas las celdas de la tabla** (incluyendo encabezados). Use `Ctrl+A` dentro de la tabla y luego `Ctrl+C`.

**Resultado esperado:** Comprensión clara de la estructura del dataset y contenido copiado en el portapapeles.

**Verificación:** Confirme que ha copiado los encabezados y las 10 filas de datos. La selección debe incluir todas las 10 columnas.

---

#### Paso 1.2: Carga del dataset en Copilot y solicitud de descripción narrativa de facies

**Objetivo:** Usar Copilot Chat para transformar los datos tabulares en descripciones narrativas estructuradas por intervalo.

**Instrucciones:**

1. Cambie a la pestaña del navegador con Copilot Chat.
2. En el campo de entrada del chat, pegue los datos copiados del paso anterior (`Ctrl+V`). Los datos aparecerán como texto tabulado.

   > 💡 **Alternativa:** Si su versión de Copilot Chat permite adjuntar archivos, haga clic en el ícono de adjunto (📎) y cargue directamente el archivo `Lab04_Dataset_Geologico.xlsx`. Luego indique en el prompt que trabaje con la hoja `Datos_Litologicos`.

3. Después de pegar los datos, escriba el siguiente prompt estructurado y presione **Enter**:

   ```
   Actúa como geólogo sedimentólogo senior con experiencia en descripción de facies para 
   informes de mapeo geológico. A continuación te proporciono una tabla de datos litológicos 
   de 10 intervalos de perforación entre 100 m y 200 m de profundidad.

   Para cada intervalo, genera una descripción narrativa de facies geológica que incluya:
   1. Denominación de la facies (nombre descriptivo corto, máximo 5 palabras)
   2. Descripción sedimentológica (2-3 oraciones): litología principal, estructuras sedimentarias, 
      color y contenido fosilífero
   3. Interpretación de ambiente deposicional (1 oración)
   4. Propiedades mecánicas relevantes: dureza y abrasividad con su clasificación cualitativa 
      (baja/media/alta/muy alta)
   5. Aptitud para leyenda de perfil estratigráfico (1 oración resumen)

   Presenta los resultados en formato de lista numerada, uno por intervalo, con subtítulos claros.
   Usa terminología geológica técnica apropiada para un informe profesional.

   [PEGAR AQUÍ LOS DATOS DE LA TABLA]
   ```

   > 📝 **Nota:** Reemplace `[PEGAR AQUÍ LOS DATOS DE LA TABLA]` con los datos reales copiados de Excel, o si ya los pegó antes del prompt, reorganice el mensaje para que los datos precedan al prompt de instrucción.

4. Espere la respuesta de Copilot (aproximadamente 15-30 segundos).

**Resultado esperado:** Copilot genera 10 descripciones narrativas de facies, una por intervalo, con la estructura de 5 puntos solicitada. Las descripciones deben ser geológicamente coherentes con los valores de GR, RHOB, litología y estructuras sedimentarias del dataset.

**Verificación:** Revise que:
- [ ] Cada descripción tiene los 5 componentes solicitados.
- [ ] Las denominaciones de facies son descriptivas y coherentes (ej. "Arenisca de grano medio con laminación paralela").
- [ ] La clasificación de dureza y abrasividad es consistente con los valores numéricos de `Dureza_MPa` y `Abrasividad_AI`.
- [ ] El lenguaje es técnico y apropiado para un informe geológico profesional.

---

#### Paso 1.3: Refinamiento y solicitud de tabla resumen de facies

**Objetivo:** Refinar las descripciones y generar una tabla resumen apta para leyenda de perfil.

**Instrucciones:**

1. Evalúe la respuesta del paso anterior. Si alguna descripción le parece imprecisa o inconsistente, identifíquela.
2. Envíe el siguiente prompt de refinamiento en la **misma conversación** (no abra una nueva):

   ```
   Excelente trabajo. Ahora, basándote en las 10 descripciones de facies que generaste, 
   crea una tabla resumen con las siguientes columnas:

   | Intervalo (m) | Código Facies | Denominación Facies | Litología Principal | 
   | Ambiente Deposicional | Dureza | Abrasividad | Color HEX sugerido para perfil |

   Para el Color HEX, sugiere un color representativo coherente con los códigos litológicos 
   estándar (arenisca = dorado #DAA520, lutita = gris #808080, caliza = azul #1E90FF, 
   dolomía = verde #8FBC8F). Si hay variantes mixtas, propón un color intermedio justificado.

   Presenta la tabla en formato Markdown.
   ```

3. Copie la tabla generada por Copilot y péguela en un archivo de texto (Notepad o Notepad++) guardado como `Lab04_Tabla_Facies.txt` en su carpeta de trabajo.

**Resultado esperado:** Una tabla Markdown de 10 filas con los 8 campos solicitados, incluyendo códigos de color HEX coherentes con la paleta litológica estándar de la Lección 4.1.

**Verificación:**
- [ ] La tabla tiene exactamente 10 filas de datos más la fila de encabezado.
- [ ] Los colores HEX son coherentes con la paleta estándar estudiada.
- [ ] El archivo `Lab04_Tabla_Facies.txt` está guardado correctamente.

---

### Bloque 2: Generación de Alertas de Riesgo Geológico (15 minutos)

**Objetivo del bloque:** Utilizar Copilot Chat para analizar parámetros geotécnicos del dataset y generar un sistema de alertas de riesgo categorizadas con justificación técnica y recomendaciones de mitigación.

---

#### Paso 2.1: Carga de datos geotécnicos y solicitud de sistema de alertas

**Objetivo:** Generar alertas de riesgo categorizadas basadas en parámetros geotécnicos del dataset.

**Instrucciones:**

1. Regrese a Excel y active la hoja **`Datos_Geotecnicos`** del archivo `Lab04_Dataset_Geologico.xlsx`. Esta hoja contiene:

   | Columna | Descripción |
   |---|---|
   | `Prof_Top_m` | Profundidad al tope del intervalo (metros) |
   | `Prof_Base_m` | Profundidad a la base del intervalo (metros) |
   | `Litologia` | Tipo litológico |
   | `RQD_pct` | Rock Quality Designation (%) |
   | `Indice_Fracturacion` | Número de fracturas por metro |
   | `Presencia_Falla` | Indicador de falla (Sí/No) |
   | `Presion_Poros_MPa` | Presión de poros estimada (MPa) |
   | `UCS_MPa` | Resistencia a la compresión uniaxial (MPa) |
   | `Cohesion_MPa` | Cohesión del material (MPa) |
   | `Angulo_Friccion_deg` | Ángulo de fricción interna (grados) |

2. Copie todos los datos de esta hoja (encabezados + 10 filas).
3. En Copilot Chat, **continúe en la misma conversación** del Bloque 1 y envíe el siguiente prompt:

   ```
   Ahora trabajaremos con los datos geotécnicos del mismo sondaje. A continuación te 
   proporciono la tabla de parámetros geotécnicos para los mismos 10 intervalos.

   Actúa como ingeniero geotécnico especialista en minería subterránea y a cielo abierto.
   Analiza los datos y genera un sistema de alertas de riesgo geológico-geotécnico con 
   las siguientes especificaciones:

   CATEGORÍAS DE ALERTA:
   - 🟢 BAJO: Condiciones estables, operación normal sin restricciones especiales
   - 🟡 MEDIO: Condiciones moderadas, monitoreo recomendado y medidas preventivas
   - 🟠 ALTO: Condiciones adversas, intervención técnica requerida antes de operación
   - 🔴 CRÍTICO: Condiciones de riesgo severo, suspensión de operaciones y evaluación inmediata

   Para cada intervalo genera:
   1. Nivel de alerta asignado con justificación técnica (menciona los parámetros específicos 
      que determinaron la clasificación, con sus valores)
   2. Principales mecanismos de falla identificados (máximo 3)
   3. Recomendaciones técnicas de mitigación (mínimo 2 acciones concretas)
   4. Parámetro crítico dominante (el factor de mayor peso en la decisión)

   Al final, genera un resumen ejecutivo de 3-4 oraciones sobre el estado general del 
   macizo rocoso en el intervalo 100-200 m y las zonas de mayor atención prioritaria.

   [PEGAR AQUÍ LOS DATOS GEOTÉCNICOS]
   ```

4. Espere la respuesta completa de Copilot.

**Resultado esperado:** Un sistema de alertas completo con los 4 componentes por intervalo y el resumen ejecutivo final. Las alertas deben ser coherentes con los valores de RQD (RQD < 25% = muy pobre calidad), índice de fracturación, presencia de fallas y UCS.

**Verificación:**
- [ ] Se generaron alertas para los 10 intervalos.
- [ ] Los niveles de alerta son coherentes con los valores del dataset (ej. RQD < 25% + presencia de falla = alerta ALTO o CRÍTICO).
- [ ] Cada alerta incluye justificación con valores numéricos específicos del dataset.
- [ ] Las recomendaciones son técnicamente aplicables (no genéricas).

---

#### Paso 2.2: Solicitud de tabla consolidada de alertas

**Objetivo:** Obtener una tabla consolidada de alertas para incorporar en la presentación técnica.

**Instrucciones:**

1. En la misma conversación, envíe el siguiente prompt:

   ```
   Perfecto. Ahora consolida todas las alertas en una tabla resumen ejecutiva con 
   las siguientes columnas:

   | Intervalo (m) | Litología | Nivel Alerta | Parámetro Crítico | 
   | Mecanismo Falla Principal | Acción Prioritaria |

   Ordena la tabla de mayor a menor criticidad (primero los CRÍTICOS, luego ALTOS, 
   luego MEDIOS, luego BAJOS). Presenta en formato Markdown.

   Adicionalmente, indica cuántos intervalos caen en cada categoría de alerta 
   (conteo por categoría).
   ```

2. Copie la tabla y el conteo generados. Guárdelos en un nuevo archivo `Lab04_Alertas_Riesgo.txt`.

**Resultado esperado:** Tabla ordenada por criticidad con los 6 campos solicitados y conteo por categoría.

**Verificación:**
- [ ] La tabla está ordenada correctamente por nivel de criticidad.
- [ ] El conteo por categoría suma exactamente 10 intervalos.
- [ ] El archivo `Lab04_Alertas_Riesgo.txt` está guardado.

---

### Bloque 3: Evaluación Predictiva Conceptual de Escenarios de Falla en Trituración (15 minutos)

**Objetivo del bloque:** Explorar con Copilot Chat escenarios conceptuales de falla en equipos de trituración según las características litológicas y mecánicas identificadas, comprendiendo las limitaciones de este análisis como aproximación conceptual asistida por IA y no como simulación física.

> ⚠️ **Advertencia metodológica importante:** El análisis de este bloque es una **evaluación conceptual cualitativa** basada en relaciones conocidas entre propiedades de roca y comportamiento de equipos de trituración. **No reemplaza** modelos de simulación física, ensayos de laboratorio (Bond Work Index, pruebas de desgaste) ni la experiencia de ingenieros de proceso especializados. Copilot Chat no tiene acceso a parámetros operacionales reales de sus equipos. Utilice estos resultados únicamente como punto de partida para discusión técnica.

---

#### Paso 3.1: Contextualización del escenario de trituración

**Objetivo:** Establecer el contexto operacional para que Copilot genere evaluaciones conceptualmente relevantes.

**Instrucciones:**

1. En la misma conversación de Copilot Chat, envíe el siguiente prompt de contextualización:

   ```
   Cambiamos de enfoque. Ahora trabajaremos en la evaluación conceptual de riesgo 
   operacional para equipos de trituración.

   CONTEXTO OPERACIONAL:
   - Operación: Mina a cielo abierto con planta de procesamiento mineral
   - Equipos de trituración: Triturador primario de mandíbulas (jaw crusher), 
     triturador secundario cónico (cone crusher), triturador terciario de impacto (VSI)
   - El material a procesar proviene de los 10 intervalos litológicos ya analizados
   - Los equipos operan en secuencia: el material de todos los intervalos se mezcla 
     en proporciones variables durante la operación

   Con base en los datos de litología, dureza (MPa), abrasividad (Índice Cerchar) 
   y las descripciones de facies que ya generamos, realiza una evaluación conceptual 
   del riesgo operacional para los equipos de trituración.

   Para cada tipo de triturador, identifica:
   1. Los 3 intervalos litológicos que representan mayor riesgo para ese equipo específico
   2. El escenario de falla conceptual más probable (desgaste acelerado de piezas, 
      bloqueo por material arcilloso, sobrecarga por material muy duro, fragmentación 
      irregular, etc.)
   3. Indicadores de alerta temprana que el operador debería monitorear
   4. Recomendación conceptual de ajuste operacional o mantenimiento preventivo

   Recuerda indicar explícitamente que esta es una evaluación conceptual cualitativa 
   y no un modelo de simulación física.
   ```

2. Espere la respuesta completa.

**Resultado esperado:** Evaluación conceptual para los tres tipos de trituradores, con los 4 componentes por equipo. Copilot debe incluir la advertencia metodológica sobre el carácter conceptual del análisis.

**Verificación:**
- [ ] Se generó evaluación para los tres tipos de trituradores (mandíbulas, cónico, VSI).
- [ ] Los intervalos identificados como de mayor riesgo son coherentes con los valores de dureza y abrasividad del dataset (mayor dureza y abrasividad = mayor riesgo para piezas de desgaste).
- [ ] Copilot incluye alguna mención al carácter conceptual/cualitativo del análisis.
- [ ] Los escenarios de falla son técnicamente plausibles para cada tipo de equipo.

---

#### Paso 3.2: Matriz de criticidad litología-equipo

**Objetivo:** Generar una matriz de criticidad que relacione tipos de formación con equipos de trituración para uso en la presentación.

**Instrucciones:**

1. En la misma conversación, envíe el siguiente prompt:

   ```
   Basándote en el análisis anterior, genera una Matriz de Criticidad Litología-Equipo 
   en formato de tabla Markdown con la siguiente estructura:

   - Filas: Los 4 tipos litológicos principales presentes en el dataset 
     (SAND, SHALE, LIMESTONE, DOLOMITE)
   - Columnas: Triturador de Mandíbulas | Triturador Cónico | Triturador VSI
   - Contenido de cada celda: Nivel de criticidad (BAJA / MEDIA / ALTA / MUY ALTA) 
     + escenario de falla dominante en 3-5 palabras

   Después de la tabla, agrega una sección de "Recomendaciones Operacionales Prioritarias" 
   con las 5 acciones más importantes para reducir el riesgo de falla en los equipos, 
   ordenadas de mayor a menor impacto esperado.

   Incluye al inicio de tu respuesta un párrafo breve recordando las limitaciones 
   metodológicas de esta evaluación conceptual.
   ```

2. Copie la matriz y las recomendaciones. Guárdelas en `Lab04_Matriz_Trituración.txt`.

**Resultado esperado:** Matriz de 4×3 con niveles de criticidad y escenarios de falla, más 5 recomendaciones operacionales priorizadas, precedidas por el párrafo de limitaciones metodológicas.

**Verificación:**
- [ ] La matriz tiene 4 filas (litologías) × 3 columnas (equipos) correctamente estructurada.
- [ ] Los niveles de criticidad son coherentes con las propiedades mecánicas conocidas de cada litología (ej. dolomía dura = criticidad ALTA/MUY ALTA para trituradores).
- [ ] El archivo `Lab04_Matriz_Trituración.txt` está guardado.

---

### Bloque 4: Preparación de Presentación Técnica para Comité (20 minutos)

**Objetivo del bloque:** Integrar todos los productos de los bloques anteriores en una presentación PowerPoint de 8 a 10 diapositivas para comité técnico, utilizando Copilot para generar el texto, mensajes clave, conclusiones y recomendaciones operacionales.

---

#### Paso 4.1: Generación del guion completo de la presentación

**Objetivo:** Crear el contenido textual completo de la presentación antes de construirla en PowerPoint.

**Instrucciones:**

1. En la misma conversación de Copilot Chat, envíe el siguiente prompt:

   ```
   Ahora integraremos todo el trabajo previo en una presentación técnica ejecutiva 
   para comité técnico de operaciones mineras.

   AUDIENCIA: Comité técnico compuesto por Gerente de Mina, Jefe de Geología, 
   Jefe de Operaciones y Jefe de Mantenimiento. Nivel técnico alto pero con tiempo 
   limitado (presentación de 15-20 minutos).

   OBJETIVO DE LA PRESENTACIÓN: Comunicar el estado geológico-geotécnico del 
   sondaje Zona Norte (100-200 m), las alertas de riesgo identificadas y las 
   recomendaciones operacionales para los equipos de trituración.

   Genera el guion completo de una presentación de 9 diapositivas con la 
   siguiente estructura:

   DIAPOSITIVA 1 - PORTADA:
   - Título principal de la presentación
   - Subtítulo con alcance y fecha
   - Área/zona geológica

   DIAPOSITIVA 2 - AGENDA / CONTENIDO:
   - Lista de 5-6 puntos del contenido a cubrir

   DIAPOSITIVA 3 - RESUMEN EJECUTIVO:
   - 4-5 bullets con los hallazgos más importantes (los que el comité debe recordar)
   - Mensaje clave de 1 oración (el "take-away" principal)

   DIAPOSITIVA 4 - PERFIL LITOLÓGICO Y FACIES:
   - Título de sección
   - Descripción de las facies más representativas (3-4 bullets)
   - Nota metodológica breve

   DIAPOSITIVA 5 - MAPA DE ALERTAS DE RIESGO GEOTÉCNICO:
   - Título de sección
   - Distribución de alertas por categoría (usar el conteo del Bloque 2)
   - Zonas de atención prioritaria (2-3 bullets)
   - Mensaje clave de seguridad

   DIAPOSITIVA 6 - ANÁLISIS DETALLADO DE ZONAS CRÍTICAS:
   - Los 3 intervalos de mayor criticidad con sus parámetros clave
   - Mecanismos de falla identificados
   - Impacto operacional estimado

   DIAPOSITIVA 7 - EVALUACIÓN DE RIESGO EN TRITURACIÓN:
   - Título de sección
   - Resumen de la matriz de criticidad litología-equipo
   - Los 2 escenarios de falla de mayor impacto
   - Advertencia metodológica (evaluación conceptual)

   DIAPOSITIVA 8 - RECOMENDACIONES OPERACIONALES:
   - Las 5 recomendaciones prioritarias del Bloque 3 en formato de bullets ejecutivos
   - Responsable sugerido para cada acción (Geología / Operaciones / Mantenimiento)
   - Plazo sugerido (inmediato / corto plazo / mediano plazo)

   DIAPOSITIVA 9 - CONCLUSIONES Y PRÓXIMOS PASOS:
   - 3-4 conclusiones técnicas principales
   - 3 próximos pasos concretos con fechas tentativas
   - Cierre con mensaje de valor del análisis geológico integrado

   Para cada diapositiva, indica:
   - TÍTULO: [título de la diapositiva]
   - CONTENIDO PRINCIPAL: [bullets o texto]
   - NOTAS DEL PRESENTADOR: [1-3 oraciones de apoyo para el presentador]
   - SUGERENCIA VISUAL: [qué tipo de gráfico, tabla o imagen sería ideal]
   ```

2. Espere la respuesta completa. Esta puede ser extensa (5-8 minutos de lectura). Revísela con atención.
3. Copie todo el guion generado y guárdelo en `Lab04_Guion_Presentacion.txt`.

**Resultado esperado:** Guion completo de 9 diapositivas con los 4 componentes por diapositiva (título, contenido, notas del presentador, sugerencia visual), integrado con los hallazgos de los bloques anteriores.

**Verificación:**
- [ ] El guion cubre las 9 diapositivas con la estructura solicitada.
- [ ] El contenido es coherente con los análisis de los bloques 1, 2 y 3.
- [ ] Las notas del presentador son útiles y adicionales al contenido de la diapositiva.
- [ ] Las sugerencias visuales son específicas y realizables en PowerPoint.

---

#### Paso 4.2: Construcción de la presentación en PowerPoint

**Objetivo:** Transferir el guion generado por Copilot a la plantilla corporativa de PowerPoint.

**Instrucciones:**

1. Abra el archivo `Lab04_Plantilla_Presentacion.pptx` en Microsoft PowerPoint.
2. La plantilla tiene diseño corporativo preconfigurado. Utilice las diapositivas de plantilla disponibles (portada, contenido, sección, datos, cierre).
3. Construya las 9 diapositivas siguiendo el guion de `Lab04_Guion_Presentacion.txt`:
   - **Diapositiva 1 (Portada):** Use el diseño de portada de la plantilla. Ingrese el título y subtítulo del guion.
   - **Diapositivas 2-8:** Use el diseño de contenido estándar. Copie los bullets del guion en el área de contenido. Copie las notas del presentador en el panel de notas de PowerPoint (Vista → Notas).
   - **Diapositiva 9 (Cierre):** Use el diseño de cierre de la plantilla.
4. Para la **Diapositiva 5** (Mapa de Alertas), inserte una tabla simple de 5 filas × 3 columnas con los datos de conteo de alertas:

   | Categoría | Cantidad de Intervalos | % del Total |
   |---|---|---|
   | 🔴 CRÍTICO | [dato del Bloque 2] | [calcular] |
   | 🟠 ALTO | [dato del Bloque 2] | [calcular] |
   | 🟡 MEDIO | [dato del Bloque 2] | [calcular] |
   | 🟢 BAJO | [dato del Bloque 2] | [calcular] |

5. Para la **Diapositiva 7** (Evaluación de Riesgo en Trituración), inserte la matriz de criticidad del Bloque 3 como tabla de 5 filas × 4 columnas (encabezado + 4 litologías).
6. Guarde el archivo como `Lab04_Presentacion_Comite_[SuNombre].pptx`.

**Resultado esperado:** Presentación de 9 diapositivas completa, con contenido del guion transferido correctamente, tablas de datos incluidas y notas del presentador en cada diapositiva.

**Verificación:**
- [ ] La presentación tiene exactamente 9 diapositivas.
- [ ] Cada diapositiva tiene título, contenido y notas del presentador completados.
- [ ] Las tablas de alertas y de criticidad están incluidas y son legibles.
- [ ] El archivo está guardado con el nombre correcto.

---

#### Paso 4.3: Generación del mensaje de apertura y cierre con Copilot

**Objetivo:** Refinar la comunicación ejecutiva con frases de apertura y cierre de alto impacto.

**Instrucciones:**

1. Regrese a Copilot Chat y envíe el siguiente prompt final:

   ```
   Para cerrar la preparación de la presentación, necesito dos textos adicionales:

   TEXTO 1 - APERTURA (para el presentador, antes de mostrar la Diapositiva 1):
   Escribe un párrafo de apertura de 4-5 oraciones que:
   - Establezca la relevancia del análisis geológico integrado para las decisiones 
     operacionales de la mina
   - Mencione brevemente el alcance del trabajo (sondaje Zona Norte, 100-200 m)
   - Genere expectativa sobre los hallazgos críticos
   - Sea apropiado para una audiencia de gerentes y jefes técnicos
   - Tono: profesional, directo, orientado a decisiones

   TEXTO 2 - CIERRE (para el presentador, después de la Diapositiva 9):
   Escribe un párrafo de cierre de 3-4 oraciones que:
   - Refuerce el valor del análisis geológico integrado como herramienta de gestión 
     de riesgo operacional
   - Invite a la discusión y preguntas del comité
   - Destaque la disponibilidad del equipo técnico para profundizar en cualquier 
     punto de interés
   - Cierre con un llamado a la acción concreto (aprobación de recomendaciones, 
     asignación de responsables, definición de cronograma)
   ```

2. Copie los dos textos generados y agréguelos como notas en las diapositivas 1 y 9 respectivamente de su presentación PowerPoint.
3. Guarde nuevamente el archivo PowerPoint.

**Resultado esperado:** Dos textos de alta calidad comunicativa para apertura y cierre de la presentación, integrados como notas del presentador en las diapositivas correspondientes.

**Verificación:**
- [ ] El texto de apertura cumple los 5 criterios especificados.
- [ ] El texto de cierre incluye el llamado a la acción concreto.
- [ ] Ambos textos están agregados como notas en las diapositivas 1 y 9.

---

## Validación y Pruebas Finales

Una vez completados los cuatro bloques, realice las siguientes verificaciones de calidad integral:

### Lista de verificación de productos entregables

| Producto | Archivo | Estado |
|---|---|---|
| Tabla de facies geológicas | `Lab04_Tabla_Facies.txt` | ☐ Completado |
| Sistema de alertas de riesgo | `Lab04_Alertas_Riesgo.txt` | ☐ Completado |
| Matriz de criticidad trituración | `Lab04_Matriz_Trituración.txt` | ☐ Completado |
| Guion completo de presentación | `Lab04_Guion_Presentacion.txt` | ☐ Completado |
| Presentación PowerPoint | `Lab04_Presentacion_Comite_[SuNombre].pptx` | ☐ Completado |

### Prueba de coherencia interna

Realice esta prueba final de coherencia cruzando los productos:

1. **Prueba de coherencia litológica:** Verifique que los intervalos identificados como CRÍTICO o ALTO en el Bloque 2 correspondan a los mismos intervalos identificados como de mayor riesgo para los equipos de trituración en el Bloque 3. ¿Existe correlación lógica entre alta fracturación/fallas y mayor riesgo de bloqueo en trituradores?

2. **Prueba de coherencia narrativa:** Abra su presentación PowerPoint y léala de principio a fin como si fuera el presentador. ¿El hilo narrativo es lógico? ¿Las conclusiones de la Diapositiva 9 se derivan claramente del análisis de las diapositivas 3-8?

3. **Prueba de completitud técnica:** Envíe el siguiente prompt de validación a Copilot Chat:

   ```
   Actúa como revisor técnico senior. Voy a compartirte el guion de mi presentación 
   para comité técnico. Por favor evalúa:
   1. ¿Están presentes todos los elementos técnicos esenciales para una presentación 
      de riesgo geológico-operacional?
   2. ¿Hay alguna inconsistencia técnica evidente entre las secciones?
   3. ¿Qué elemento adicional fortalecería más la presentación?
   
   [PEGAR AQUÍ EL CONTENIDO DE Lab04_Guion_Presentacion.txt]
   ```

4. Revise la retroalimentación de Copilot e incorpore al menos **una mejora sugerida** en su presentación PowerPoint.

### Criterios de éxito de la práctica

| Criterio | Indicador de logro |
|---|---|
| Transformación tabular efectiva | Las descripciones narrativas son geológicamente coherentes con los valores del dataset y aptas para un informe técnico profesional |
| Sistema de alertas funcional | Las alertas están correctamente categorizadas según los parámetros geotécnicos y las recomendaciones son técnicamente aplicables |
| Evaluación de trituración conceptual | La matriz de criticidad es coherente con las propiedades mecánicas de las litologías y se reconocen explícitamente las limitaciones metodológicas |
| Presentación ejecutiva completa | La presentación de 9 diapositivas integra coherentemente todos los análisis previos en un formato comunicativamente efectivo para la audiencia objetivo |
| Uso efectivo de prompts | Los prompts utilizados son estructurados, específicos y orientados a resultados técnicos concretos |

---

## Resolución de Problemas

### Problema 1: Copilot genera descripciones de facies genéricas o sin valores numéricos del dataset

**Síntomas:** Las descripciones narrativas del Bloque 1 son vagas (ej. "roca de grano medio con algunas estructuras") sin mencionar los valores específicos de GR, RHOB, dureza o abrasividad del dataset. Las descripciones parecen generadas sin leer los datos reales.

**Causa probable:** Los datos tabulares no fueron correctamente incluidos en el prompt, o el formato de pegado desde Excel generó texto mal estructurado que Copilot no pudo interpretar como tabla. También puede ocurrir si el prompt fue demasiado corto y no especificó explícitamente que debía usar los valores del dataset.

**Solución:**
1. Verifique que los datos están efectivamente en el mensaje enviado a Copilot. Revise el historial de la conversación y confirme que la tabla es visible y legible.
2. Si los datos se pegaron con formato incorrecto, regrese a Excel, seleccione la tabla, cópiela, y en el chat de Copilot use la opción "Pegar como texto sin formato" (`Ctrl+Shift+V` en algunos navegadores).
3. Reformule el prompt añadiendo una instrucción explícita: `"Para cada descripción, cita los valores numéricos exactos del dataset (GR_api_prom, RHOB_gcc_prom, Dureza_MPa, Abrasividad_AI) que justifican tu caracterización."` 
4. Alternativamente, cargue directamente el archivo Excel usando el botón de adjunto (📎) de Copilot Chat y referencie la hoja específica en el prompt: `"Analiza la hoja 'Datos_Litologicos' del archivo adjunto..."`.

---

### Problema 2: La presentación PowerPoint queda desorganizada al transferir el guion de Copilot

**Síntomas:** Al copiar el contenido del guion al PowerPoint, el texto aparece en un solo bloque de texto sin estructura de bullets, los caracteres especiales (emojis de alerta 🟢🟡🟠🔴) no se muestran correctamente, o el contenido de una diapositiva excede el espacio disponible del diseño de la plantilla.

**Causa probable:** El guion generado por Copilot está en formato Markdown o texto plano con asteriscos y guiones que no se convierten automáticamente a formato de PowerPoint. Los emojis pueden no ser compatibles con algunas fuentes corporativas. El volumen de texto por diapositiva puede superar lo visualmente recomendable para una presentación ejecutiva.

**Solución:**
1. **Para el formato de bullets:** No copie y pegue el texto directamente. Léalo del guion y reescriba manualmente los bullets en PowerPoint, usando la tecla `Tab` para crear niveles de jerarquía. Esto permite un mayor control del formato.
2. **Para los emojis de alerta:** Reemplace los emojis por formas de PowerPoint con relleno de color (círculos de colores: rojo, naranja, amarillo, verde). Use `Insertar → Formas → Elipse` y aplique el color correspondiente. Esto es más profesional para una presentación corporativa.
3. **Para el exceso de texto:** Solicite a Copilot que reduzca el contenido de la diapositiva problemática con el prompt: `"La diapositiva [X] tiene demasiado texto para una presentación ejecutiva. Reduce el contenido a máximo 5 bullets de no más de 12 palabras cada uno, manteniendo los puntos más importantes."` Aplique la versión reducida en PowerPoint.
4. **Para la estructura general:** Use la vista `Esquema` de PowerPoint (`Vista → Esquema`) para pegar texto estructurado de forma más eficiente y luego cambie a vista Normal para ajustar el formato visual.

---

## Limpieza y Cierre

Al finalizar la práctica, realice las siguientes acciones de cierre:

### Organización de archivos

1. Verifique que todos los archivos de entregables están guardados en su carpeta de trabajo (`C:\Labs\Lab04\` o equivalente):
   - `Lab04_Tabla_Facies.txt`
   - `Lab04_Alertas_Riesgo.txt`
   - `Lab04_Matriz_Trituración.txt`
   - `Lab04_Guion_Presentacion.txt`
   - `Lab04_Presentacion_Comite_[SuNombre].pptx`

2. Suba la carpeta completa a su espacio personal de OneDrive/SharePoint del curso para respaldo y revisión del instructor:
   - Abra OneDrive en el navegador o el cliente de escritorio.
   - Cargue la carpeta `Lab04` completa al directorio `Cursos/Copilot_Geologia/Practicas/Lab04/`.

3. Si el instructor solicitó compartir la presentación para revisión grupal, comparta el archivo `Lab04_Presentacion_Comite_[SuNombre].pptx` con el enlace de OneDrive del curso.

### Cierre de la sesión de Copilot

1. La conversación de Copilot Chat de esta práctica contiene datos del dataset de muestra. No es necesario eliminarla, pero **confirme que no cargó datos reales de su empresa** durante la sesión.
2. Si desea conservar los prompts utilizados como referencia futura, puede copiar los prompts más efectivos de esta práctica a un documento personal de "Biblioteca de Prompts Geológicos".
3. Cierre la pestaña de Copilot Chat al finalizar.

### Reflexión post-práctica (opcional, 5 minutos)

Responda brevemente en su cuaderno o en un documento de texto:
- ¿Qué bloque le resultó más desafiante y por qué?
- ¿En qué situación de su trabajo real podría aplicar el flujo de trabajo de esta práctica?
- ¿Qué limitaciones identificó en el uso de Copilot para análisis geológico-geotécnico?

---

## Resumen

### Lo que aprendió en esta práctica

En esta práctica integradora aplicó un flujo de trabajo geológico completo asistido por Microsoft Copilot Chat, cubriendo cuatro competencias clave:

| Bloque | Competencia aplicada | Producto generado |
|---|---|---|
| **Bloque 1** | Transformación de datos tabulares en narrativas de facies geológicas | Tabla de facies con descripciones narrativas y códigos de color |
| **Bloque 2** | Generación de sistemas de alertas de riesgo geotécnico categorizadas | Sistema de alertas con justificación técnica y recomendaciones de mitigación |
| **Bloque 3** | Evaluación conceptual de criticidad en equipos de trituración | Matriz de criticidad litología-equipo con escenarios de falla y limitaciones metodológicas explícitas |
| **Bloque 4** | Preparación de presentación técnica ejecutiva para comité | Presentación PowerPoint de 9 diapositivas lista para comité técnico |

### Principios clave reforzados

- **Prompts estructurados producen resultados técnicos de mayor calidad:** El uso de roles, contexto, formato de salida y criterios específicos en los prompts mejora significativamente la utilidad de las respuestas de Copilot para aplicaciones geológicas profesionales.
- **Copilot como acelerador, no como sustituto del juicio técnico:** Los resultados de Copilot requieren revisión crítica por parte del geólogo o ingeniero. La validación técnica de la coherencia entre parámetros es responsabilidad del profesional.
- **Las limitaciones metodológicas deben comunicarse explícitamente:** Especialmente en evaluaciones de equipos y simulaciones conceptuales, es fundamental que los resultados de IA incluyan advertencias claras sobre su naturaleza cualitativa y sus limitaciones frente a modelos de simulación física.
- **La integración de análisis en presentaciones ejecutivas es una competencia diferenciadora:** La capacidad de transformar datos técnicos complejos en comunicaciones claras para tomadores de decisión es tan valiosa como el análisis técnico mismo.

### Recursos de referencia adicionales

- [Documentación oficial de Microsoft Copilot Chat para empresas](https://learn.microsoft.com/es-es/copilot/microsoft-365/microsoft-365-copilot-overview)
- [Mejores prácticas para prompts en Copilot (Microsoft)](https://adoption.microsoft.com/es-es/copilot/)
- [Copilot en Excel: guía de inicio](https://support.microsoft.com/es-es/topic/introducción-a-microsoft-copilot-en-excel-018898f0-a795-4ee9-b07f-b419844dcfce)
- [Copilot en PowerPoint: guía de inicio](https://support.microsoft.com/es-es/topic/introducción-a-copilot-en-powerpoint-3571b9f9-c0d1-4f67-8f4b-c9b9a7d8c2a0)
- [Log ASCII Standard (LAS) — Wikipedia EN](https://en.wikipedia.org/wiki/Log_ASCII_Standard)
- [Rock Quality Designation (RQD) — ISRM](https://www.isrm.net/)
- [Cerchar Abrasivity Index — descripción técnica](https://en.wikipedia.org/wiki/Cerchar_abrasivity_index)
- [Introducción a Copilot en Power BI](https://learn.microsoft.com/es-es/power-bi/create-reports/copilot-introduction)

---

*Fin del Lab 04-00-01 — Práctica 4 Integradora*

---
LAB_END---
