# Proyecto - Security Data Science

Implementacion del proyecto de `CC3094 - Security Data Science`, alineada con la propuesta de investigacion sobre deteccion de phishing asistido por LLM.

## Objetivo de las entregas

La **Parte 1**, segun [PROYECTO_Implementacion_Parte_1.pdf](docs/PROYECTO_Implementacion_Parte_1.pdf), cubre:

- seleccion o construccion del dataset;
- analisis exploratorio de datos (EDA);
- generacion y seleccion de caracteristicas para el modelo.

La **Parte 2**, segun [PROYECTO - Implementacion - Parte 2.pdf](docs/PROYECTO%20-%20Implementaci%C3%B3n%20-%20Parte%202.pdf), cubre:

- implementacion y refinamiento de modelos;
- evaluacion con Accuracy, Precision, Recall, F1 score y Curva ROC;
- interpretacion de metricas en el contexto del problema.

## Correccion del feedback

La primera implementacion trabajaba principalmente con caracteristicas `URL-only`, lo cual dejaba incompleta la propuesta original porque el phishing tambien depende del texto del correo o mensaje que acompana el enlace.

Para corregirlo, la Parte 2 agrega un dataset textual de correos y compara tres enfoques:

- `URL-only`;
- `texto-only`;
- `URL + texto`.

## Datasets usados

### Parte 1: PhiUSIIL

El notebook de la Parte 1 usa:

- **PhiUSIIL_Phishing_URL_Dataset.csv**

Se eligio **PhiUSIIL Phishing URL (Website)** porque:

- es publico, trazable y reciente;
- contiene la URL cruda y 54 caracteristicas tabulares;
- tiene suficiente volumen para una primera implementacion robusta;
- encaja con la rama de URL descrita en el articulo de investigacion.

### Parte 2: CEAS 2008 email dataset

El notebook de la Parte 2 usa:

- **CEAS_08.csv**

Este dataset complementa PhiUSIIL porque contiene `subject`, `body`, `label` y presencia de URLs dentro del correo. Con eso se pueden extraer caracteristicas de texto y de URL desde la misma fila.

## Estructura del proyecto

```text
PROYECTO/
|-- data/
|   |-- CEAS_08.csv
|   |-- PhiUSIIL_Phishing_URL_Dataset.csv
|   |-- feature_scores_url_only.csv
|   `-- phiusiil_url_only_features.csv
|-- docs/
|   |-- Articulo_Gabriel_Paz.pdf
|   |-- PROYECTO - Implementacion - Parte 2.pdf
|   `-- PROYECTO_Implementacion_Parte_1.pdf
|-- notebooks/
|   |-- 01_implementacion_parte_1_eda_features.ipynb
|   `-- 02_implementacion_parte_2_modelos_texto_url.ipynb
|-- .gitignore
|-- README.md
`-- requirements.txt
```

## Notebooks

[01_implementacion_parte_1_eda_features.ipynb](notebooks/01_implementacion_parte_1_eda_features.ipynb) esta preparado para:

- cargar `PhiUSIIL` desde `data/PhiUSIIL_Phishing_URL_Dataset.csv`;
- realizar EDA sobre la clase objetivo;
- generar features adicionales desde la URL cruda;
- seleccionar un conjunto inicial de variables `URL-only`;
- guardar salidas procesadas dentro de `data/`.

[02_implementacion_parte_2_modelos_texto_url.ipynb](notebooks/02_implementacion_parte_2_modelos_texto_url.ipynb) esta preparado para:

- cargar `CEAS_08.csv`;
- construir texto del correo con asunto y cuerpo;
- extraer URLs del cuerpo y generar caracteristicas numericas;
- entrenar modelos `URL-only`, `texto-only` y `URL + texto`;
- refinar el umbral de decision;
- reportar Accuracy, Precision, Recall, F1 score, ROC AUC, curvas ROC y matriz de confusion.

## Fuentes oficiales

- PhiUSIIL (UCI): https://archive.ics.uci.edu/dataset/967/phiusil-phishing-url-dataset
- CEAS email dataset usado desde GitHub: https://github.com/rokibulroni/Phishing-Email-Dataset
- Phishing Websites (UCI): https://archive.ics.uci.edu/dataset/327/phishing+websites
- PhishTank: https://www.phishtank.org/developer_info.php
- URLhaus: https://urlhaus.abuse.ch/api/

## Como ejecutar

1. Crear un entorno virtual.
2. Instalar dependencias con `pip install -r requirements.txt`.
3. Abrir Jupyter en la raiz del proyecto.
4. Ejecutar los notebooks en orden.

## Resultados esperados

Al ejecutar la Parte 1 se generan archivos procesados dentro de `data/`, incluyendo:

- un dataset con features seleccionadas para el enfoque `URL-only`;
- un ranking inicial de importancia de caracteristicas.

Al ejecutar la Parte 2 se obtiene una comparacion directa entre modelos. En la ejecucion actual, el enfoque `URL-only` queda claramente por debajo de los modelos con texto, lo cual respalda la correccion realizada a partir del feedback.
