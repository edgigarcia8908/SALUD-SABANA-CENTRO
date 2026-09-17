# Diagnóstico en Salud Pública Provincial — Sabana Centro (Asocentro)

Este repositorio contiene la información de diagnóstico en salud pública de los 11 municipios
de la provincia de Sabana Centro (Cundinamarca), recolectada durante 2024-2025 por
**Asocentro** (Asociación de Municipios de Sabana Centro) como insumo para el
**Bootcamp de Asocentro**, cuyo objetivo es explorar formas de digitalizar y facilitar el
diligenciamiento de esta información (hoy recogida en matrices de Excel).

Municipios incluidos: Cajicá, Chía, Cogua, Cota, Gachancipá, Nemocón, Sopó, Tabio, Tenjo,
Tocancipá y Zipaquirá.

## Punto de partida obligatorio

Antes de tocar cualquier archivo, lee **[`instructivo_dx_provincial.pdf`](instructivo_dx_provincial.pdf)**.
Es el instructivo oficial elaborado por la Secretaría de Salud de Cajicá y la Universidad de
La Sabana; explica el propósito de cada formato y cómo se diligencia. Este README resume ese
documento para dar contexto rápido, pero el PDF es la fuente autorizada.

> ⚠️ Los formatos originales tienen una regla explícita: **no se deben agregar ni quitar filas
> ni columnas**, porque los archivos de la carpeta general consolidan una hoja por municipio.
> Cualquier herramienta o app que el bootcamp construya para reemplazar estas matrices debe
> respetar (o migrar deliberadamente) esa misma estructura de datos.

## Estructura del repositorio

```
├── 01_indicadores_salud_publica.xlsx      # 1 libro, 1 hoja por municipio + CONSOLIDADO
├── 02_resumen_gaudi_2024.xlsx             # 1 libro, 1 hoja por municipio
├── 03_adherencia_resolucion_3280.xlsx     # 1 libro, 1 hoja por municipio + CONSOLIDADO
├── 04_siau_2024_2025.xlsx                 # 1 libro, 1 hoja por municipio
├── instructivo_dx_provincial.pdf          # Instructivo oficial de diligenciamiento
└── <municipio>/                           # cajica/ chia/ cogua/ cota/ gachancipa/
    ├── 05_plan_cuidados_comunitario.xlsx  #   nemocon/ sopo/ tabio/ tenjo/
    ├── 06_matriz_priorizacion.xlsx        #   tocancipa/ zipaquira/
    └── 07_riss_2025.xlsx
```

Los nombres de archivos y carpetas fueron normalizados (minúsculas, sin tildes ni espacios,
con prefijo numérico) respecto a como llegaron originalmente, para que se puedan clonar y leer
sin problemas en Windows/Mac/Linux y desde Python/R (pandas, openpyxl, etc.).

### Los 7 formatos

| # | Archivo | Ámbito | ¿Qué mide? |
|---|---------|--------|------------|
| 1 | `01_indicadores_salud_publica.xlsx` | Provincial (carpeta general) | Indicadores demográficos y epidemiológicos por municipio. |
| 2 | `02_resumen_gaudi_2024.xlsx` | Provincial (carpeta general) | Evaluación GAUDÍ del aseguramiento y la prestación de servicios por EAPB/EPS (cumple / no cumple + hallazgo), vigencia 2024. |
| 3 | `03_adherencia_resolucion_3280.xlsx` | Provincial (carpeta general) | Medición de adherencia a las Rutas Integrales de Atención en Salud (RIAS) de la Resolución 3280/2018, por prestador. |
| 4 | `04_siau_2024_2025.xlsx` | Provincial (carpeta general) | Consolidado mensual de PQRSDF (peticiones, quejas, reclamos, sugerencias, denuncias, felicitaciones) por EAPB/IPS, 2024-2025. |
| 5 | `<municipio>/05_plan_cuidados_comunitario.xlsx` | Por municipio | Plan de cuidados comunitario: necesidades sentidas en salud, causas, estrategias (ciclo PHVA) y responsables. |
| 6 | `<municipio>/06_matriz_priorizacion.xlsx` | Por municipio | Matriz de priorización de necesidades en salud pública (criterios ponderados: impacto/urgencia, factibilidad, costo-efectividad, alineación, equidad). |
| 7 | `<municipio>/07_riss_2025.xlsx` | Por municipio | Autoevaluación de Redes Integradas de Servicios de Salud (RISS), aporte de la Universidad de La Sabana. |

## Archivos "borrador" (no eliminados, pero no son la fuente canónica)

Algunos municipios subieron versiones de trabajo adicionales que ya están representadas como
hoja dentro de los archivos consolidados de la carpeta general. Se dejaron en su lugar (con
sufijo `_BORRADOR`) para no perder historial, pero **no deben usarse como fuente de verdad**:

- `cogua/encuesta_asocentro_analisis_atencion_2025_BORRADOR.xlsx` — versión suelta de la
  encuesta GAUDÍ de Cogua; el dato vigente está en la hoja `COGUA` de `02_resumen_gaudi_2024.xlsx`.
- `zipaquira/01_indicadores_salud_publica_21072025_BORRADOR.xlsx`,
  `zipaquira/02_resumen_gaudi_2024_BORRADOR.xlsx`,
  `zipaquira/04_siau_2024_2025_BORRADOR.xlsx` — copias de trabajo de Zipaquirá de los
  formatos 1, 2 y 4; el dato vigente está en la hoja `ZIPAQUIRA` de cada archivo consolidado
  de la raíz. **Antes de usarlas, vale la pena comparar celda a celda contra la hoja
  consolidada**, por si Zipaquirá actualizó algo aquí que no se trasladó al consolidado.

## Sobre datos sensibles

Se revisó el contenido completo de los 41 archivos antes de publicar este repositorio.
**No se encontraron registros individuales de pacientes** (sin nombres, cédulas, direcciones
ni diagnósticos de personas identificables). Toda la información es agregada o institucional:
conteos de PQRSDF por EPS, cumplimiento normativo por prestador, indicadores demográficos
poblacionales, planes de acción territoriales, etc.

Lo único de tipo personal que aparece es el **nombre y correo institucional del funcionario
público responsable de diligenciar cada formato** (p. ej. "Responsable de la información:
Fulano de Tal — correo@municipio-cundinamarca.gov.co"), y en algunas plantillas hay columnas
para el nombre/celular/correo de quienes elaboran el Plan de Cuidados Comunitario. Es
información de contacto profesional de servidores públicos en ejercicio de su cargo, no datos
de pacientes ni de ciudadanos particulares. Aun así, si el equipo de Asocentro prefiere no
exponerla en un repositorio público, esas celdas puntuales se pueden anonimizar antes de
publicar (decisión de Asocentro, no un requisito técnico).

## Ideas para el equipo del bootcamp

- **Modelo de datos**: usar la tabla de "Los 7 formatos" de arriba como punto de partida para
  diseñar un esquema relacional (o de documentos) que reemplace las 3 hojas de "instrucciones"
  y la hoja de datos por formato.
- **Migración**: escribir un script (Python + `openpyxl`/`pandas`) que vuelque cada hoja
  municipal de estos 41 archivos a un formato tabular limpio (CSV/DB), como base para un MVP
  de captura vía formulario web en vez de Excel.
- **Validaciones**: varios formatos ya traen reglas implícitas (listas desplegables,
  porcentajes que deben sumar 100, "no agregar filas/columnas"); son buen material para
  convertir en validaciones de un formulario.
- **Zipaquirá/Cogua**: antes de dar por buena la migración, reconciliar los archivos
  `_BORRADOR` contra los consolidados (ver sección anterior).

## Créditos

Instructivo y formatos consolidados por la Secretaría de Salud del Municipio de Cajicá
(Sandra Liliana Corredor Espinel, Alba Milena Tovar López, Laura Daniela Garzón Zambrano),
con aportes de la Universidad de La Sabana, Tabio y Tenjo. Ver
`instructivo_dx_provincial.pdf` para el detalle completo de autoría.
