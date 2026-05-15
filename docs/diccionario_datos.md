# 📖 Diccionario de Datos

**Proyecto:** MCCI — Contratos de Partidos Políticos  
**Fuente:** Mexicanos Contra la Corrupción y la Impunidad  
**Última actualización:** mayo 2026

---

## Variables compartidas (ambos datasets)

| # | Variable | Tipo de dato | Valores posibles / Ejemplo | Descripción |
|---|---|---|---|---|
| 1 | `id` | Entero | `1698071028` | Identificador único del contrato. Sirve como llave para cruzar ambos datasets. |
| 2 | `ano` | Entero | `2020`, `2021`, ..., `2025` | Año del periodo de reporte al que corresponde el contrato. |
| 3 | `fecha_inicio_periodo` | Fecha | `2020-01-01` | Fecha de inicio del trimestre o periodo de reporte. |
| 4 | `fecha_fin_periodo` | Fecha | `2020-03-31` | Fecha de fin del trimestre o periodo de reporte. |
| 5 | `tipo_contrato` | Categórica | `Adquisición`, `Prestación de servicio`, `Arrendamiento` | Naturaleza jurídica del contrato. |
| 6 | `tipo_persona` | Categórica | `Física`, `Moral` | Indica si el proveedor es una persona física (individuo) o moral (empresa/organización). |
| 7 | `fisica_nombre` | Texto | `Juan` | Nombre de pila del proveedor cuando es persona física. Puede estar vacío si es persona moral. |
| 8 | `fisica_apellido1` | Texto | `García` | Primer apellido del proveedor (persona física). |
| 9 | `fisica_apellido2` | Texto | `López` | Segundo apellido del proveedor (persona física). |
| 10 | `moral_razon` | Texto | `IQSEC, S.A. DE C.V.` | Razón social del proveedor cuando es persona moral. |
| 11 | `fecha_firma` | Fecha | `2020-10-19` | Fecha en que se firmó el contrato. |
| 12 | `tema` | Categórica | `Prestación`, `Contrato de compraventa` | Categoría temática asignada al contrato. |
| 13 | `descripcion` | Texto libre | `SERVICIO DE LIMPIEZA...` | Descripción del objeto o propósito del contrato. Puede ser muy extensa. |
| 14 | `url` | URL | `https://...pdf` | Enlace al documento PDF oficial del contrato publicado en el portal de transparencia del partido. |
| 15 | `fecha_inicio_vigencia` | Fecha | `2020-10-19` | Fecha en que inicia la vigencia del contrato. |
| 16 | `fecha_fin_vigencia` | Fecha | `2020-12-31` | Fecha en que concluye la vigencia del contrato. |
| 17 | `alcance` | Texto | `Compraventa`, `Prestación` | Alcance o modalidad específica de la contratación. |
| 18 | `costo` | Numérico (MXN) | `262275000.0`, `0.0` | Monto del contrato en pesos mexicanos. Puede ser 0 en contratos abiertos. |
| 19 | `area` | Texto | `Secretaría de Finanzas` | Área interna del partido responsable del contrato. |
| 20 | `fecha_actualizacion` | Fecha | `2020-12-31` | Última fecha en que se actualizó el registro en la base de datos. |
| 21 | `nota` | Texto libre | — | Observaciones o aclaraciones adicionales sobre el registro. |
| 22 | `partido_archivo` | Texto | `Morena`, `Partido Acción Nacional` | Nombre del partido tal como aparece en el archivo fuente original (puede variar en formato). |
| 23 | `ano_archivo` | Numérico | `2020.0` | Año del archivo fuente del que se tomó el registro. |
| 24 | `archivo` | Texto | `bd_bienes_y_servicios_MORENA_2020` | Nombre del archivo fuente original antes de la integración. |
| 25 | `fecha_validacion` | Fecha | `2021-01-10` | Fecha en que MCCI validó el registro. |
| 26 | `nom_fisica` | Texto | `Juan García López` | Nombre completo concatenado de la persona física (para facilitar búsquedas). |
| 27 | `nom_fisica_homo` | Texto | `JUAN GARCIA LOPEZ` | Nombre homologado (sin acentos, mayúsculas) para cruce y deduplicación de registros. |
| 28 | `moral_razon_homo` | Texto | `IQSEC SA DE CV` | Razón social homologada (sin puntuación, mayúsculas) para cruce de registros. |

---

## Variables exclusivas de `contratos_montos.csv`

| # | Variable | Tipo de dato | Valores posibles / Ejemplo | Descripción |
|---|---|---|---|---|
| 29 | `H1` | Entero | `13199`, `13200` | Índice de fila heredado del archivo fuente original. **Variable auxiliar, no usar en análisis**. |
| 30 | `partido` | Categórica | `Morena`, `PAN`, `PRI`, `MC` | Nombre estandarizado del partido político. Esta columna es la principal diferencia con `contratos.csv` y facilita el análisis por partido. |

---

## Notas metodológicas

### ¿Por qué hay menos filas en `contratos_montos.csv`?

`contratos_montos.csv` tiene **618 filas menos** que `contratos.csv`. Las posibles razones son:

1. **Registros sin partido identificable**: Algunos registros en `contratos.csv` no pudieron ser asignados a un partido específico.
2. **Contratos sin monto**: Es posible que se hayan filtrado contratos con `costo == 0` o `costo` vacío.
3. **Depuración de duplicados**: El proceso de homologación pudo haber eliminado registros duplicados.

> 💡 **Recomendación**: Al comparar resultados entre ambos datasets, siempre reporta cuál archivo estás utilizando.

### Calidad de los datos

- La columna `costo` puede contener `0.0` en contratos abiertos donde el monto no se fija al momento de la firma.
- Las columnas de fecha pueden tener valores faltantes (`NA`) en algunos registros.
- Las columnas `fisica_nombre`, `fisica_apellido1`, `fisica_apellido2` estarán vacías cuando `tipo_persona == "Moral"`, y viceversa para `moral_razon`.
- La columna `descripcion` puede contener caracteres especiales y saltos de línea.

---

## Partidos políticos en el dataset

| Partido | Nombre completo |
|---|---|
| `PAN` | Partido Acción Nacional |
| `PRI` | Partido Revolucionario Institucional |
| `PRD` | Partido de la Revolución Democrática |
| `Morena` | Movimiento Regeneración Nacional |
| `MC` | Movimiento Ciudadano |
| `PVEM` | Partido Verde Ecologista de México |
| `PT` | Partido del Trabajo |
| `NA` | Nueva Alianza |
| `PES` | Partido Encuentro Social |
