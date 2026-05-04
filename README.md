# Proyecto - Security Data Science

Implementacion del proyecto de `CC3094 - Security Data Science` enfocada en deteccion de phishing a partir de dos fuentes de senales:

- caracteristicas de URL;
- contenido textual del correo.

La idea central del repositorio es mostrar la evolucion del proyecto en dos entregas. La Parte 1 construye una linea base `URL-only`; la Parte 2 corrige esa limitacion e incorpora texto para comparar modelos `URL-only`, `texto-only` y `URL + texto`.

## Resumen del proyecto

- **Parte 1:** seleccion de dataset, EDA y generacion de features.
- **Parte 2:** entrenamiento, refinamiento y evaluacion de modelos.
- **Pregunta que guia la implementacion:** que tanto mejora la deteccion de phishing cuando el modelo ve no solo la URL, sino tambien el mensaje que intenta persuadir al usuario.

## Resultado principal

La conclusion de la Parte 2 es consistente: los modelos que usan texto superan con mucha diferencia al enfoque `URL-only`.

| Modelo | Accuracy | Precision | Recall | F1 | ROC AUC |
| --- | ---: | ---: | ---: | ---: | ---: |
| `Texto-only` | 0.9935 | 0.9945 | 0.9938 | 0.9941 | 0.9995 |
| `URL + texto` | 0.9932 | 0.9942 | 0.9935 | 0.9939 | 0.9991 |
| `URL + texto refinado` | 0.9909 | 0.9892 | 0.9945 | 0.9918 | 0.9991 |
| `URL-only` | 0.7067 | 0.7964 | 0.6351 | 0.7066 | 0.7875 |

Esto respalda el punto principal del feedback recibido: modelar solo la URL deja fuera una parte importante del comportamiento del phishing, porque el ataque tambien depende del texto del correo o mensaje.

## Objetivos por entrega

### Parte 1

Segun [PROYECTO_Implementacion_Parte_1.pdf](docs/PROYECTO_Implementacion_Parte_1.pdf), esta fase cubre:

- seleccion o construccion del dataset;
- analisis exploratorio de datos;
- generacion y seleccion de caracteristicas iniciales.

### Parte 2

Segun [PROYECTO - Implementacion - Parte 2.pdf](docs/PROYECTO%20-%20Implementaci%C3%B3n%20-%20Parte%202.pdf), esta fase cubre:

- implementacion y refinamiento de modelos;
- evaluacion con Accuracy, Precision, Recall, F1 score y ROC AUC;
- interpretacion de metricas en el contexto del problema.

## Datasets usados

### 1. PhiUSIIL Phishing URL Dataset

Archivo local:

- `data/PhiUSIIL_Phishing_URL_Dataset.csv`

Se usa en la Parte 1 para construir la base `URL-only`. Fue elegido porque:

- es publico y trazable;
- incluye la URL cruda y decenas de atributos tabulares;
- permite hacer EDA y seleccion de features con una base suficientemente grande.

### 2. CEAS 2008 Email Dataset

Archivo local:

- `data/CEAS_08.csv`

Se usa en la Parte 2 porque cada fila contiene informacion textual del correo junto con la etiqueta. Eso permite:

- construir features de texto desde `subject` y `body`;
- extraer URLs visibles desde el contenido del correo;
- comparar directamente modelos `URL-only`, `texto-only` y `URL + texto`.

El notebook de la Parte 2 tambien puede volver a descargar este archivo desde GitHub si no existe localmente.

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

### `01_implementacion_parte_1_eda_features.ipynb`

Incluye:

- carga del dataset `PhiUSIIL`;
- EDA de la variable objetivo;
- exploracion de correlaciones y relevancia de variables;
- generacion de features adicionales desde la URL cruda;
- seleccion de un conjunto inicial de variables `URL-only`.

Salidas esperadas:

- `data/phiusiil_url_only_features.csv`
- `data/feature_scores_url_only.csv`

### `02_implementacion_parte_2_modelos_texto_url.ipynb`

Incluye:

- carga de `CEAS_08.csv`;
- limpieza y composicion del texto del correo;
- extraccion de URLs y generacion de features numericas;
- vectorizacion TF-IDF para el contenido textual;
- entrenamiento de modelos logisticos comparables;
- refinamiento del umbral de decision;
- evaluacion con metricas y visualizaciones.

Modelos comparados:

- `URL-only`
- `Texto-only`
- `URL + texto`

## Como ejecutar

### 1. Crear entorno virtual

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
```

### 2. Instalar dependencias

```powershell
pip install -r requirements.txt
```

### 3. Abrir Jupyter

```powershell
jupyter notebook
```

### 4. Ejecutar en orden

1. `notebooks/01_implementacion_parte_1_eda_features.ipynb`
2. `notebooks/02_implementacion_parte_2_modelos_texto_url.ipynb`

## Dependencias

El proyecto usa las siguientes librerias principales:

- `jupyter`
- `matplotlib`
- `numpy`
- `pandas`
- `scikit-learn`
- `seaborn`

## Interpretacion de resultados

- Si `URL-only` queda por debajo de `texto-only`, entonces la URL aislada no captura todo el comportamiento del phishing.
- Si `URL + texto` iguala o mejora al modelo textual, entonces las senales de URL siguen siendo utiles como complemento.
- En este proyecto, el principal hallazgo es que el texto del correo aporta casi toda la mejora discriminativa frente a la base `URL-only`.
- El modelo fusionado sigue siendo valioso porque representa mejor el escenario real: el usuario recibe un mensaje junto con un enlace, no una URL en el vacio.

## Fuentes

- PhiUSIIL (UCI): https://archive.ics.uci.edu/dataset/967/phiusil-phishing-url-dataset
- CEAS email dataset usado desde GitHub: https://github.com/rokibulroni/Phishing-Email-Dataset
- Phishing Websites (UCI): https://archive.ics.uci.edu/dataset/327/phishing+websites
- PhishTank: https://www.phishtank.org/developer_info.php
- URLhaus: https://urlhaus.abuse.ch/api/
