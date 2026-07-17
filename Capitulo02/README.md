# Cómo usar Copilot para correlacionar datos de diferentes fuentes y generar resúmenes ejecutivos de cuencas o yacimientos en segundos.

## 1. Metadatos

| Atributo | Valor |
|---|---|
| **Duración estimada** | 100 minutos |
| **Complejidad** | Alta |
| **Nivel Bloom** | Aplicar |
| **Módulo** | 2 — Correlación Multifuente y Síntesis Ejecutiva |
| **ID de práctica** | 02-00-01 |
| **Versión del documento** | 1.0 |

---

## 2. Descripción General

Esta práctica desarrolla la competencia de **correlación multifuente**, uno de los desafíos más frecuentes en el trabajo geológico profesional. Trabajarás con un conjunto de cuatro documentos de muestra que simulan informes técnicos reales de una misma cuenca sedimentaria ficticia (Cuenca Noreste — "CNE-2025"), los cuales contienen información complementaria, inconsistencias deliberadas y vacíos de datos que representan situaciones reales de campo.

Aplicarás el flujo de trabajo de procesamiento inteligente aprendido en la Lección 2.1 — ingesta, extracción, normalización, correlación y validación — utilizando Microsoft Copilot Chat como asistente orquestador. Al finalizar, habrás generado resúmenes ejecutivos calibrados para tres audiencias distintas y habrás verificado su fidelidad contra los documentos fuente.

> ⚠️ **AVISO DE CONFIDENCIALIDAD:** Durante toda esta práctica utiliza **únicamente** los datasets de muestra proporcionados por el instructor. **No cargues datos geológicos reales, confidenciales o propietarios de tu empresa** en Copilot Chat bajo ninguna circunstancia.

---

## 3. Objetivos de Aprendizaje

Al completar esta práctica serás capaz de:

- [ ] **Aplicar** el flujo de trabajo de correlación multifuente (ingesta → extracción → normalización → correlación → validación) en Copilot Chat con documentos geológicos heterogéneos.
- [ ] **Utilizar** prompts estructurados de correlación cruzada para identificar datos convergentes, divergentes y faltantes entre cuatro informes técnicos de una misma cuenca.
- [ ] **Generar** resúmenes ejecutivos de diferente extensión y nivel técnico (comité técnico, dirección ejecutiva, informe regulatorio) mediante prompts de síntesis adaptados a la audiencia.
- [ ] **Evaluar** la calidad y precisión técnica de los resúmenes producidos por Copilot comparándolos sistemáticamente con los documentos fuente originales.
- [ ] **Refinar** iterativamente las respuestas de Copilot mediante prompts de corrección para resolver inconsistencias detectadas en la validación.

---

## 4. Prerrequisitos

### 4.1 Conocimientos Previos

| Área | Nivel requerido |
|---|---|
| Geología de cuencas sedimentarias | Básico-Intermedio (conceptos de cuenca, yacimiento, facies, porosidad, permeabilidad, saturación) |
| Lectura de informes técnicos geológicos en español | Básico |
| Uso de Microsoft Copilot Chat | Completar Práctica 1 del Módulo 1 o experiencia equivalente |
| Microsoft Word y Excel | Básico (apertura, lectura y navegación de documentos) |

### 4.2 Accesos y Recursos Necesarios

| Recurso | Estado requerido antes de iniciar |
|---|---|
| Cuenta corporativa Microsoft 365 activa | ✅ Verificada con TI |
| Acceso a Microsoft Copilot Chat (versión empresarial) | ✅ Licencia confirmada — capacidad de carga de documentos habilitada |
| Carpeta compartida OneDrive/SharePoint del curso | ✅ Acceso concedido (URL proporcionada por instructor) |
| Cuatro documentos de práctica descargados localmente | ✅ Ver Sección 5.3 |
| Microsoft Edge 120+ o Chrome 120+ | ✅ Instalado y actualizado |

> 📌 **Nota del instructor:** Si la velocidad de respuesta de Copilot es lenta (>30 s por respuesta), verificar que la conexión supere los 10 Mbps y que no haya descargas en segundo plano. Tener al menos 2 GB de almacenamiento libre para guardar capturas y archivos de salida.

---

## 5. Entorno de Laboratorio

### 5.1 Hardware Recomendado

| Componente | Mínimo | Recomendado |
|---|---|---|
| Procesador | Intel Core i5 8ª gen / AMD Ryzen 5 | Intel Core i7 10ª gen / AMD Ryzen 7 |
| Memoria RAM | 8 GB | 16 GB |
| Almacenamiento libre | 2 GB | 5 GB |
| Resolución de pantalla | 1366 × 768 px | 1920 × 1080 px |
| Conexión a internet | 10 Mbps | 25 Mbps |

### 5.2 Software Requerido

| Aplicación | Versión mínima | Uso en esta práctica |
|---|---|---|
| Microsoft Copilot Chat (web empresarial) | Vigente (M365 corporativo) | Herramienta principal de correlación y síntesis |
| Microsoft Edge / Chrome | Edge 120+ / Chrome 120+ | Acceso a Copilot Chat |
| Microsoft Word | M365 versión 2301+ | Revisión de informes técnicos de muestra |
| Microsoft Excel | M365 versión 2301+ | Revisión de tablas petrofísicas |
| OneDrive / SharePoint | Vigente (M365 corporativo) | Descarga de documentos de práctica |
| Bloc de Notas / Notepad++ | Cualquier versión reciente | Registro de prompts y observaciones |

### 5.3 Configuración del Entorno — Pasos Previos

Realiza los siguientes pasos **antes de comenzar la Actividad 1**. Tiempo estimado: 10 minutos.

**Paso P-1: Descargar los documentos de práctica**

1. Abre Microsoft Edge o Chrome.
2. Navega a la URL de OneDrive/SharePoint proporcionada por el instructor.
3. Localiza la carpeta: `Curso_Copilot_Geologia / Practica_02 / Documentos_CNE2025/`
4. Descarga los cuatro archivos siguientes a una carpeta local en tu equipo (por ejemplo: `C:\LabCopilot\Practica02\`):

```
CNE2025_Informe_Exploracion_Sismica.docx
CNE2025_Reporte_Petrofisica_Pozos.docx
CNE2025_Boletin_Geoquimica.docx
CNE2025_Memoria_Evaluacion_Reservas.docx
```

5. Verifica que los cuatro archivos se abrieron correctamente en Microsoft Word (doble clic sobre cada uno).

**Paso P-2: Preparar tu bloc de notas de sesión**

1. Abre Notepad++ (o Bloc de Notas).
2. Crea un nuevo archivo y guárdalo como: `Lab02_Registro_Prompts.txt`
3. Escribe en la primera línea:

```
=== REGISTRO DE PROMPTS - LAB 02-00-01 ===
Fecha: [YYYY-MM-DD]
Participante: [Tu nombre]
```

4. Mantén este archivo abierto durante toda la práctica para copiar cada prompt que uses.

**Paso P-3: Abrir Microsoft Copilot Chat**

1. En el navegador, abre una nueva pestaña y navega a:

```
https://copilot.microsoft.com
```

2. Inicia sesión con tu cuenta corporativa Microsoft 365.
3. Verifica que aparece la interfaz empresarial (debe mostrar tu nombre corporativo en la esquina superior derecha y el indicador "Protegido por tu organización" o equivalente).
4. Asegúrate de que el modo de conversación está en **"Trabajo"** (Work) y no en modo personal.
5. Inicia una **nueva conversación** haciendo clic en el ícono de "Nueva conversación" (✏️ o equivalente).

> ✅ **Verificación de entorno:** Si puedes ver el botón para adjuntar archivos (📎 o clip) en la barra de entrada de Copilot Chat, tu cuenta tiene habilitada la funcionalidad de carga de documentos. Si no aparece este botón, contacta a TI antes de continuar.

---

## 6. Actividades Paso a Paso

> **Estructura de la práctica:** La práctica se divide en **cuatro actividades progresivas** que siguen el flujo de trabajo de la Lección 2.1. Cada actividad construye sobre la anterior.
>
> | Actividad | Tema | Tiempo estimado |
> |---|---|---|
> | **A1** | Ingesta y extracción estructurada de múltiples fuentes | 20 min |
> | **A2** | Correlación cruzada e identificación de inconsistencias | 25 min |
> | **A3** | Generación de resúmenes ejecutivos para diferentes audiencias | 30 min |
> | **A4** | Validación de fidelidad y refinamiento iterativo | 15 min |
> | **Cierre** | Reflexión y guardado de resultados | 10 min |

---

### Actividad 1: Ingesta y Extracción Estructurada de Múltiples Fuentes

**Objetivo de la actividad:** Cargar los cuatro documentos de la Cuenca CNE-2025 en Copilot Chat y extraer sus entidades geológicas clave en formato estructurado, siguiendo el patrón de prompt "Resume y extrae" de la Lección 2.1.

---

#### Paso 1.1 — Familiarización con los Documentos de Práctica

**Instrucciones:**

1. Antes de usar Copilot, dedica **5 minutos** a revisar brevemente los cuatro documentos en Microsoft Word. Para cada uno, anota en tu `Lab02_Registro_Prompts.txt`:
   - Tipo de información principal que contiene.
   - Pozos o zonas geográficas que menciona.
   - Formaciones geológicas citadas.
   - Parámetros técnicos presentes (porosidad, permeabilidad, saturación, etc.).

2. Completa la siguiente tabla en tu archivo de registro (valores de ejemplo; reemplaza con los reales de los documentos):

```
TABLA DE INVENTARIO INICIAL
------------------------------------------------------------
Documento                          | Tipo         | Pozos | Formaciones | Parámetros
CNE2025_Informe_Exploracion...     | Sísmica      |       |             |
CNE2025_Reporte_Petrofisica...     | Petrofísica  |       |             |
CNE2025_Boletin_Geoquimica...      | Geoquímica   |       |             |
CNE2025_Memoria_Evaluacion...      | Reservas     |       |             |
------------------------------------------------------------
```

**Resultado esperado:** Tabla de inventario completada con al menos 2 ítems por celda. Este paso simula la etapa de "Inventario e ingestión" del flujo de la Lección 2.1.

**Verificación:** Confirma que identificaste al menos una inconsistencia obvia entre documentos durante la lectura (por ejemplo, un pozo mencionado en un documento pero no en otro, o unidades diferentes para el mismo parámetro).

---

#### Paso 1.2 — Carga del Primer Documento y Extracción Inicial

**Instrucciones:**

1. En Copilot Chat, haz clic en el botón de adjuntar archivo (📎).
2. Selecciona el archivo: `CNE2025_Informe_Exploracion_Sismica.docx`
3. Espera a que el archivo se cargue completamente (aparecerá el nombre del archivo sobre el campo de texto).
4. Ingresa el siguiente prompt de extracción estructurada (cópialo exactamente en tu registro de prompts):

```
Actúa como geólogo de exploración con experiencia en análisis de cuencas 
sedimentarias. Acabo de adjuntar el informe de exploración sísmica de la 
Cuenca CNE-2025.

Por favor, extrae y organiza la siguiente información en una tabla con estas 
columnas exactas:
| Campo | Valor | Unidad | Profundidad_MD_m | Formación | Fuente_Párrafo |

Extrae específicamente:
1. Nombres de pozos mencionados
2. Intervalos sísmicos o estratigráficos identificados
3. Formaciones geológicas nombradas
4. Parámetros técnicos cuantificables (espesores, velocidades, profundidades)
5. Coordenadas o referencias espaciales
6. Fechas de adquisición o procesamiento sísmico

Al final de la tabla, agrega una sección "DUDAS Y AMBIGÜEDADES" listando 
cualquier dato incompleto, unidad no especificada o referencia poco clara 
que encontraste en el documento.
```

5. Espera la respuesta completa de Copilot.
6. Copia la tabla generada en tu archivo `Lab02_Registro_Prompts.txt`.

**Resultado esperado:** Una tabla estructurada con al menos 8-12 filas de entidades extraídas del informe sísmico, más una sección de dudas con al menos 2-3 ítems identificados.

**Verificación:** Abre el documento Word original y verifica manualmente que al menos 3 valores en la tabla de Copilot correspondan exactamente a texto del documento fuente. Si Copilot inventó algún dato que no está en el documento, anótalo como "alucinación" en tu registro.

---

#### Paso 1.3 — Carga Progresiva de los Tres Documentos Restantes

**Instrucciones:**

1. Inicia una **nueva conversación** en Copilot Chat (esto es importante para evitar que el contexto anterior interfiera).
2. Esta vez, adjunta los **cuatro documentos simultáneamente** (si tu versión de Copilot lo permite) o uno por uno en el mismo hilo de conversación. Para adjuntar múltiples archivos:
   - Haz clic en 📎 y selecciona `CNE2025_Informe_Exploracion_Sismica.docx`
   - Repite con `CNE2025_Reporte_Petrofisica_Pozos.docx`
   - Repite con `CNE2025_Boletin_Geoquimica.docx`
   - Repite con `CNE2025_Memoria_Evaluacion_Reservas.docx`

3. Una vez cargados todos los documentos, ingresa el siguiente prompt de inventario global:

```
Tengo adjuntos cuatro documentos técnicos de la Cuenca Noreste CNE-2025:
1. Informe de Exploración Sísmica
2. Reporte de Análisis Petrofísico de Pozos
3. Boletín de Caracterización Geoquímica
4. Memoria Técnica de Evaluación de Reservas

Antes de cualquier análisis, genera un INVENTARIO DE CONTENIDOS con la 
siguiente estructura para cada documento:

**Documento:** [nombre]
**Tipo de información:** [categoría]
**Pozos mencionados:** [lista]
**Formaciones geológicas:** [lista]
**Parámetros técnicos principales:** [lista con unidades]
**Período temporal cubierto:** [fechas o rango]
**Escala geográfica:** [local/regional/cuenca]
**Observaciones iniciales:** [gaps o inconsistencias notorias]

Sé conciso pero completo. Si algún campo no está disponible en el documento, 
escribe "No especificado".
```

4. Guarda la respuesta completa en tu registro de prompts.

**Resultado esperado:** Un inventario estructurado con las 8 secciones completadas para cada uno de los cuatro documentos. Copilot debe haber identificado al menos 1-2 observaciones iniciales de gaps o inconsistencias por documento.

**Verificación:** Compara el inventario generado por Copilot con tu tabla manual del Paso 1.1. Identifica si Copilot detectó alguna información que tú pasaste por alto, o viceversa. Anota las diferencias.

---

### Actividad 2: Correlación Cruzada e Identificación de Inconsistencias

**Objetivo de la actividad:** Aplicar prompts de correlación cruzada para relacionar información entre los cuatro documentos, identificar datos convergentes y divergentes, y construir una tabla maestra de parámetros comparativos, siguiendo el patrón de correlación de la Lección 2.1.

---

#### Paso 2.1 — Correlación por Pozos y Formaciones

**Instrucciones:**

1. Continuando en la **misma conversación** del Paso 1.3 (con los cuatro documentos cargados), ingresa el siguiente prompt de correlación por entidades:

```
Ahora realiza una CORRELACIÓN CRUZADA entre los cuatro documentos adjuntos.

Crea una tabla maestra con las siguientes columnas:
| Pozo_ID | Formación | Doc_Sísmica | Doc_Petrofísica | Doc_Geoquímica | Doc_Reservas | Convergencia | Conflicto |

Instrucciones para completar la tabla:
- En las columnas de cada documento, coloca el valor del parámetro más 
  relevante mencionado para ese pozo/formación (o "No mencionado" si aplica).
- En "Convergencia": describe brevemente en qué coinciden los documentos 
  sobre ese pozo/formación.
- En "Conflicto": describe cualquier dato contradictorio o inconsistente 
  entre documentos para ese registro.

Incluye TODOS los pozos y formaciones identificados en el inventario previo.
Si un pozo aparece con nombres ligeramente diferentes entre documentos 
(ej. "CNE-01" vs "Pozo Norte 1"), señálalo como posible alias y aplica 
tu mejor criterio para unificarlos.
```

2. Guarda la tabla generada en tu registro.
3. Ingresa un prompt de seguimiento para profundizar en los conflictos:

```
De los conflictos identificados en la tabla anterior, selecciona los 
3 más significativos desde el punto de vista geológico y para cada uno:

1. Describe el conflicto con precisión técnica (qué dato difiere, entre 
   qué documentos, y cuál es la magnitud de la discrepancia).
2. Propón una hipótesis de por qué existe esa discrepancia (diferencia 
   metodológica, período de tiempo distinto, error de transcripción, etc.).
3. Recomienda qué fuente debe tener precedencia y por qué (considera que 
   los datos de laboratorio tienen mayor precisión que los narrativos, 
   y los datos más recientes prevalecen sobre los históricos).
4. Indica qué información adicional se necesitaría para resolver el conflicto.

Usa el formato: **CONFLICTO #[N]: [Título breve]**
```

**Resultado esperado:** Una tabla maestra de correlación con al menos 6-8 filas (una por combinación pozo-formación), seguida de un análisis detallado de los 3 conflictos más importantes con las 4 secciones solicitadas para cada uno.

**Verificación:** Abre los documentos Word correspondientes y verifica que los conflictos identificados por Copilot sean reales (es decir, que efectivamente los documentos digan cosas diferentes). Si Copilot inventó un conflicto inexistente, anótalo.

---

#### Paso 2.2 — Normalización de Unidades y Parámetros

**Instrucciones:**

1. En la misma conversación, ingresa el siguiente prompt de normalización (basado en el patrón "Normaliza" de la Lección 2.1):

```
Basándote en los cuatro documentos adjuntos, identifica todos los parámetros 
petrofísicos y geológicos que aparecen con unidades distintas entre documentos 
o con formatos inconsistentes.

Genera una TABLA DE NORMALIZACIÓN con estas columnas:
| Parámetro | Unidad_Doc1 | Unidad_Doc2 | Unidad_Doc3 | Unidad_Doc4 | Unidad_Normalizada_SI | Factor_Conversión | Observación |

Parámetros a buscar (incluye todos los que encuentres):
- Profundidades (MD, TVD)
- Porosidad
- Permeabilidad  
- Saturación de agua/hidrocarburo
- Presión de formación
- Temperatura
- Densidad de roca/fluido
- Espesores de formación
- Coordenadas geográficas

Adicionalmente, lista los sinónimos terminológicos encontrados entre documentos 
(ej. "lutita" vs "shale" vs "pelita") en una tabla separada con columnas:
| Término_Documento | Término_Normalizado | Equivalencia_Confirmada |
```

2. Guarda la respuesta completa.

**Resultado esperado:** Una tabla de normalización con al menos 5-6 parámetros identificados y su conversión a unidades SI, más una tabla de sinónimos con al menos 4-5 equivalencias terminológicas.

**Verificación:** Selecciona un parámetro de la tabla (por ejemplo, permeabilidad en mD vs. m²) y verifica manualmente que el factor de conversión proporcionado por Copilot sea correcto usando una fuente de referencia estándar.

---

#### Paso 2.3 — Construcción del Repositorio Integrado

**Instrucciones:**

1. Ingresa el siguiente prompt de síntesis de correlación:

```
Con base en el inventario, la tabla de correlación cruzada y la normalización 
de unidades que hemos desarrollado, genera un REPORTE DE CORRELACIÓN INTEGRADO 
para la Cuenca CNE-2025 con las siguientes secciones:

**1. COBERTURA DE DATOS** (1 párrafo)
Describe qué pozos y formaciones tienen cobertura en múltiples fuentes vs. 
los que solo aparecen en una fuente. Incluye un porcentaje estimado de 
cobertura multifuente.

**2. HALLAZGOS CONVERGENTES** (lista con viñetas)
Los 5 principales hallazgos geológicos en los que 3 o más documentos 
están de acuerdo. Cita la fuente para cada hallazgo.

**3. INCONSISTENCIAS CRÍTICAS** (lista numerada)
Las 3 inconsistencias que más impactan la evaluación del yacimiento, 
con la magnitud de la discrepancia y la fuente de mayor confiabilidad.

**4. GAPS DE INFORMACIÓN** (tabla)
| Aspecto_Faltante | Documentos_Afectados | Impacto_en_Evaluación | Prioridad_de_Resolución |

**5. MÉTRICAS DE CALIDAD DEL REPOSITORIO**
- Porcentaje de pozos con cobertura en ≥3 fuentes: [X]%
- Número de parámetros normalizados exitosamente: [N]
- Número de conflictos pendientes de resolución humana: [N]
- Confiabilidad general del repositorio: [Alta/Media/Baja] con justificación

Etiqueta el nivel de confianza de cada hallazgo como [ALTA], [MEDIA] o [BAJA].
```

2. Guarda el reporte completo en tu registro de prompts.

**Resultado esperado:** Un reporte de correlación integrado con las 5 secciones completas, incluyendo métricas de calidad. La sección de hallazgos convergentes debe tener al menos 5 viñetas y la tabla de gaps al menos 4 filas.

**Verificación:** Revisa que las fuentes citadas en la sección de hallazgos convergentes correspondan efectivamente a los documentos adjuntos y no sean referencias inventadas.

---

### Actividad 3: Generación de Resúmenes Ejecutivos para Diferentes Audiencias

**Objetivo de la actividad:** Generar tres versiones de resumen ejecutivo de la Cuenca CNE-2025 calibradas para audiencias distintas (comité técnico, dirección ejecutiva, informe regulatorio), aplicando prompts de síntesis adaptativa con control explícito de extensión, vocabulario y estructura.

> 💡 **Concepto clave (Lección 2.1):** Copilot puede adaptar el nivel técnico, la extensión y el formato de un resumen según las instrucciones del prompt. La clave está en especificar explícitamente la audiencia, el propósito, la extensión máxima y el formato de salida.

---

#### Paso 3.1 — Resumen para Comité Técnico Geológico

**Instrucciones:**

1. En la misma conversación (con los documentos y el contexto de correlación acumulado), ingresa:

```
Genera un RESUMEN TÉCNICO GEOLÓGICO de la Cuenca CNE-2025 dirigido a un 
Comité Técnico compuesto por geólogos senior e ingenieros de yacimientos.

ESPECIFICACIONES:
- Extensión: 600-800 palabras
- Formato: Secciones con títulos en negrita
- Nivel técnico: ALTO — usa terminología técnica específica sin definirla
- Incluye valores numéricos con unidades precisas
- Cita explícitamente las fuentes (Informe Sísmico, Reporte Petrofísico, 
  Boletín Geoquímico, Memoria de Reservas) para los datos más importantes

SECCIONES OBLIGATORIAS:
1. Contexto Geológico y Marco Estratigráfico
2. Caracterización Petrofísica del Yacimiento Principal
3. Evaluación Geoquímica y Sistema Petrolífero
4. Estimación de Reservas y Parámetros de Incertidumbre
5. Inconsistencias Identificadas y Recomendaciones de Estudio

Al final, incluye una tabla resumen:
| Parámetro | Valor | Unidad | Fuente | Confiabilidad |

Utiliza únicamente información de los cuatro documentos adjuntos. 
Si un dato no está disponible, escribe "No determinado" — NO inventes valores.
```

2. Guarda el resumen generado con la etiqueta `[RESUMEN_TECNICO_v1]` en tu registro.
3. Toma una captura de pantalla de la respuesta completa.

**Resultado esperado:** Un resumen técnico de 600-800 palabras con las 5 secciones solicitadas, valores numéricos con unidades, citas de fuente y una tabla resumen con al menos 8 parámetros.

**Verificación:** Verifica que el resumen menciona al menos 3 formaciones geológicas específicas y al menos 2 pozos de la cuenca por nombre. Confirma que no hay valores numéricos que no aparezcan en ninguno de los cuatro documentos fuente.

---

#### Paso 3.2 — Resumen para Dirección Ejecutiva

**Instrucciones:**

1. Ingresa el siguiente prompt de adaptación para audiencia no técnica:

```
Ahora genera una versión del resumen de la Cuenca CNE-2025 para la 
DIRECCIÓN EJECUTIVA de la empresa (CEO, CFO y VP de Exploración), 
quienes tienen formación de negocios pero conocimiento geológico limitado.

ESPECIFICACIONES:
- Extensión: 300-400 palabras MÁXIMO
- Formato: Párrafos cortos + bullets de puntos clave
- Nivel técnico: BAJO — evita jerga técnica; si es indispensable, 
  define el término entre paréntesis en la primera mención
- Enfoque: Oportunidad de negocio, riesgos clave y próximos pasos
- NO incluyas tablas de parámetros técnicos
- Usa lenguaje de negocios: "potencial de reservas", "riesgo de inversión", 
  "recomendación de acción"

ESTRUCTURA:
**Resumen en una oración** (máximo 40 palabras)
**Hallazgos Principales** (3 bullets)
**Riesgos e Incertidumbres** (2-3 bullets)
**Próximos Pasos Recomendados** (2-3 bullets con responsable y plazo sugerido)

Basa el contenido EXCLUSIVAMENTE en los documentos adjuntos. 
No añadas información externa ni proyecciones no respaldadas.
```

2. Guarda con etiqueta `[RESUMEN_EJECUTIVO_v1]`.
3. Compara visualmente con el resumen técnico del Paso 3.1 — anota en tu registro al menos 3 diferencias de estilo o contenido entre ambas versiones.

**Resultado esperado:** Un resumen ejecutivo de 300-400 palabras con la estructura de 4 secciones, sin terminología técnica sin definir, con enfoque en oportunidad/riesgo/acción.

**Verificación:** Pide a un compañero que no tenga formación geológica que lea el resumen ejecutivo y confirme que lo entiende sin necesidad de explicaciones adicionales. Si hay términos confusos, anótalos para el Paso 4.2.

---

#### Paso 3.3 — Resumen para Informe Regulatorio

**Instrucciones:**

1. Ingresa el siguiente prompt para formato regulatorio:

```
Genera una SÍNTESIS TÉCNICA para informe regulatorio de la Cuenca CNE-2025, 
siguiendo los estándares típicos de reportes ante autoridades de hidrocarburos.

ESPECIFICACIONES:
- Extensión: 500-600 palabras
- Formato: Numeración jerárquica (1., 1.1, 1.2, 2., etc.)
- Tono: Formal, objetivo, en tercera persona
- Incluye unidades del Sistema Internacional (SI) en todos los valores
- Agrega una sección de "Limitaciones y Datos Faltantes" obligatoria
- Incluye referencias a los documentos fuente en formato: 
  [Tipo_Documento, Año_si_disponible]

SECCIONES REQUERIDAS:
1. Identificación del Área de Estudio
   1.1 Ubicación y Extensión
   1.2 Marco Geológico Regional
2. Metodología de Evaluación
   2.1 Fuentes de Información Utilizadas
   2.2 Período de los Datos
3. Resultados Técnicos
   3.1 Características del Yacimiento
   3.2 Parámetros Petrofísicos
   3.3 Evaluación Geoquímica
4. Estimación de Recursos
5. Limitaciones y Datos Faltantes
6. Conclusiones

Mantén un tono neutral y objetivo. Señala explícitamente cuando un dato 
proviene de una sola fuente y no ha sido verificado por fuentes independientes.
```

2. Guarda con etiqueta `[RESUMEN_REGULATORIO_v1]`.

**Resultado esperado:** Una síntesis de 500-600 palabras con numeración jerárquica completa, tono formal en tercera persona, unidades SI y sección de limitaciones con al menos 3 ítems.

**Verificación:** Confirma que la sección 2.1 lista los cuatro documentos de práctica como fuentes, y que la sección 5 menciona al menos 2 de los gaps identificados en la Actividad 2.

---

#### Paso 3.4 — Comparación de las Tres Versiones

**Instrucciones:**

1. Ingresa el siguiente prompt de metaanálisis:

```
Acabas de generar tres versiones de resumen de la Cuenca CNE-2025 para 
diferentes audiencias. Sin regenerar los resúmenes, realiza un análisis 
comparativo de las tres versiones:

Crea una tabla con estas columnas:
| Criterio | Resumen_Técnico | Resumen_Ejecutivo | Resumen_Regulatorio |

Evalúa los siguientes criterios (califica como Alto/Medio/Bajo o con valor):
1. Densidad de terminología técnica
2. Cantidad de valores numéricos incluidos
3. Orientación a decisión de negocio
4. Trazabilidad a documentos fuente
5. Adecuación al público objetivo (del 1 al 5)
6. Información sobre riesgos e incertidumbres
7. Extensión (palabras aproximadas)

Concluye con 2-3 observaciones sobre cómo la misma información geológica 
puede comunicarse de manera radicalmente diferente según la audiencia.
```

2. Guarda la tabla comparativa en tu registro.

**Resultado esperado:** Una tabla comparativa con 7 criterios evaluados para las 3 versiones, más 2-3 observaciones de cierre sobre comunicación adaptativa.

---

### Actividad 4: Validación de Fidelidad y Refinamiento Iterativo

**Objetivo de la actividad:** Evaluar sistemáticamente la precisión técnica de los resúmenes generados por Copilot comparándolos con los documentos fuente, y aplicar prompts de refinamiento para corregir errores o mejorar la calidad.

---

#### Paso 4.1 — Protocolo de Validación de Fidelidad

**Instrucciones:**

1. Abre los cuatro documentos Word de práctica en ventanas separadas.
2. Selecciona el **Resumen Técnico** (`[RESUMEN_TECNICO_v1]`) y realiza la siguiente verificación manual. Completa la tabla en tu registro:

```
PROTOCOLO DE VALIDACIÓN DE FIDELIDAD — RESUMEN TÉCNICO
=======================================================
Para cada afirmación verificada, clasifica como:
[V] = Verificado y correcto
[P] = Parcialmente correcto (valor aproximado o incompleto)
[E] = Error (dato incorrecto o no encontrado en fuentes)
[I] = Información inventada (no existe en ningún documento fuente)

AFIRMACIONES A VERIFICAR (selecciona 10 del resumen):
1. [Afirmación extraída del resumen] → [V/P/E/I] → [Documento fuente]
2. ...
...
10. ...

MÉTRICAS:
- Afirmaciones Verificadas [V]: ___ / 10 = ____%
- Afirmaciones Parciales [P]: ___ / 10 = ____%
- Errores [E]: ___ / 10 = ____%
- Inventadas [I]: ___ / 10 = ____%
- ÍNDICE DE FIDELIDAD GLOBAL: ____%
```

3. Anota en tu registro cuáles fueron los errores o invenciones más graves.

**Resultado esperado:** Un protocolo de validación completado con 10 afirmaciones evaluadas y un índice de fidelidad calculado. Se espera un índice de fidelidad entre 70-90% en condiciones normales.

**Verificación:** Si el índice de fidelidad es inferior al 60%, revisa si los documentos se cargaron correctamente en Copilot y considera reiniciar la conversación con una carga más explícita de los archivos.

---

#### Paso 4.2 — Refinamiento mediante Prompts de Corrección

**Instrucciones:**

1. Basándote en los errores identificados en el Paso 4.1, ingresa el siguiente prompt de refinamiento (adapta los errores específicos que encontraste):

```
He revisado el resumen técnico que generaste contra los documentos fuente 
y encontré las siguientes imprecisiones que necesito corregir:

[LISTA TUS ERRORES ESPECÍFICOS AQUÍ — ejemplo:]
- Error 1: Indicaste que la porosidad del Yacimiento X es [valor A], pero 
  el Reporte Petrofísico indica [valor B] en la página [N].
- Error 2: Mencionaste la Formación [Y] como el reservorio principal, pero 
  la Memoria de Reservas indica que es la Formación [Z].
- Error 3: El valor de permeabilidad está en mD pero debería estar en m² 
  según la normalización SI acordada.

Por favor:
1. Corrige ÚNICAMENTE los errores listados en el resumen técnico.
2. Mantén el resto del contenido sin cambios.
3. Marca cada corrección con [CORREGIDO] al final de la oración modificada.
4. Si alguna corrección te genera dudas sobre qué valor es el correcto 
   según los documentos, indícalo con [REQUIERE_REVISIÓN_HUMANA].
```

2. Guarda el resumen corregido con etiqueta `[RESUMEN_TECNICO_v2]`.
3. Vuelve a verificar las afirmaciones corregidas contra los documentos fuente.

**Resultado esperado:** Una versión corregida del resumen técnico con marcas `[CORREGIDO]` en los puntos modificados. El índice de fidelidad de la versión v2 debe ser superior al de v1.

**Verificación:** Compara `[RESUMEN_TECNICO_v1]` y `[RESUMEN_TECNICO_v2]` lado a lado en tu registro. Confirma que las correcciones solicitadas fueron aplicadas y que no se introdujeron nuevos errores en el proceso de refinamiento.

---

#### Paso 4.3 — Generación del Log de Trazabilidad

**Instrucciones:**

1. Ingresa el siguiente prompt para generar documentación de trazabilidad (concepto clave de la Lección 2.1):

```
Para completar el proceso de correlación y síntesis de la Cuenca CNE-2025, 
genera un LOG DE TRAZABILIDAD del trabajo realizado en esta sesión.

El log debe tener el siguiente formato:

**LOG DE TRANSFORMACIONES Y DECISIONES — CUENCA CNE-2025**
Fecha: [fecha actual]

| # | Operación | Documentos_Involucrados | Regla_Aplicada | Resultado | Confianza | Requiere_Revisión_Humana |
|---|---|---|---|---|---|---|

Incluye una fila por cada decisión significativa tomada durante el análisis:
- Cada correlación entre documentos
- Cada normalización de unidades
- Cada resolución de conflicto entre fuentes
- Cada dato marcado como "No determinado"
- Cada alias de pozo o formación unificado

Al final, agrega:
**RESUMEN DE CALIDAD DEL PROCESO:**
- Total de operaciones registradas: N
- Operaciones de alta confianza (sin ambigüedad): N (X%)
- Operaciones que requieren revisión humana: N (X%)
- Recomendaciones para próxima iteración: [lista]
```

2. Guarda el log completo en tu registro de prompts.

**Resultado esperado:** Un log de trazabilidad con al menos 10 filas de operaciones documentadas y un resumen de calidad con métricas calculadas.

**Verificación:** El log debe incluir al menos 1 operación de cada uno de los 5 tipos listados (correlación, normalización, resolución de conflicto, dato faltante, alias unificado).

---

### Cierre: Reflexión y Guardado de Resultados

**Instrucciones:**

1. Guarda todos los outputs generados durante la práctica:
   - Exporta o copia los tres resúmenes ejecutivos (v1 y v2 del técnico) en un documento Word nuevo: `Lab02_Resultados_[TuNombre].docx`
   - Guarda tu archivo `Lab02_Registro_Prompts.txt` con todos los prompts utilizados.

2. Sube ambos archivos a la carpeta de entrega en OneDrive/SharePoint:
   ```
   Curso_Copilot_Geologia / Practica_02 / Entregas / [TuNombre]/
   ```

3. Responde brevemente en tu registro las siguientes preguntas de reflexión (5-7 líneas cada una):
   - ¿En qué tipo de conflicto entre documentos fue más útil Copilot? ¿En cuál fue menos confiable?
   - ¿Qué diferencia observaste entre el resumen técnico y el ejecutivo en términos de utilidad práctica?
   - ¿Qué estrategia de prompt funcionó mejor para obtener respuestas más precisas y menos alucinaciones?

---

## 7. Validación y Pruebas Finales

Al completar las cuatro actividades, verifica que puedes responder afirmativamente a cada uno de los siguientes criterios:

| # | Criterio de validación | ¿Cumplido? |
|---|---|---|
| V-01 | Cargué los cuatro documentos de práctica en Copilot Chat y obtuve un inventario estructurado de cada uno. | ☐ |
| V-02 | Generé una tabla de correlación cruzada con al menos 6 filas que relaciona pozos y formaciones entre múltiples documentos. | ☐ |
| V-03 | Identifiqué y documenté al menos 3 inconsistencias entre documentos con propuesta de resolución. | ☐ |
| V-04 | Produje una tabla de normalización de unidades con al menos 5 parámetros y sus factores de conversión. | ☐ |
| V-05 | Generé tres versiones de resumen ejecutivo diferenciadas por audiencia (técnico, ejecutivo, regulatorio). | ☐ |
| V-06 | Apliqué el protocolo de validación de fidelidad y calculé un índice de fidelidad para el resumen técnico. | ☐ |
| V-07 | Refiné el resumen técnico mediante prompts de corrección y obtuve una versión v2 con mayor fidelidad. | ☐ |
| V-08 | Generé un log de trazabilidad con al menos 10 operaciones documentadas. | ☐ |
| V-09 | Guardé y subí todos los archivos de entrega a la carpeta correspondiente en OneDrive/SharePoint. | ☐ |

> **Criterio de aprobación:** Mínimo 7 de 9 criterios cumplidos (78%). Si no alcanzas este umbral, revisa las actividades correspondientes a los criterios no cumplidos antes de avanzar a la Práctica 3.

---

## 8. Resolución de Problemas

### Problema 1: Copilot no reconoce el contenido de los documentos adjuntos y responde con información genérica

**Síntoma:** Copilot genera respuestas sobre geología genérica en lugar de referirse a los pozos, formaciones y parámetros específicos de los documentos de práctica CNE-2025. Las respuestas no mencionan ningún nombre de pozo específico ni valor numérico del documento.

**Causa probable:** El archivo no se cargó correctamente (tamaño excesivo, formato no compatible, o error silencioso durante la carga), o el prompt no hace referencia explícita al documento adjunto, por lo que Copilot utiliza su conocimiento general en lugar del contexto documental.

**Solución:**
1. Verifica que el archivo se cargó correctamente: debe aparecer el nombre del archivo como un chip/etiqueta sobre el campo de texto antes de enviar el prompt.
2. Si el archivo no aparece, intenta cargarlo nuevamente. Si el problema persiste, verifica que el archivo `.docx` no supere los 20 MB y que no esté protegido con contraseña.
3. Modifica tu prompt para hacer referencia explícita al documento: en lugar de "analiza el informe", escribe **"Analiza el documento adjunto titulado 'CNE2025_Informe_Exploracion_Sismica.docx' que acabo de cargar"**.
4. Si el problema continúa, copia y pega directamente el texto de las primeras 2-3 páginas del documento en el campo de texto de Copilot como contexto explícito, precedido por: `"El siguiente texto proviene del Informe de Exploración Sísmica CNE-2025: [TEXTO PEGADO]"`.
5. Como alternativa, intenta en una nueva conversación con un solo documento a la vez en lugar de los cuatro simultáneamente.

---

### Problema 2: Las respuestas de Copilot varían significativamente entre intentos con el mismo prompt, generando inconsistencias entre actividades

**Síntoma:** Al repetir un prompt idéntico (por ejemplo, para regenerar la tabla de correlación cruzada), Copilot produce una tabla con diferente número de filas, valores distintos o una estructura de columnas diferente a la solicitada. Los resúmenes ejecutivos cambian de extensión o incluyen/omiten secciones entre regeneraciones.

**Causa probable:** Esta variabilidad es inherente a los modelos de lenguaje generativo (temperatura estocástica del modelo). Se agrava cuando los prompts son ambiguos, no incluyen ejemplos de formato esperado, o cuando la conversación acumula mucho contexto previo que "contamina" las instrucciones.

**Solución:**
1. **Aumenta la especificidad del prompt:** En lugar de "genera una tabla comparativa", especifica exactamente el número de columnas, sus nombres, el número esperado de filas y un ejemplo de fila. Cuanto más concreto sea el prompt, menor será la variabilidad.
2. **Incluye un ejemplo en el prompt (few-shot):** Agrega al final del prompt: `"Ejemplo de formato esperado para la primera fila: | CNE-01 | Formación Roja | Espesor: 45 m | Porosidad: 18% | ..."`.
3. **Usa instrucciones de restricción:** Añade frases como: `"No agregues columnas adicionales a las especificadas"`, `"Mantén exactamente este formato de tabla"`, `"No incluyas información que no esté en los documentos adjuntos"`.
4. **Inicia una nueva conversación limpia** si el hilo actual tiene más de 15-20 intercambios: el contexto acumulado puede degradar la coherencia de las respuestas. Vuelve a cargar los documentos y usa el Reporte de Correlación Integrado del Paso 2.3 como contexto de arranque en la nueva conversación.
5. **Documenta la variabilidad:** Anota en tu registro cuándo observaste variabilidad significativa — esto es material de aprendizaje valioso sobre las limitaciones de los LLMs en contextos técnicos.

---

## 9. Limpieza del Entorno

Al finalizar la práctica, realiza los siguientes pasos de limpieza:

1. **Cerrar la conversación de Copilot:** En la interfaz de Copilot Chat, cierra la conversación activa. Si tu organización tiene políticas de retención de datos, verifica con TI si las conversaciones se eliminan automáticamente o si debes hacerlo manualmente.

2. **Verificar la subida de archivos de entrega:**
   ```
   Confirmar en OneDrive/SharePoint:
   ✅ Lab02_Resultados_[TuNombre].docx — subido
   ✅ Lab02_Registro_Prompts.txt — subido
   ```

3. **Cerrar documentos Word:** Cierra los cuatro documentos de práctica en Word. No es necesario guardar cambios en los documentos originales.

4. **Limpiar archivos temporales locales (opcional):** Si deseas liberar espacio, puedes eliminar los archivos descargados de la carpeta local `C:\LabCopilot\Practica02\` una vez confirmada la subida a OneDrive.

5. **Cerrar sesión de Copilot (recomendado en equipos compartidos):** Si usas un equipo compartido, cierra sesión en Copilot Chat y en Microsoft 365 para proteger la confidencialidad de la sesión.

> 🔒 **Recordatorio de seguridad:** Verifica que no hayas guardado datos reales o confidenciales de tu empresa en ninguno de los archivos generados durante la práctica. Los archivos de entrega deben contener únicamente información de los datasets de muestra CNE-2025.

---

## 10. Resumen

### Lo que aprendiste en esta práctica

En esta práctica aplicaste el flujo de trabajo completo de **correlación multifuente** con Microsoft Copilot Chat, cubriendo las cinco etapas del ciclo de procesamiento inteligente presentado en la Lección 2.1:

| Etapa | Actividad realizada | Herramienta de Copilot utilizada |
|---|---|---|
| **Inventario e ingestión** | Carga de 4 documentos y generación de inventario estructurado | Prompts de "Resume y extrae" |
| **Extracción y estructuración** | Tablas de entidades geológicas por documento | Prompts de extracción con columnas definidas |
| **Normalización** | Unificación de unidades SI y diccionario de sinónimos | Prompts de "Normaliza" |
| **Correlación multimodal** | Tabla maestra cruzada con convergencias y conflictos | Prompts de "Correlaciona" con reglas de precedencia |
| **Validación y trazabilidad** | Protocolo de fidelidad, refinamiento v2 y log de transformaciones | Prompts de "Valida" y refinamiento iterativo |

Adicionalmente, desarrollaste la competencia de **síntesis adaptativa**, generando el mismo contenido geológico en tres registros comunicativos distintos (técnico, ejecutivo, regulatorio) mediante el control explícito de audiencia, extensión y formato en los prompts.

### Conceptos Clave Reforzados

- **Trazabilidad:** Toda transformación realizada por Copilot debe quedar documentada en un log con fuente, regla aplicada y nivel de confianza.
- **Validación de fidelidad:** Las respuestas de Copilot siempre deben verificarse contra los documentos fuente; el índice de fidelidad es una métrica práctica para medir la calidad del output.
- **Prompts deterministas:** La especificidad del prompt (columnas exactas, ejemplos de formato, restricciones explícitas) reduce significativamente la variabilidad de las respuestas.
- **Síntesis adaptativa:** La misma información geológica puede y debe comunicarse de manera radicalmente diferente según la audiencia y el propósito del documento.

### Recursos Adicionales

| Recurso | URL / Referencia |
|---|---|
| Microsoft Learn — Copilot para M365 | https://learn.microsoft.com/microsoft-365-copilot/overview-copilot |
| EPSG.io — Catálogo de CRS | https://epsg.io/ |
| USGS Geolex — Nomenclatura estratigráfica | https://ngmdb.usgs.gov/Geolex/ |
| CWLS LAS — Estándar de registros de pozo | https://www.cwls.org/las/ |
| GeoPandas — Documentación oficial | https://geopandas.org/en/stable/ |
| OGC API Features — Estándar geoespacial | https://ogcapi.ogc.org/features/ |

### Próximos Pasos

Con las competencias desarrolladas en esta práctica, estás preparado para:

- **Práctica 3:** Crear agentes de IA especializados en estándares geológicos que validen automáticamente informes técnicos contra normativas sectoriales específicas.
- **Aplicación inmediata:** Comenzar a construir tu propio diccionario corporativo de sinónimos litológicos y catálogo de formaciones para usar como contexto en futuros prompts de correlación.
- **Mejora continua:** Revisar y refinar tus plantillas de prompts de extracción, normalización y correlación con base en los resultados y variabilidades observadas en esta sesión.

---

> **Nota pedagógica para el instructor:** Si el tiempo disponible es menor a 100 minutos, las Actividades 1 y 2 son obligatorias (competencia core de correlación). La Actividad 3 puede reducirse a solo dos versiones de resumen (técnico + ejecutivo). La Actividad 4 puede asignarse como tarea asincrónica con entrega previa a la siguiente sesión.

---
