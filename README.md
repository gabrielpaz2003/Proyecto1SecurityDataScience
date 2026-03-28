# Proyecto - Security Data Science

Implementacion base para la **Parte 1** del proyecto de `CC3094 - Security Data Science`, alineada con la propuesta de investigacion sobre deteccion de phishing asistido por LLM.

## Objetivo de esta entrega

Segun [PROYECTO_Implementacion_Parte_1.pdf](docs/PROYECTO_Implementacion_Parte_1.pdf), esta fase debe cubrir:

- seleccion o construccion del dataset;
- analisis exploratorio de datos (EDA);
- generacion y seleccion de caracteristicas para el modelo.

## Dataset a usar

Para esta entrega el dataset que se va a usar es:

- **PhiUSIIL_Phishing_URL_Dataset.csv**

Esta es la unica data que necesita el notebook principal. La deje directamente dentro de `data/` para que correrlo en Colab o en Jupyter sea mas simple.

Se eligio **PhiUSIIL Phishing URL (Website)** porque:

- es publico, trazable y reciente;
- contiene la URL cruda y 54 caracteristicas tabulares;
- tiene suficiente volumen para una primera implementacion robusta;
- encaja con la rama de URL descrita en el articulo de investigacion.

## Estructura del proyecto

```text
PROYECTO/
|-- data/
|   `-- PhiUSIIL_Phishing_URL_Dataset.csv
|-- docs/
|   |-- Articulo_Gabriel_Paz.pdf
|   `-- PROYECTO_Implementacion_Parte_1.pdf
|-- notebooks/
|   `-- 01_implementacion_parte_1_eda_features.ipynb
|-- .gitignore
|-- README.md
`-- requirements.txt
```

## Notebook principal

El notebook [01_implementacion_parte_1_eda_features.ipynb](notebooks/01_implementacion_parte_1_eda_features.ipynb) esta preparado para:

- cargar `PhiUSIIL` desde `data/PhiUSIIL_Phishing_URL_Dataset.csv`;
- realizar EDA sobre la clase objetivo;
- generar features adicionales desde la URL cruda;
- seleccionar un conjunto inicial de variables `URL-only`;
- guardar salidas procesadas dentro de `data/`.

## Fuentes oficiales

- PhiUSIIL (UCI): https://archive.ics.uci.edu/dataset/967/phiusil-phishing-url-dataset
- Phishing Websites (UCI): https://archive.ics.uci.edu/dataset/327/phishing+websites
- PhishTank: https://www.phishtank.org/developer_info.php
- URLhaus: https://urlhaus.abuse.ch/api/

## Como ejecutar

1. Crear un entorno virtual.
2. Instalar dependencias con `pip install -r requirements.txt`.
3. Abrir Jupyter en la raiz del proyecto.
4. Ejecutar el notebook en orden.

## Resultados esperados de la Parte 1

Al ejecutar el notebook se generan archivos procesados dentro de `data/`, incluyendo:

- un dataset con features seleccionadas para el enfoque `URL-only`;
- un ranking inicial de importancia de caracteristicas.
