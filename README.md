# Percepción de inseguridad y denuncia en el AMG

Proyecto de análisis descriptivo sobre percepción de inseguridad, victimización, denuncia y confianza en la policía en municipios del Área Metropolitana de Guadalajara (AMG), con énfasis en Zapopan, la comparación principal utiliza las tablas cruzadas de las encuestas de Jalisco Cómo Vamos (JCV) de 2022 y 2024 y también se incluyen algunas referencias externas para dar contexto; no son necesariamente comparables entre sí.

## Contenido del repositorio

```text
.
├── datos/
│   ├── crudos/         # CSV originales de JCV para 2022 y 2024
│   └── procesados/     # Tablas CSV que genera el notebook
├── docs/
│   ├── figuras/        # Figuras 01–08 en PDF y PNG
│   ├── main.tex        # Fuente LaTeX del artículo
│   └── PERCEPCION DE INSEGURIDAD Y NO DENUCIA DEL DELITO.pdf
│                       # Copia de un artículo compilado
├── notebooks/
│   └── analisis_percepcion.ipynb
└── README.md
```

## Análisis

El notebook [analisis_percepcion.ipynb](./notebooks/analisis_percepcion.ipynb) carga los CSV crudos, los transforma a formato tabular ordenado y genera comparaciones de:

- Percepción de inseguridad por municipio, sexo y edad.
- Víctimas que declararon no denunciar y motivos para no hacerlo.
- Confianza en la policía.
- Referencias contextuales JCV–ENSU y percepción–tasa de carpetas en Zapopan.
- Causas institucionales de no denuncia con referencias externas de ENVIPE.

El notebook incluye también un resumen de hallazgos y propuestas de política pública y de investigación futura.

## Datos y fuentes

### Datos guardados en el repositorio

- `datos/crudos/`: tablas cruzadas de la VIII encuesta de JCV (2022) y la IX encuesta de JCV (2024). Son las entradas del análisis principal.
- `datos/procesados/`: salidas CSV del notebook, incluidos los datos limpios y las tablas de percepción, cifra negra (indicador parcial de no denuncia), comparación de tres métricas, resultados por sexo y edad, y referencia JCV–ENSU.

### Fuentes externas citadas o usadas como contexto

- [Jalisco Cómo Vamos: datos abiertos](https://jaliscocomovamos.org/datos-abiertos/) — encuestas de calidad de vida de 2022 y 2024.
- [IIEG: ENSU](https://iieg.gob.mx/ns/?page_id=25306) — referencia externa de percepción de inseguridad.
- [INEGI: ENVIPE](https://www.inegi.org.mx/programas/envipe/) — contexto de cifra negra y motivos de no denuncia.
- [SESNSP: datos abiertos de incidencia delictiva](https://www.gob.mx/sesnsp/acciones-y-programas/datos-abiertos-de-incidencia-delictiva) — fuente administrativa de carpetas de investigación. La comparación de Zapopan incluida en el proyecto se consultó vía [MunicipioData](https://municipiodata.com/).

La Figura 7 compara percepción de JCV con una tasa administrativa por cada 100 mil habitantes: son indicadores con unidades y procesos de registro distintos. La Figura 8 combina referencias de distintos años (ENVIPE 2023 y una referencia de Jalisco 2021); sus porcentajes no forman una serie homogénea. Se recomienda consultar las fuentes originales antes de reutilizar estas cifras.

## Requisitos

- Python 3 con Jupyter.
- Paquetes de Python: `pandas`, `numpy`, `matplotlib` y `seaborn`.
- Para compilar el artículo: una distribución de LaTeX, como TeX Live o MiKTeX, con los paquetes utilizados en `docs/main.tex` (entre ellos `geometry`, `babel`, `newtx`, `graphicx`, `booktabs`, `caption`, `titlesec`, `enumitem`, `amsmath`, `hyperref` y `xcolor`).

Instala los paquetes de Python en el entorno del kernel si no están disponibles:

```bash
python -m pip install pandas numpy matplotlib seaborn jupyter
```

## Cómo reproducir el análisis

1. Abre `notebooks/analisis_percepcion.ipynb` en Jupyter o VS Code y selecciona un kernel de Python que tenga los paquetes requeridos.
2. Ejecuta las celdas en orden, de arriba hacia abajo. El notebook usa rutas relativas como `../datos/crudos/` y `../docs/figuras/`, por lo que su directorio de trabajo debe ser `notebooks/`. Si inicias Jupyter desde una terminal, hazlo así desde la raíz del proyecto:

   ```bash
   cd notebooks
   jupyter lab analisis_percepcion.ipynb
   ```

   En VS Code, configura el directorio de trabajo del notebook como `notebooks/` si tu kernel inicia desde otra carpeta.
3. La sección de exportación guarda las tablas CSV en `datos/procesados/`.
4. La última celda crea o actualiza las ocho figuras en `docs/figuras/`, en formatos PDF y PNG (300 dpi). Si ejecutas solo una parte del notebook, asegúrate de haber ejecutado primero las celdas que definen y calculan sus datos.

## Artículo y compilación

El artículo está escrito en [docs/main.tex](./docs/main.tex). Las figuras se leen desde `docs/figuras/`. El PDF que ya está en `docs/` es una copia compilada; para actualizarlo después de editar el `.tex` o regenerar las figuras, compila desde el directorio `docs/`:

```bash
cd docs
pdflatex -interaction=nonstopmode -halt-on-error main.tex
pdflatex -interaction=nonstopmode -halt-on-error main.tex
```

La segunda compilación actualiza las referencias cruzadas. El resultado habitual es `docs/main.pdf`; puedes renombrarlo después de confirmar que la compilación terminó sin errores.

## Figuras exportadas

Las versiones PDF (vectoriales) y PNG de cada figura están en `docs/figuras/`:

| Archivo base | Contenido |
|---|---|
| `fig01_percepcion_por_municipio` | Percepción de inseguridad por municipio, 2022 y 2024. |
| `fig02_confianza_policia` | Distribución de confianza en la policía: Zapopan y AMG. |
| `fig03_heatmap_3metricas` | Percepción, no denuncia y confianza policial. |
| `fig04_brechas_sexo_edad` | Percepción por sexo y grupo de edad. |
| `fig05_razones_no_denuncia` | Motivos homologados para comparar 2022 y 2024. |
| `fig06_jcv_vs_ensu` | Referencia contextual entre JCV y ENSU; instrumentos distintos. |
| `fig07_percepcion_vs_carpetas_zapopan` | Percepción JCV y tasa de carpetas en Zapopan. |
| `fig08_causas_no_denuncia` | Motivos institucionales de no denuncia con referencias externas. |

## Alcance e interpretación

Los resultados principales son descriptivos y se calculan con tablas agregadas. El indicador de personas víctimas que no denunciaron es parcial y no equivale por sí solo a la cifra negra completa de INEGI. Con estos tabulados no se pueden estimar de forma individual intervalos de confianza, significancia estadística, efectos causales ni un modelo de decisión de denunciar. ENSU, ENVIPE y los registros de carpetas tienen periodos, unidades y metodologías diferentes; las comparaciones del proyecto se presentan como contexto, no como una misma serie.
