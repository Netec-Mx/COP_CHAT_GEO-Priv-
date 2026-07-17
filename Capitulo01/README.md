# Uso de Copilot para identificar patrones litológicos, quiebres de formación y anomalías en datos de perforación

## Metadatos

| Campo             | Detalle                                                                 |
|-------------------|-------------------------------------------------------------------------|
| **Duración**      | 70 minutos                                                              |
| **Complejidad**   | Media                                                                   |
| **Nivel Bloom**   | Aplicar (Apply)                                                         |
| **Módulo**        | Módulo 1 — Análisis de Registros de Perforación con IA                  |
| **Práctica**      | 01 de 03                                                                |

---

## Visión General

En esta práctica aplicarás Microsoft Copilot Chat como asistente de análisis geológico para examinar un registro de perforación simulado. Utilizarás prompts estructurados y progresivamente refinados para identificar patrones litológicos recurrentes, detectar quiebres de formación (cambios abruptos entre intervalos de profundidad) y señalar anomalías en propiedades petrofísicas como densidad, porosidad y gamma ray. Al finalizar, Copilot generará un resumen interpretativo del perfil litológico analizado que podrás documentar y comparar con los resultados de tus compañeros.

> ⚠️ **Aviso de Confidencialidad:** Durante toda la práctica, utiliza **únicamente** los datasets de muestra proporcionados por el instructor. **No cargues datos geológicos reales, confidenciales o propietarios de tu organización** en Copilot Chat bajo ninguna circunstancia.

---

## Objetivos de Aprendizaje

Al completar esta práctica, serás capaz de:

- [ ] Cargar contexto tabular de un registro de perforación en Copilot Chat y obtener un resumen estructurado de rangos, nulos y anomalías por curva.
- [ ] Formular prompts con reglas explícitas para que Copilot identifique patrones litológicos recurrentes y quiebres de formación en secuencias de profundidad.
- [ ] Refinar iterativamente prompts para mejorar la precisión de la detección de anomalías (valores atípicos en GR, RHOB, NPHI y RT).
- [ ] Comparar la efectividad de al menos dos estructuras de prompt distintas para la misma tarea de análisis litológico.
- [ ] Solicitar a Copilot un resumen interpretativo ejecutivo del perfil litológico analizado.

---

## Prerrequisitos

### Conocimientos

| Área | Nivel requerido |
|------|----------------|
| Terminología litológica básica (sedimentaria, ígnea, metamórfica) | Básico |
| Concepto de formación geológica y secuencia estratigráfica | Básico |
| Lectura de tablas de datos en Excel o formato CSV | Básico |
| Introducción teórica del Módulo 1 (Lección 1.1) | Completada |

### Acceso y Cuentas

| Recurso | Estado requerido |
|---------|-----------------|
| Cuenta corporativa Microsoft 365 activa | ✅ Verificado por TI |
| Acceso habilitado a Microsoft 365 Copilot Chat (versión empresarial) | ✅ Confirmado |
| Acceso a la carpeta compartida en OneDrive/SharePoint del curso | ✅ Disponible |
| Microsoft Excel 365 (versión 2301 o superior) instalado | ✅ Instalado |
| Microsoft Edge 120+ o Google Chrome 120+ | ✅ Actualizado |

---

## Entorno de Laboratorio

### Hardware Mínimo Recomendado

| Componente | Mínimo | Recomendado |
|------------|--------|-------------|
| Procesador | Intel Core i5 8ª gen / AMD Ryzen 5 | Intel Core i7 / AMD Ryzen 7 |
| Memoria RAM | 8 GB | 16 GB |
| Almacenamiento libre | 500 MB | 2 GB |
| Resolución de pantalla | 1366×768 px | 1920×1080 px |
| Conexión a internet | 10 Mbps estable | 25 Mbps o superior |

### Software Requerido

| Software | Versión | Uso en esta práctica |
|----------|---------|----------------------|
| Microsoft 365 Copilot Chat | Versión empresarial vigente | Análisis principal |
| Microsoft Excel 365 | 2301 o superior | Visualización del dataset |
| Microsoft Edge / Chrome | 120 o superior | Acceso a Copilot Chat |
| OneDrive / SharePoint | Empresarial vigente | Descarga de archivos de práctica |
| Bloc de Notas / Notepad++ | Cualquier versión reciente | Registro de prompts |

### Configuración Inicial del Entorno

Realiza los siguientes pasos **antes** de comenzar las actividades:

```
1. Abre tu navegador (Edge o Chrome) e inicia sesión en:
   https://m365.cloud.microsoft/chat

2. Verifica que aparece la interfaz de Copilot Chat empresarial
   (debe mostrar el logo de Microsoft 365 y tu cuenta corporativa).

3. Abre la carpeta compartida del curso en OneDrive:
   [URL proporcionada por el instructor]
   Navega a: Módulo_01 > Práctica_01 > Archivos

4. Descarga los siguientes archivos a tu carpeta local de trabajo
   (ej. C:\LabGeo\Practica01\):
   - POZO_FICTICIO_ALFA_Registros.xlsx
   - POZO_FICTICIO_ALFA_Registros.csv
   - Plantilla_Registro_Prompts_P01.docx

5. Abre POZO_FICTICIO_ALFA_Registros.xlsx en Excel para
   familiarizarte con la estructura del dataset.

6. Abre Plantilla_Registro_Prompts_P01.docx en Word para
   documentar tus prompts y resultados durante la práctica.
```

### Descripción del Dataset de Práctica

El archivo **POZO_FICTICIO_ALFA_Registros.csv** contiene un registro de perforación simulado del pozo ficticio "Alfa-1" con las siguientes columnas:

| Columna | Unidades | Descripción |
|---------|----------|-------------|
| `DEPTH_MD` | metros (m) | Profundidad medida a lo largo del pozo |
| `GR` | API | Gamma Ray — indicador de arcillosidad |
| `RHOB` | g/cc | Densidad de la formación |
| `NPHI` | v/v | Porosidad neutrónica |
| `RT` | ohm·m | Resistividad verdadera |
| `LITHO_DESC` | texto | Descripción litológica del perforador |
| `COLOR` | texto | Color observado en recortes |
| `HARDNESS` | 1–5 | Dureza relativa estimada (1=muy blando, 5=muy duro) |
| `NOTES` | texto | Notas adicionales del perforador |

**Rango de profundidades:** 1,450 m – 1,650 m (intervalo de 0.5 m)
**Número de filas:** ~400 registros
**Formaciones presentes (ficticias):** Fm. Arenisca Palmira, Fm. Lutita Oscura, Fm. Caliza Compacta

> 📌 **Nota pedagógica:** Copilot Chat puede generar respuestas ligeramente diferentes en cada sesión para el mismo prompt. Esto es normal e inherente a los modelos de lenguaje. Si tu resultado difiere del ejemplo mostrado, evalúa si la respuesta es técnicamente coherente, no si es idéntica.

---

## Actividades Paso a Paso

---

### Actividad 1: Familiarización con el Dataset y Carga de Contexto en Copilot (15 minutos)

**Objetivo:** Explorar el dataset en Excel, preparar el contexto para Copilot y obtener un resumen estructurado de las curvas disponibles.

#### Instrucciones

**1.1 — Exploración del dataset en Excel**

1. Abre **POZO_FICTICIO_ALFA_Registros.xlsx** en Excel.
2. Examina las primeras 20 filas y las últimas 20 filas del dataset.
3. Identifica visualmente:
   - ¿Existen celdas vacías o con valores "#N/A"?
   - ¿Hay valores de GR extremadamente altos (>200 API) o bajos (<0 API)?
   - ¿Notas cambios bruscos en la columna `LITHO_DESC`?
4. Anota tus observaciones preliminares en **Plantilla_Registro_Prompts_P01.docx**, sección "Observaciones Previas al Análisis con Copilot".

**1.2 — Preparación del extracto de datos para Copilot**

Dado que Copilot Chat tiene límites de contexto, utilizarás un extracto representativo del CSV. Sigue estos pasos:

1. En Excel, selecciona las primeras **50 filas de datos** (más la fila de encabezados).
2. Copia las celdas seleccionadas (Ctrl+C).
3. Abre **Bloc de Notas** y pega el contenido (Ctrl+V). Guarda como `extracto_alfa1.txt`.

> 💡 **Alternativa:** Si tu versión de Copilot Chat empresarial permite adjuntar archivos, puedes subir directamente el archivo `POZO_FICTICIO_ALFA_Registros.csv` usando el botón de adjuntar archivo (📎) en la interfaz. El instructor indicará cuál método usar según la configuración disponible.

**1.3 — Primer prompt: Resumen del dataset**

1. Abre Copilot Chat en tu navegador: `https://m365.cloud.microsoft/chat`
2. Inicia una **nueva conversación**.
3. Si adjuntas archivo: sube `POZO_FICTICIO_ALFA_Registros.csv` primero, luego escribe el prompt.
   Si pegas texto: copia el contenido de `extracto_alfa1.txt` e inclúyelo en el prompt entre triple comillas.

Escribe el siguiente prompt (cópialo exactamente, adaptando el método de carga):

```
Actúa como un geólogo de subsuelo experto en análisis de registros de perforación.
Tengo un archivo CSV del pozo ficticio Alfa-1 con las siguientes columnas:
DEPTH_MD [m], GR [API], RHOB [g/cc], NPHI [v/v], RT [ohm·m],
LITHO_DESC [texto], COLOR [texto], HARDNESS [1-5], NOTES [texto].
El intervalo de profundidades es 1,450 m a 1,650 m.

Por favor, analiza los datos y proporciona:
1) Rangos mínimo y máximo de cada curva numérica (GR, RHOB, NPHI, RT).
2) Porcentaje estimado de valores nulos o faltantes por columna.
3) Lista de posibles outliers usando la regla de 1.5×IQR para GR, RHOB, NPHI y RT.
4) Tramos con posible pérdida de datos continuos (>2 m sin registro válido).
5) Tabla resumen en formato Markdown.

Indica claramente cualquier supuesto que hagas en el análisis.
```

4. Envía el prompt y espera la respuesta completa.
5. Copia la respuesta de Copilot en la sección "Actividad 1 — Resumen del Dataset" de tu plantilla.

#### Salida Esperada

Copilot debe generar una tabla Markdown similar a la siguiente (los valores variarán según el dataset):

```markdown
| Curva  | Mínimo   | Máximo    | % Nulos | Outliers detectados (IQR) |
|--------|----------|-----------|---------|---------------------------|
| GR     | 12 API   | 187 API   | 1.5%    | 3 valores >175 API        |
| RHOB   | 2.05 g/cc| 2.78 g/cc | 0.5%    | 1 valor <2.1 g/cc         |
| NPHI   | 0.04 v/v | 0.38 v/v  | 2.0%    | 2 valores >0.35 v/v       |
| RT     | 0.8 ohm·m| 245 ohm·m | 1.0%    | 4 valores >200 ohm·m      |
```

Además, Copilot debe listar los supuestos utilizados (ej. "Asumí que los valores nulos están representados por celdas vacías o -999.25, convención estándar LAS").

#### Verificación

- [ ] La tabla contiene las 4 curvas numéricas con rangos y porcentaje de nulos.
- [ ] Copilot identificó al menos un outlier en alguna curva.
- [ ] La respuesta incluye una sección de supuestos o notas metodológicas.
- [ ] Copiaste la respuesta completa en tu plantilla de documentación.

---

### Actividad 2: Identificación de Patrones Litológicos Recurrentes (15 minutos)

**Objetivo:** Formular prompts con reglas explícitas para que Copilot identifique patrones litológicos recurrentes y tendencias estratigráficas en el registro del pozo Alfa-1.

#### Instrucciones

**2.1 — Prompt para identificación de patrones litológicos**

En la **misma conversación** de Copilot (para mantener el contexto del dataset), escribe el siguiente prompt:

```
Utilizando los datos del pozo Alfa-1 que ya tienes en contexto,
identifica patrones litológicos recurrentes aplicando estas reglas:

REGLAS DE INTERPRETACIÓN:
- Arena limpia: GR < 50 API, RHOB entre 2.15–2.35 g/cc, NPHI < 0.20 v/v
- Lutita / Shale: GR > 100 API, RHOB > 2.45 g/cc, NPHI > 0.28 v/v
- Caliza densa: GR < 30 API, RHOB > 2.60 g/cc, NPHI < 0.12 v/v
- Arena arcillosa: GR entre 50–100 API, RHOB entre 2.30–2.50 g/cc
- Zona ambigua: no cumple criterios anteriores claramente

TAREA:
1) Clasifica cada intervalo de 5 m en una de las litologías anteriores.
2) Identifica secuencias repetitivas (ej. arena–lutita–arena o ciclos granodecrecientes).
3) Señala los 3 intervalos con mayor confianza de clasificación y los 3 con mayor ambigüedad.
4) Devuelve los resultados en una tabla Markdown con columnas:
   depth_top_m | depth_base_m | litologia_probable | confianza (Alta/Media/Baja) | evidencia_curvas

Limita tu respuesta a hipótesis interpretativas, no a conclusiones definitivas.
```

Envía el prompt y espera la respuesta.

**2.2 — Refinamiento del prompt (iteración 1)**

Observa la respuesta anterior. Si Copilot no identificó secuencias repetitivas o los intervalos son demasiado amplios, refina el prompt:

```
Buen análisis. Ahora enfócate específicamente en:
1) Identificar ciclos sedimentarios completos (secuencias que empiecen en arena limpia
   y terminen en lutita, o viceversa) dentro del rango 1,480–1,600 m.
2) Para cada ciclo identificado, indica:
   - Profundidad de inicio y fin del ciclo.
   - Tipo de ciclo: granodecreciente (coarsening-up) o granocreciente (fining-up).
   - Espesor total del ciclo en metros.
3) ¿Observas algún patrón de repetición en la frecuencia de estos ciclos?
Responde con una tabla y un párrafo interpretativo de 3–4 oraciones.
```

Envía el prompt refinado y registra ambas respuestas en tu plantilla.

**2.3 — Documentación comparativa**

En tu plantilla, completa la siguiente tabla comparativa:

| Aspecto | Prompt 2.1 (general) | Prompt 2.2 (refinado) |
|---------|---------------------|----------------------|
| Nivel de detalle de la respuesta | | |
| ¿Identificó ciclos sedimentarios? | | |
| Claridad de la evidencia citada | | |
| Utilidad práctica del resultado | | |

#### Salida Esperada

Copilot debe generar una tabla de clasificación litológica por intervalos de 5 m, similar a:

```markdown
| depth_top_m | depth_base_m | litologia_probable | confianza | evidencia_curvas               |
|-------------|-------------|-------------------|-----------|-------------------------------|
| 1,480       | 1,485       | Arena limpia      | Alta      | GR=28 API; RHOB=2.22; NPHI=0.15|
| 1,485       | 1,490       | Arena arcillosa   | Media     | GR=72 API; RHOB=2.38; NPHI=0.22|
| 1,490       | 1,495       | Lutita            | Alta      | GR=142 API; RHOB=2.52; NPHI=0.31|
| ...         | ...         | ...               | ...       | ...                            |
```

El prompt refinado debe producir una descripción de ciclos sedimentarios con espesores y tipo de apilamiento.

#### Verificación

- [ ] La tabla del prompt 2.1 contiene al menos 15 intervalos clasificados.
- [ ] Se identificaron al menos 2 litologías distintas con confianza "Alta".
- [ ] El prompt refinado (2.2) produjo información adicional sobre ciclos sedimentarios.
- [ ] Completaste la tabla comparativa en tu plantilla.

---

### Actividad 3: Detección de Quiebres de Formación y Cambios Estratigráficos (15 minutos)

**Objetivo:** Utilizar prompts con criterios estratigráficos explícitos para que Copilot identifique quiebres de formación y límites de secuencia en el registro del pozo Alfa-1.

#### Instrucciones

**3.1 — Prompt para límites de secuencia**

En la misma conversación, escribe:

```
Ahora necesito identificar quiebres de formación y límites de secuencia estratigráfica
en el registro del pozo Alfa-1. Aplica las siguientes reglas:

CRITERIOS DE QUIEBRE DE FORMACIÓN:
- Cambio abrupto de GR: variación >40 API en menos de 2 m de profundidad.
- Cambio de tendencia sostenida de GR: de descendente a ascendente (o viceversa)
  mantenida por más de 10 m.
- Confirmación requerida: el cambio en GR debe estar acompañado de variación
  concordante en RT (>50% de cambio relativo) O en RHOB (>0.15 g/cc de cambio).

TIPOS DE LÍMITE:
- Límite de Secuencia (LS): cambio abrupto con erosión aparente (GR baja bruscamente,
  RT sube significativamente).
- Superficie de Máxima Inundación (MFS): GR en máximo local sostenido, RT en mínimo.
- Superficie Transgresiva (TS): GR comienza tendencia ascendente sostenida desde arena.

SALIDA REQUERIDA:
Devuelve un JSON con la siguiente estructura por cada límite identificado:
{
  "depth_m": número,
  "tipo_limite": "LS" | "MFS" | "TS" | "quiebre_litologico",
  "confianza": número entre 0 y 1,
  "evidencia": "descripción de curvas implicadas",
  "comentario": "interpretación geológica breve"
}

Identifica todos los límites posibles en el rango completo del pozo (1,450–1,650 m).
```

Envía el prompt y registra la respuesta.

**3.2 — Validación con tops conocidos**

El instructor ha proporcionado los siguientes tops conocidos para el pozo Alfa-1 (datos ficticios):

| Marcador | Profundidad (m) | Descripción |
|----------|----------------|-------------|
| Base_Fm_Palmira | 1,468 m | Base de la Formación Arenisca Palmira |
| MFS-1 | 1,512 m | Superficie de Máxima Inundación 1 |
| Top_Fm_LutitaOscura | 1,558 m | Tope de la Formación Lutita Oscura |
| LS-2 | 1,598 m | Límite de Secuencia 2 |

Escribe el siguiente prompt de validación:

```
Alinea los siguientes tops conocidos del pozo Alfa-1 con los límites que identificaste:
- Base_Fm_Palmira: 1,468 m
- MFS-1: 1,512 m
- Top_Fm_LutitaOscura: 1,558 m
- LS-2: 1,598 m

Para cada marcador conocido:
1) Indica si encontraste un límite correspondiente en tu análisis.
2) Calcula la diferencia en metros entre el top conocido y tu límite inferido (delta_m).
3) Clasifica la concordancia como: Buena (delta ≤ 3 m), Moderada (delta 3–8 m),
   Pobre (delta > 8 m) o No detectado.
4) Sugiere una posible razón para las discrepancias mayores a 5 m.

Devuelve una tabla con columnas:
marcador | depth_conocida_m | depth_inferida_m | delta_m | concordancia | comentario
```

Registra la respuesta en tu plantilla.

#### Salida Esperada

**Prompt 3.1 — Ejemplo de salida JSON:**
```json
[
  {
    "depth_m": 1468.5,
    "tipo_limite": "LS",
    "confianza": 0.78,
    "evidencia": "GR cae de 145 a 32 API en 1.5 m; RT sube de 8 a 67 ohm·m",
    "comentario": "Posible superficie erosiva con entrada de arena limpia"
  },
  {
    "depth_m": 1511.0,
    "tipo_limite": "MFS",
    "confianza": 0.71,
    "evidencia": "GR en máximo local 168 API; RT en mínimo 2.3 ohm·m; NPHI alto",
    "comentario": "Probable máxima inundación, lutita condensada"
  }
]
```

**Prompt 3.2 — Ejemplo de tabla de validación:**
```markdown
| marcador            | depth_conocida_m | depth_inferida_m | delta_m | concordancia | comentario                        |
|---------------------|-----------------|-----------------|---------|--------------|-----------------------------------|
| Base_Fm_Palmira     | 1,468           | 1,468.5         | 0.5     | Buena        | Excelente coincidencia            |
| MFS-1               | 1,512           | 1,511.0         | 1.0     | Buena        | Confirmado por GR/RT              |
| Top_Fm_LutitaOscura | 1,558           | 1,563.0         | 5.0     | Moderada     | Posible gradación litológica lenta|
| LS-2                | 1,598           | No detectado    | —       | No detectado | Requiere revisión de criterios    |
```

#### Verificación

- [ ] Copilot generó al menos 4 límites en formato JSON con los campos requeridos.
- [ ] La tabla de validación contiene los 4 marcadores conocidos.
- [ ] Al menos 2 marcadores tienen concordancia "Buena" o "Moderada".
- [ ] Copilot proporcionó comentarios interpretativos para las discrepancias.

---

### Actividad 4: Detección de Anomalías en Propiedades Petrofísicas (10 minutos)

**Objetivo:** Formular prompts específicos para que Copilot señale anomalías en los datos de perforación — valores inesperados de densidad, porosidad o resistividad que no corresponden con la litología descrita.

#### Instrucciones

**4.1 — Prompt para detección de anomalías cruzadas**

En la misma conversación, escribe:

```
Analiza el registro del pozo Alfa-1 en busca de anomalías petrofísicas
que representen inconsistencias entre las curvas y la litología descrita.

TIPOS DE ANOMALÍAS A BUSCAR:
1) Anomalía de densidad: RHOB < 2.10 g/cc en una zona descrita como caliza o arenisca
   compacta (esperaría RHOB > 2.50 g/cc). Posible indicador de vugosidad, fractura
   o error de herramienta.
2) Anomalía de porosidad-densidad: NPHI > 0.30 v/v simultáneamente con RHOB > 2.60 g/cc.
   Separación NPHI-RHOB anómala que puede indicar presencia de gas o dolomía.
3) Anomalía de resistividad en zona arcillosa: RT > 50 ohm·m donde GR > 90 API.
   Posible hidrocarburo en shale o error de escala.
4) Anomalía de GR en caliza: GR > 60 API donde LITHO_DESC indica "caliza".
   Posible caliza arcillosa no descrita o contaminación de muestra.

PARA CADA ANOMALÍA DETECTADA:
- Profundidad exacta (m)
- Tipo de anomalía (según lista anterior)
- Valores observados vs. valores esperados
- Nivel de alerta: ALTA (requiere revisión inmediata), MEDIA (monitorear),
  BAJA (posible variación natural)
- Recomendación de acción

Presenta los resultados en una tabla Markdown ordenada por nivel de alerta
(ALTA primero).
```

Envía el prompt y registra la respuesta.

**4.2 — Prompt de anomalía específica (refinamiento)**

Si Copilot detectó alguna anomalía de nivel ALTA, escribe el siguiente prompt de seguimiento:

```
Para la anomalía de mayor alerta que identificaste, proporciona:
1) Un análisis más detallado del intervalo ±5 m alrededor de esa profundidad.
2) Tres hipótesis geológicas que podrían explicar esta anomalía, ordenadas
   de mayor a menor probabilidad según el contexto del pozo Alfa-1.
3) Qué dato adicional (núcleo, análisis de fluido, registro sónico DT)
   ayudaría más a confirmar o descartar cada hipótesis.
Responde en formato de lista estructurada.
```

#### Salida Esperada

Copilot debe generar una tabla de anomalías similar a:

```markdown
| Profundidad (m) | Tipo Anomalía          | Valor Observado         | Valor Esperado      | Alerta | Recomendación                        |
|-----------------|------------------------|-------------------------|---------------------|--------|--------------------------------------|
| 1,523.5         | Resistividad en shale  | RT=87 ohm·m, GR=118 API | RT<10 en shale      | ALTA   | Revisar posible hidrocarburo en shale|
| 1,487.0         | Densidad baja en caliza| RHOB=2.08, desc="caliza" | RHOB>2.55 en caliza | ALTA   | Verificar vugosidad o fractura        |
| 1,541.0         | Separación NPHI-RHOB   | NPHI=0.32, RHOB=2.62    | Valores consistentes| MEDIA  | Evaluar presencia de gas             |
| 1,612.5         | GR alto en caliza      | GR=74 API, desc="caliza" | GR<30 en caliza     | BAJA   | Posible caliza arcillosa             |
```

#### Verificación

- [ ] Copilot detectó al menos 3 tipos distintos de anomalías petrofísicas.
- [ ] Al menos una anomalía fue clasificada como alerta ALTA.
- [ ] El prompt de refinamiento (4.2) produjo hipótesis geológicas específicas.
- [ ] Registraste ambas respuestas en tu plantilla de documentación.

---

### Actividad 5: Síntesis Interpretativa y Comparación de Prompts (15 minutos)

**Objetivo:** Solicitar a Copilot un resumen interpretativo ejecutivo del perfil litológico completo y reflexionar sobre la efectividad de las distintas estructuras de prompts utilizadas.

#### Instrucciones

**5.1 — Prompt de resumen ejecutivo**

En la misma conversación, escribe el prompt final de síntesis:

```
Con base en todo el análisis realizado del pozo ficticio Alfa-1
(patrones litológicos, quiebres de formación, anomalías petrofísicas),
redacta un resumen interpretativo ejecutivo con la siguiente estructura:

FORMATO REQUERIDO:

## Resumen Interpretativo — Pozo Alfa-1 (Ficticio)

### 1. Descripción del Perfil Litológico
(2–3 oraciones describiendo las principales litologías identificadas
y su distribución en profundidad)

### 2. Secuencia Estratigráfica Principal
(Describe los límites de secuencia más significativos, superficies clave
identificadas y el modelo deposicional inferido en 3–4 oraciones)

### 3. Intervalos de Mayor Interés Geológico
(Lista de 3 intervalos con sus profundidades, razón de interés
y nivel de confianza: Alto/Medio/Bajo)

### 4. Anomalías Críticas Detectadas
(Resumen de las 2 anomalías más importantes y su implicación)

### 5. Incertidumbres y Datos Adicionales Requeridos
(2–3 limitaciones del análisis y qué información adicional
reduciría la incertidumbre: núcleos, análisis de fluidos, etc.)

### 6. Próximos Pasos Recomendados
(3 acciones concretas en orden de prioridad)

El resumen debe tener entre 250–350 palabras, usar terminología geológica
apropiada y ser comprensible para una audiencia técnica gerencial.
```

Envía el prompt y registra la respuesta completa en tu plantilla.

**5.2 — Comparación de estructuras de prompts**

Revisa todos los prompts que utilizaste durante la práctica. En tu plantilla, completa la siguiente tabla de análisis comparativo:

| Prompt | Actividad | Tipo de estructura | Resultado obtenido | Calidad (1–5) | Lección aprendida |
|--------|-----------|-------------------|-------------------|--------------|-------------------|
| Prompt 1.3 | Resumen dataset | Listado numerado + formato tabla | | | |
| Prompt 2.1 | Patrones litológicos | Reglas explícitas + formato tabla | | | |
| Prompt 2.2 | Ciclos sedimentarios | Refinamiento iterativo + párrafo | | | |
| Prompt 3.1 | Límites de secuencia | Criterios + formato JSON | | | |
| Prompt 3.2 | Validación con tops | Datos conocidos + tabla | | | |
| Prompt 4.1 | Anomalías | Tipología + alerta + acción | | | |
| Prompt 5.1 | Resumen ejecutivo | Plantilla estructurada | | | |

**5.3 — Reflexión individual (5 minutos)**

Responde brevemente en tu plantilla:

1. ¿Qué elemento del prompt tuvo mayor impacto en la calidad de la respuesta de Copilot? (ej. especificar formato, dar reglas explícitas, pedir supuestos)
2. ¿En qué actividad encontraste mayor variabilidad o resultados menos esperados? ¿Cómo lo resolverías con un prompt más preciso?
3. ¿Qué limitaciones observaste en Copilot para este tipo de análisis geológico?

#### Salida Esperada

El resumen ejecutivo debe:
- Tener entre 250 y 350 palabras.
- Mencionar las 6 secciones solicitadas.
- Citar profundidades específicas del análisis.
- Incluir al menos 2 términos técnicos geológicos (ej. "superficie de máxima inundación", "ciclo granodecreciente").
- Señalar explícitamente las incertidumbres del análisis.

#### Verificación

- [ ] El resumen ejecutivo contiene las 6 secciones solicitadas.
- [ ] La tabla comparativa de prompts está completada con evaluaciones de calidad.
- [ ] Respondiste las 3 preguntas de reflexión en tu plantilla.
- [ ] Guardaste la plantilla completa en tu carpeta de trabajo local.

---

## Validación y Pruebas

Al finalizar todas las actividades, verifica que has completado los siguientes entregables:

### Lista de Verificación Final

| Entregable | Descripción | ¿Completado? |
|-----------|-------------|-------------|
| **Plantilla documentada** | `Plantilla_Registro_Prompts_P01.docx` con todas las secciones completadas | ☐ |
| **Resumen del dataset** | Tabla con rangos, nulos y outliers por curva (Actividad 1) | ☐ |
| **Tabla de clasificación litológica** | Intervalos de 5 m clasificados con confianza y evidencia (Actividad 2) | ☐ |
| **JSON de límites de secuencia** | Al menos 4 límites identificados con tipo y confianza (Actividad 3) | ☐ |
| **Tabla de validación con tops** | Comparación de 4 marcadores conocidos vs. inferidos (Actividad 3) | ☐ |
| **Tabla de anomalías petrofísicas** | Al menos 3 anomalías con nivel de alerta (Actividad 4) | ☐ |
| **Resumen ejecutivo** | Texto de 250–350 palabras con 6 secciones (Actividad 5) | ☐ |
| **Tabla comparativa de prompts** | 7 prompts evaluados con calidad y lecciones (Actividad 5) | ☐ |

### Prueba de Calidad del Análisis

Para validar que el análisis fue técnicamente coherente, responde estas preguntas sin usar Copilot:

1. **Pregunta de coherencia litológica:** Si GR = 145 API y RHOB = 2.55 g/cc, ¿qué litología esperarías según las reglas definidas en la Actividad 2? ¿Coincide con lo que Copilot clasificó para valores similares?

2. **Pregunta de límites de secuencia:** ¿Cuál es la diferencia conceptual entre un Límite de Secuencia (LS) y una Superficie de Máxima Inundación (MFS)? ¿Copilot distinguió correctamente estos dos tipos en su análisis?

3. **Pregunta sobre anomalías:** La anomalía de "separación NPHI-RHOB" (NPHI alto + RHOB alto simultáneamente) ¿qué podría indicar geológicamente? ¿La explicación de Copilot fue consistente con este concepto?

> 📌 Comparte tus respuestas con el instructor o en la discusión grupal al finalizar la práctica.

---

## Solución de Problemas

### Problema 1: Copilot no reconoce o interpreta incorrectamente los datos pegados en el chat

**Síntoma:** Al pegar el extracto CSV en el prompt, Copilot responde que no puede ver los datos, interpreta los valores como texto sin sentido, o genera rangos y estadísticas completamente incorrectas (ej. reporta GR máximo de 5 API cuando el dataset tiene valores de hasta 187 API).

**Causa probable:** El formato de pegado del CSV perdió la estructura tabular al copiarse desde Excel al Bloc de Notas, resultando en una cadena de texto sin delimitadores claros. Alternativamente, Copilot recibió demasiados datos en un solo mensaje y procesó solo una fracción del contexto.

**Solución:**
1. En Excel, selecciona el extracto de datos (máximo 30–40 filas para mayor confiabilidad).
2. Copia y pega en Notepad++. Verifica que las columnas estén separadas por tabulaciones o comas.
3. Al insertar en el prompt, precede los datos con una instrucción explícita de formato:
   ```
   Los siguientes datos están en formato CSV (separado por comas).
   La primera fila es el encabezado. Cada fila representa una medición a una profundidad específica:
   
   DEPTH_MD,GR,RHOB,NPHI,RT,LITHO_DESC
   1450.0,45,2.28,0.18,12.5,Arenisca
   1450.5,48,2.30,0.17,14.2,Arenisca
   ...
   ```
4. Si el problema persiste, intenta subir el archivo CSV directamente usando el botón de adjuntar archivo (📎) en Copilot Chat, si está disponible en tu licencia.
5. Como alternativa, reduce el extracto a 20 filas e incluye una descripción estadística manual: "Los datos tienen GR entre 12 y 187 API, RHOB entre 2.05 y 2.78 g/cc..."

---

### Problema 2: Las respuestas de Copilot son genéricas o no aplican las reglas específicas del prompt

**Síntoma:** Copilot genera una respuesta sobre análisis de registros de perforación en términos muy generales (ej. "El GR alto indica arcillas...") sin aplicar los criterios numéricos específicos definidos en el prompt (ej. "GR < 50 API = arena limpia"), sin producir la tabla solicitada, o sin usar el formato JSON requerido.

**Causa probable:** El prompt es demasiado extenso y Copilot priorizó el contexto general sobre las instrucciones específicas de formato y reglas. También puede ocurrir cuando las reglas están mezcladas con el contexto sin una separación visual clara, o cuando la conversación ha acumulado demasiado historial y el contexto inicial se diluyó.

**Solución:**
1. **Refuerza las instrucciones de formato al inicio y al final del prompt:**
   ```
   IMPORTANTE: Debes responder ÚNICAMENTE con una tabla Markdown.
   No incluyas texto introductorio ni conclusiones fuera de la tabla.
   ```
2. **Separa visualmente las secciones del prompt** usando etiquetas en mayúsculas (como se muestra en los prompts de esta práctica): `REGLAS:`, `TAREA:`, `FORMATO DE SALIDA:`.
3. **Reduce la longitud del prompt:** Si el prompt tiene más de 300 palabras, divídelo en dos mensajes consecutivos: primero establece las reglas, luego solicita la tarea.
4. **Inicia una nueva conversación** si el historial es muy largo. Repega el contexto del dataset y las reglas en el nuevo chat antes de hacer la pregunta.
5. **Usa un ejemplo en el prompt** (técnica "few-shot"): muestra a Copilot una fila de ejemplo con el formato de salida esperado para que replique la estructura:
   ```
   Ejemplo de fila esperada en la tabla:
   | 1480 | 1485 | Arena limpia | Alta | GR=28; RHOB=2.22; NPHI=0.15 |
   ```

---

## Limpieza del Entorno

Al finalizar la práctica, realiza los siguientes pasos de cierre:

### Guardado de Trabajo

```
1. Guarda la Plantilla_Registro_Prompts_P01.docx actualizada en:
   C:\LabGeo\Practica01\[TuNombre]_P01_Completada.docx

2. Sube el archivo completado a la carpeta de entrega en OneDrive/SharePoint:
   [URL de carpeta de entrega proporcionada por el instructor]
   Módulo_01 > Entregas > Práctica_01 > [TuNombre]/

3. Opcional: Exporta la conversación de Copilot (usa Ctrl+A para seleccionar
   todo el texto de la conversación, copia y pega en un documento Word adicional
   como respaldo).
```

### Cierre de Sesión y Archivos

```
1. Cierra la pestaña de Copilot Chat en el navegador.
   NO es necesario cerrar sesión de Microsoft 365 si usas una computadora personal.
   SÍ cierra sesión si usas una computadora compartida o de sala de entrenamiento.

2. Cierra Excel y Word. Guarda los cambios si se solicita.

3. Los archivos de práctica (POZO_FICTICIO_ALFA_Registros.xlsx/.csv)
   pueden conservarse en tu carpeta local para referencia futura.
   No contienen datos reales ni confidenciales.

4. Elimina el archivo extracto_alfa1.txt de tu escritorio o carpeta temporal
   si ya no lo necesitas.
```

### Verificación de Entrega

- [ ] Plantilla completada subida a la carpeta de entrega en OneDrive/SharePoint.
- [ ] Archivo nombrado correctamente: `[TuNombre]_P01_Completada.docx`
- [ ] Sesión cerrada en computadoras compartidas.

---

## Resumen

### Puntos Clave Aprendidos

En esta práctica aplicaste Microsoft Copilot Chat como asistente de análisis geológico para trabajar con registros de perforación estructurados. Los conceptos y habilidades clave que desarrollaste incluyen:

1. **Carga de contexto estructurado:** Aprendiste a proporcionar datos tabulares a Copilot con instrucciones de formato explícitas para obtener análisis coherentes y reproducibles.

2. **Prompts con reglas geológicas explícitas:** Comprobaste que definir criterios numéricos precisos (ej. "GR < 50 API = arena limpia") en el prompt produce clasificaciones litológicas mucho más útiles que preguntas abiertas.

3. **Detección de quiebres de formación:** Utilizaste la combinación de curvas GR + RT (y opcionalmente RHOB/NPHI) con criterios de cambio de tendencia para que Copilot identificara límites de secuencia estratigráfica, incluyendo Límites de Secuencia (LS), Superficies de Máxima Inundación (MFS) y Superficies Transgresivas (TS).

4. **Identificación de anomalías petrofísicas:** Formulaste prompts con tipología de anomalías cruzadas (densidad-litología, resistividad-arcillosidad, separación NPHI-RHOB) y niveles de alerta para priorizar la revisión de intervalos problemáticos.

5. **Refinamiento iterativo de prompts:** Experimentaste cómo pequeños cambios en la especificidad, el formato de salida solicitado y la separación visual de instrucciones impactan significativamente la calidad de las respuestas de Copilot.

6. **Validación con datos conocidos:** Practicaste la alineación de interpretaciones de Copilot con tops conocidos, un paso crítico para anclar el análisis asistido por IA en evidencia geológica verificable.

> ⚠️ **Recordatorio fundamental:** Copilot Chat es un asistente que acelera el análisis preliminar y la generación de hipótesis. Sus interpretaciones **deben validarse** con datos de núcleos, análisis petrofísicos formales, correcciones ambientales y el criterio del geocientífico experto. Nunca utilices las salidas de Copilot como base única para decisiones técnicas de perforación o evaluación de reservas.

### Recursos de Referencia

| Recurso | Descripción | URL |
|---------|-------------|-----|
| AAPG Wiki — Sequence Stratigraphy | Fundamentos de estratigrafía de secuencias | https://wiki.aapg.org/Sequence_stratigraphy |
| SPE Petrowiki — Well Logging | Visión general de registros de pozo | https://petrowiki.spe.org/Well_logging |
| SLB Oilfield Glossary | Terminología de registros y petrofísica | https://www.glossary.slb.com |
| Canadian Well Logging Society — LAS Format | Especificación del formato LAS | https://www.cwls.org/las/ |
| Microsoft Copilot Chat — Documentación | Guía de uso empresarial | https://docs.microsoft.com/copilot |
| lasio (Python) | Librería para lectura de archivos LAS | https://lasio.readthedocs.io |

### Adelanto de la Próxima Práctica

En la **Práctica 2**, integrarás informes de campo, descripciones de recortes y tops de pozo para correlacionar el perfil del pozo Alfa-1 con un pozo análogo (Pozo Beta-1). Aprenderás a usar Copilot para identificar discontinuidades laterales, proponer correlaciones estratigráficas entre pozos y generar alertas de riesgo geológico basadas en la comparación de perfiles.

---

*Práctica 01 — Módulo 1: Análisis de Registros de Perforación y Secuencias Geológicas con Copilot*
*Duración estimada: 70 minutos | Nivel Bloom: Aplicar | Complejidad: Media*
