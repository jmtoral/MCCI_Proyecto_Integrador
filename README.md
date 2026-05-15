# 🏛️ MCCI — Contratos de Partidos Políticos

> **Mexicanos Contra la Corrupción y la Impunidad (MCCI)**  
> Material educativo para el análisis de datos de contrataciones públicas de partidos políticos en México.

---

## 📋 Descripción del proyecto

Este repositorio contiene el material de trabajo y los avances del análisis de los datos compartidos por **Mexicanos Contra la Corrupción y la Impunidad (MCCI)**, una organización de la sociedad civil dedicada a combatir la corrupción en México mediante investigación periodística y datos abiertos.

El objetivo es que los estudiantes aprendan a explorar, limpiar, comparar y visualizar datos de contratos gubernamentales usando **R** y **Quarto**, siguiendo buenas prácticas de ciencia de datos reproducible.

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

## 📝 Notas para los estudiantes

1. **No modifiques los datos originales** en la carpeta `datos/`. Si necesitas limpiar o transformar datos, hazlo en tus notebooks y guarda los resultados en una nueva carpeta `datos/procesados/`.
2. **Documenta tu código**: cada bloque de código debe tener un comentario que explique qué hace y por qué.
3. **Usa nombres descriptivos** para variables y funciones.
4. **Haz commits frecuentes** con mensajes claros en español.

---

## 🤝 Créditos

Datos proporcionados por **Mexicanos Contra la Corrupción y la Impunidad (MCCI)**.  
Material didáctico preparado para el curso de Análisis de Datos.
