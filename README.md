# Análisis exploratorio y preparación del dataset TMDB

Trabajo Final Integrador de la materia **Análisis de Datos** de la Carrera de Especialización en Inteligencia Artificial (CEIA) — Facultad de Ingeniería, Universidad de Buenos Aires.

## Objetivo

El trabajo realiza un análisis exploratorio y la preparación del **Full TMDB Movies Dataset 2024** para plantear un problema supervisado de **regresión**, utilizando Vote_average como variable objetivo.

El análisis comprende:

- exploración y comprensión del dataset;
- análisis de valores faltantes y valores extremos;
- definición de la población de estudio;
- feature engineering;
- separación train-test;
- imputación de valores faltantes;
- codificación de variables categóricas y multietiqueta;
- estandarización;
- selección de features mediante Información Mutua y análisis de redundancia;
- reducción de dimensionalidad mediante PCA.

## Dataset

Se utiliza el **Full TMDB Movies Dataset 2024**, con aproximadamente 1,48 millones de películas.

Debido al tamaño del archivo original, el dataset no se incluye en este repositorio.

El archivo utilizado debe descargarse por separado y ubicarse localmente como:

data/TMDB_movie_dataset_v11.csv

## Estructura del repositorio

    ceia-analisis-datos-tmdb/
    ├── notebooks/
    │   └── 01_EDA_TMDB.ipynb
    ├── figures/
    │   ├── dataset_funnel.png
    │   ├── dimensionality_comparison.png
    │   ├── mutual_information.png
    │   └── vote_count_threshold.png
    ├── data/                  # dataset local, excluido mediante .gitignore
    ├── .gitignore
    └── README.md

## Preparación de los datos

Para construir el conjunto destinado al problema de Machine Learning se consideran películas con al menos **10 votos**, buscando un compromiso entre representatividad de ote_average y cantidad de observaciones disponibles.

Luego del proceso de limpieza y preparación se obtienen **78.814 películas**.

Entre las transformaciones realizadas se incluyen:

- tratamiento de valores faltantes;
- transformación logarítmica del presupuesto;
- generación de variables derivadas;
- codificación multi-hot de géneros;
- agrupamiento y one-hot encoding de idiomas;
- estandarización de variables;
- análisis de valores extremos sin eliminación automática.

Todas las transformaciones que requieren estimar parámetros a partir de los datos se ajustan exclusivamente sobre el conjunto de entrenamiento para evitar *data leakage*.

## Selección de features

La relevancia predictiva respecto de ote_average se analiza mediante **Información Mutua**.

La selección final reduce el espacio procesado de **62 a 7 features**:

- untime
- elease_year
- _production_companies
- _genres
- _spoken_languages
- _production_countries
- log_budget


release_decade se descarta por su elevada redundancia con release_year.

## PCA

Como estrategia alternativa de reducción dimensional se aplica **Principal Component Analysis (PCA)** sobre las variables estandarizadas.

Para conservar al menos el 80 % de la varianza se requieren **42 componentes principales**, que explican aproximadamente el **80,78 %** de la varianza total.

Esto permite comparar dos enfoques:

- **Selección de features:** 62 → 7 variables, conservando interpretabilidad.
- **PCA:** 62 → 42 componentes, conservando aproximadamente el 80 % de la varianza.

## Notebook

El análisis completo se encuentra en:


otebooks/01_EDA_TMDB.ipynb

## Autores

Trabajo Final Integrador — Análisis de Datos  
Carrera de Especialización en Inteligencia Artificial — FIUBA
