# 🏛️ MCCI — Contratos de Partidos Políticos

> **Mexicanos Contra la Corrupción y la Impunidad (MCCI)**  
> Material educativo para el análisis de datos de contrataciones públicas de partidos políticos en México.

---

## 📋 Descripción del proyecto

Este repositorio contiene el material de trabajo y los avances del análisis de los datos compartidos por **Mexicanos Contra la Corrupción y la Impunidad (MCCI)**, una organización de la sociedad civil dedicada a combatir la corrupción en México mediante investigación periodística y datos abiertos.

El objetivo es que las **personas participantes de la clase** aprendan a explorar, limpiar, comparar y visualizar datos de contratos gubernamentales usando **R** y **Quarto**, siguiendo buenas prácticas de ciencia de datos reproducible.

---

## 📁 Estructura del repositorio

```
MCCI_Proyecto_Integrador/
├── datos/                    # Datos crudos proporcionados por MCCI
│   ├── contratos.csv         # Dataset principal de contratos
│   └── contratos_montos.csv  # Dataset de contratos con montos y partido
├── notebooks/                # Análisis en Quarto (.qmd)
│   └── 01_exploracion.qmd    # Exploración y comparación de datasets
├── scripts/                  # Scripts auxiliares de R
│   └── utils.R               # Funciones de utilidad reutilizables
├── docs/                     # Documentos auxiliares y diccionarios de datos
│   └── diccionario_datos.md  # Descripción detallada de cada variable
├── _quarto.yml               # Configuración del proyecto Quarto
└── README.md                 # Este archivo
```

---

## 🗂️ Descripción de los datasets

### 1. `contratos.csv` — Contratos de partidos políticos

| Atributo | Detalle |
|---|---|
| **Fuente** | Mexicanos Contra la Corrupción y la Impunidad (MCCI) |
| **Filas** | ~15,736 contratos |
| **Columnas** | 28 variables |
| **Cobertura** | Contratos celebrados por partidos políticos en México |
| **Identificador** | `id` (único por contrato) |

Este dataset contiene el registro de contratos de bienes y servicios celebrados por partidos políticos mexicanos. Incluye información sobre el tipo de contrato, el proveedor (persona física o moral), las fechas de vigencia, el monto, el área responsable y la URL del documento soporte.

**Variables principales:**

| Variable | Tipo | Descripción |
|---|---|---|
| `id` | Numérico | Identificador único del contrato |
| `ano` | Entero | Año del periodo reportado |
| `fecha_inicio_periodo` | Fecha | Inicio del periodo de reporte |
| `fecha_fin_periodo` | Fecha | Fin del periodo de reporte |
| `tipo_contrato` | Texto | Tipo (Adquisición, Prestación de servicio, etc.) |
| `tipo_persona` | Texto | Física o Moral |
| `fisica_nombre` | Texto | Nombre del proveedor (persona física) |
| `fisica_apellido1` | Texto | Primer apellido |
| `fisica_apellido2` | Texto | Segundo apellido |
| `moral_razon` | Texto | Razón social (persona moral) |
| `fecha_firma` | Fecha | Fecha de firma del contrato |
| `tema` | Texto | Categoría temática del contrato |
| `descripcion` | Texto | Descripción del objeto del contrato |
| `url` | Texto | Enlace al documento oficial |
| `fecha_inicio_vigencia` | Fecha | Inicio de la vigencia |
| `fecha_fin_vigencia` | Fecha | Fin de la vigencia |
| `alcance` | Texto | Alcance o tipo de adquisición |
| `costo` | Numérico | Monto del contrato (pesos mexicanos) |
| `area` | Texto | Área del partido responsable |
| `fecha_actualizacion` | Fecha | Fecha de actualización del registro |
| `nota` | Texto | Notas aclaratorias |
| `partido_archivo` | Texto | Partido político al que pertenece el registro |
| `ano_archivo` | Numérico | Año del archivo fuente |
| `archivo` | Texto | Nombre del archivo fuente original |
| `fecha_validacion` | Fecha | Fecha de validación del dato |
| `nom_fisica` | Texto | Nombre completo normalizado (persona física) |
| `nom_fisica_homo` | Texto | Nombre homologado para cruce de datos |
| `moral_razon_homo` | Texto | Razón social homologada para cruce de datos |

---

### 2. `contratos_montos.csv` — Contratos con montos y partido identificado

| Atributo | Detalle |
|---|---|
| **Fuente** | Mexicanos Contra la Corrupción y la Impunidad (MCCI) |
| **Filas** | ~15,118 contratos |
| **Columnas** | 30 variables |
| **Cobertura** | Subconjunto de `contratos.csv` con partido político explícito |
| **Identificador** | `id` (compartido con `contratos.csv`) |

Este dataset es una versión derivada de `contratos.csv` que incluye **dos columnas adicionales**:

- **`partido`** — Nombre del partido político en formato estandarizado, lo que facilita filtros y agrupaciones directas sin necesidad de parsear la columna `partido_archivo`.
- **`H1`** — Índice de fila heredado del archivo fuente (columna auxiliar, puede ignorarse en análisis).

> ⚠️ **Diferencia clave:** `contratos_montos.csv` tiene **618 filas menos** que `contratos.csv`. Esto sugiere que ciertos registros fueron filtrados (por ejemplo, contratos sin monto registrado o sin partido identificable), lo cual debe considerarse al comparar resultados entre ambos archivos.

---

## 🔍 Diferencias entre datasets

| Característica | `contratos.csv` | `contratos_montos.csv` |
|---|---|---|
| Filas | 15,736 | 15,118 |
| Columnas | 28 | 30 |
| Columna `partido` | ❌ No | ✅ Sí (explícita) |
| Columna índice (`H1`) | ❌ No | ✅ Sí (auxiliar) |
| Filtrado | Todos los registros | Sin registros sin partido claro |
| Uso recomendado | Exploración completa | Análisis por partido |

---

## 🚀 Cómo usar este repositorio

### Requisitos

- [R](https://cran.r-project.org/) ≥ 4.3
- [Quarto](https://quarto.org/) ≥ 1.4
- Paquetes R: `tidyverse`, `janitor`, `skimr`, `gt`, `ggplot2`, `readr`

### Instalación de paquetes

```r
install.packages(c("tidyverse", "janitor", "skimr", "gt", "ggplot2", "readr", "knitr"))
```

### Renderizar el análisis

```bash
quarto render notebooks/01_exploracion.qmd
```

O desde RStudio, abrir el archivo `.qmd` y hacer clic en **Render**.

---

## 📚 Recursos de apoyo

- [MCCI — Página oficial](https://contralacorrupcion.mx/)
- [Quarto — Documentación oficial](https://quarto.org/docs/guide/)
- [R for Data Science (español)](https://es.r4ds.hadley.nz/)
- [The tidyverse style guide](https://style.tidyverse.org/)

---

## 📝 Lineamientos para personas participantes de la clase

### Sobre el uso del código de este repositorio

Las personas participantes de la clase pueden **reutilizar, adaptar y extender libremente el código** de este repositorio, con una condición esencial:

> **La pregunta de investigación y el problema que resuelves deben ser originales y propios.**

Copiar el análisis completo cambiando únicamente el nombre del archivo de datos **no cuenta** como trabajo propio. Se espera que cada persona traiga una perspectiva, hipótesis o enfoque analítico genuino que aporte algo nuevo al entendimiento de los datos.

**Otras reglas de convivencia:**

1. **No modifiques los datos originales** en `datos/`. Cualquier transformación debe ocurrirr dentro de tus notebooks; guarda resultados en `datos/procesados/`.
2. **Documenta tu código**: cada bloque debe tener un comentario que explique *qué hace* y *por qué*.
3. **Usa nombres descriptivos** para objetos y funciones (no `df2`, `x`, `temp`).
4. **Haz commits frecuentes** con mensajes claros y en español.

---

## 🤖 Política de uso responsable de inteligencia artificial

El uso de herramientas de IA (ChatGPT, Claude, Gemini, Copilot, etc.) está **permitido y fomentado** en este curso. Sin embargo, su uso conlleva responsabilidades:

### ✅ Lo que se espera

1. **Da crédito explícito.** Si una sección de tu código o texto fue generada o asistida por una IA, indícalo con un comentario:
   ```r
   # Generado con ayuda de Claude (Anthropic), mayo 2026.
   # Prompt: "Escribe una función en R que calcule el monto promedio por partido"
   ```
   En prosa, basta con una nota al pie o en el encabezado del documento.

2. **Incluye el prompt que usaste.** No solo el resultado: muestra *cómo* le preguntaste a la IA. Un prompt bien construido es una habilidad valiosa en sí misma.

3. **Verifica y comprende todo lo que entregas.** La IA comete errores, escribe código que no corre, e inventa referencias. Tú eres responsable del contenido final. Si no puedes explicar lo que entregaste línea por línea, no lo entregues.

### 💡 Buenas prácticas de prompting

| Práctica | Ejemplo |
|---|---|
| **Sé específico con el contexto** | *"Tengo un dataframe en R con columnas `partido`, `costo` y `ano`. Quiero calcular el monto total por partido usando `dplyr`."* |
| **Pide explicaciones, no solo código** | *"Explícame qué hace cada línea del código que generaste."* |
| **Itera y refina** | Si el resultado no es correcto, describe el error exacto y pide una corrección. |
| **Usa la IA para aprender** | *"¿Por qué usas `group_by()` antes de `summarise()`? ¿Qué pasaría si no lo hago?"* |
| **Pide alternativas** | *"¿Existe una forma más eficiente o legible de hacer esto mismo?"* |
| **No compartas datos sensibles** | Nunca pegues datos personales o confidenciales en un prompt público. |

> ⚠️ **Aviso:** Entregar trabajo generado por IA sin crédito ni comprensión propia se considera deshonestidad académica, igual que copiar de otra persona.

---

## 📊 Política de visualización de datos

El diseño de las gráficas **se evalúa**. Los notebooks de este repositorio muestran visualizaciones deliberadamente simples —escala de grises, estilo base de ggplot2— para que cada persona participante las mejore desde cero.

### 🚫 Está estrictamente prohibido entregar:

- **Pasteles** (*pie charts*)
- **Donas** (*donut charts*)
- **Cualquier gráfica circular** de cualquier variante

Estas formas son cognitivamente ineficientes para comparar proporciones y están [ampliamente desaconsejadas](https://www.data-to-viz.com/caveat/pie.html) en la literatura de visualización de datos.

### ✅ Se evaluará positivamente:

- Elección apropiada del tipo de gráfica para los datos
- Uso coherente y accesible del color
- Títulos, subtítulos, etiquetas de ejes y nota de fuente presentes
- Jerarquía visual clara y tipografía cuidada
- Buen gusto: menos es más

> 💬 *"A chart is only as good as the thinking behind it."* — Edward Tufte

---

## 🤖 Ideas de proyectos con Machine Learning

Estos datos ofrecen un terreno fértil para aplicar técnicas de ML de nivel introductorio. A continuación encontrarás ideas organizadas por tipo de problema, de menor a mayor complejidad.

> 💡 Recuerda: el valor de un buen proyecto de ML no está solo en el modelo, sino en la **pregunta que responde** y en qué tan bien puedes explicar e interpretar los resultados.

---

### 📦 Clasificación

**¿Es posible saber si un proveedor es persona física o moral sin mirar esa columna?**
*Target:* `tipo_persona` · *Features:* `costo`, `tipo_contrato`, `partido`, `ano` · *Por dónde empezar:* regresión logística, árbol de decisión

**¿Puede un modelo adivinar qué partido firmó un contrato a partir de sus características?**
*Target:* `partido` · *Features:* `costo`, `tipo_contrato`, `tipo_persona`, `area`, `ano` · *Por dónde empezar:* Random Forest, KNN

**¿Se puede distinguir entre una adquisición y una prestación de servicio usando solo variables numéricas?**
*Target:* `tipo_contrato` (binarizado) · *Features:* `costo`, `tipo_persona`, `partido`, `duracion_dias` · *Por dónde empezar:* regresión logística

**¿Qué variables predicen mejor si un contrato será de alto valor?**
*Target:* `alto_valor` (variable nueva: `costo > mediana`) · *Features:* `tipo_contrato`, `partido`, `tipo_persona`, `mes_firma` · *Por dónde empezar:* árbol de decisión, Naive Bayes

> **Nota metodológica:** Antes de modelar, discute con tu equipo si el modelo tiene riesgo de aprender sesgos de los datos (p. ej., ¿es justo predecir el partido a partir del monto?).

---

### 📈 Regresión

**¿Podemos estimar el monto de un contrato antes de que se firme?**
*Target:* `costo` (aplicar `log1p`) · *Features:* `tipo_contrato`, `partido`, `tipo_persona`, `ano`, `duracion_dias` · *Por dónde empezar:* regresión lineal, Ridge/Lasso

> **Ojo:** `costo` tiene una distribución muy sesgada. Aplica `log()` antes de modelar y reporta el RMSE en escala original para que el resultado sea interpretable.

**¿Qué factores determinan cuánto dura un contrato?**
*Target:* `fecha_fin_vigencia - fecha_inicio_vigencia` (en días) · *Features:* `costo`, `tipo_contrato`, `partido`, `ano` · *Por dónde empezar:* regresión lineal

---

### 🔍 Clustering (aprendizaje no supervisado)

**¿Existen perfiles distintos de proveedores según cómo contratan?**
Agrupa proveedores por número de contratos, monto total y partidos con los que trabajan. *Por dónde empezar:* K-Means, clustering jerárquico

**¿Se parecen entre sí los partidos en sus patrones de contratación?**
Agrupa partidos por tipos de contrato, montos y proveedores frecuentes. *Por dónde empezar:* K-Means

**¿Hay contratos que parecen anómalos o fuera de lo común?**
Identifica contratos con combinaciones raras de monto, duración y tipo. *Por dónde empezar:* Isolation Forest, DBSCAN

---

### 🔤 Procesamiento de Lenguaje Natural (NLP) — nivel básico

La columna `descripcion` contiene texto libre con el objeto de cada contrato. Algunas preguntas que puedes responder con NLP básico:

**¿De qué hablan los contratos? ¿Hay temas recurrentes por partido?**
*Técnica:* TF-IDF + clasificador, topic modeling (LDA)

**¿Qué palabras distinguen los contratos de un partido de los de otro?**
*Técnica:* n-gramas, nube de palabras comparativa

**¿Se puede clasificar el tema de un contrato a partir de su descripción?**
*Técnica:* TF-IDF + regresión logística o árbol de decisión

---

### 🛠️ Ingeniería de features sugerida

Antes de modelar, considera crear estas variables derivadas que pueden mejorar cualquier modelo:

```r
montos <- montos |>
  mutate(
    # Duración del contrato en días
    duracion_dias = as.numeric(fecha_fin_vigencia - fecha_inicio_vigencia),

    # Mes de firma (estacionalidad)
    mes_firma = month(fecha_firma),

    # ¿Es fin de año? (los gobiernos suelen contratar más en diciembre)
    es_diciembre = month(fecha_firma) == 12,

    # Logaritmo del costo (para modelos de regresión)
    log_costo = log1p(costo),

    # ¿Contrato de alto valor? (por encima de la mediana)
    alto_valor = costo > median(costo, na.rm = TRUE)
  )
```

---

### ⚠️ Advertencias éticas para proyectos de ML con estos datos

1. **Causalidad ≠ correlación.** Que un modelo prediga el partido a partir del monto no significa que el partido *cause* los montos altos.
2. **Los modelos pueden amplificar sesgos** presentes en los datos históricos.
3. **Interpreta siempre tus modelos.** Un modelo que no puedes explicar no es útil en contextos de política pública.
4. **Reporta métricas de evaluación apropiadas** (accuracy, F1, AUC, RMSE según el caso) y discute qué significa cada una.

---

## 🤝 Créditos

Datos proporcionados por **Mexicanos Contra la Corrupción y la Impunidad (MCCI)**.  
Material didáctico preparado para el curso de Análisis de Datos.
