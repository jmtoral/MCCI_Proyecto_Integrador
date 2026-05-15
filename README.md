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

## 🤝 Créditos

Datos proporcionados por **Mexicanos Contra la Corrupción y la Impunidad (MCCI)**.  
Material didáctico preparado para el curso de Análisis de Datos.
