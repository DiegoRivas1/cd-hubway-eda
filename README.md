# cd-hubway-eda

Análisis Exploratorio de Datos (Data Wrangling) sobre el dataset **Hubway**, el sistema de bicicletas
compartidas de Boston (2011–2013).

## De qué trata

El trabajo sigue la guía de laboratorio de Data Wrangling paso a paso (Paso 0 a Paso 4) sobre ~1.58
millones de viajes y 142 estaciones de Hubway:

- **Paso 0-1:** entendimiento del dataset, tipos de datos, valores nulos y duplicados. El hallazgo central
  es que los nulos en `birth_date`/`gender` no son aleatorios: el 100% de los usuarios *Casual* nunca los
  reporta, y entre los *Registered* la captura de esos datos cambia de política entre 2011 y 2013.
- **Paso 2:** outliers de duración de viaje, con dos causas distintas (errores de sensor vs. bicicletas
  perdidas/robadas reales).
- **Paso 3:** visualización de patrones de uso de dos picos horarios de *commute* (8am y 17-18h) y fuerte
  estacionalidad (el servicio se detiene en invierno).
- **Paso 4:** se plantea `subsc_type` como problema supervisado y se responde la pregunta tiempo-espacio
  cruzando el uso diario con clima real de Boston (API de Open-Meteo): días fríos o lluviosos tienen
  notoriamente menos viajes que días templados y secos.

## Estructura del repositorio

```
cd-hubway-eda/
├── data/
│   ├── hubway_stations.csv     # 142 estaciones (catálogo)
│   └── hubway_trips.csv        # ~1.58M viajes (NO se sube a git, ver abajo)
├── notebooks/
│   └── eda_hubway.ipynb        # Cuaderno con el EDA completo, ejecutado (Paso 0 a Paso 4)
├── report/
│   ├── informe.tex             # Informe en LaTeX, mismo orden que el cuaderno
│   └── figures/                # Figuras generadas por el notebook, ya referenciadas en informe.tex
└── README.md
```

## Datos

Fuente: [Boston Hubway Data Visualization Challenge Dataset (Kaggle)](https://www.kaggle.com/datasets/codebreaker619/boston-hubway-data-visualization-challenge-dataset/data).

Para reproducir el análisis, descarga `hubway_stations.csv` y `hubway_trips.csv` desde ese enlace y
colócalos en `data/`. `hubway_trips.csv` pesa ~150 MB, por eso no viene incluido en este repositorio de
GitHub (supera el límite de 100 MB por archivo).

## Dataset externo sugerido para el Paso 4 (tiempo-espacio)

Para cruzar el uso diario de Hubway con el clima de Boston (2011–2013):

- [NOAA Climate Data Online (CDO)](https://www.ncdc.noaa.gov/cdo-web/datasets) dataset **GHCN-Daily**,
  estación de Boston Logan Airport (`USW00014739`): temperatura, precipitación, nieve por día.
  Requiere crear un token gratuito para la API en <https://www.ncdc.noaa.gov/cdo-web/webservices/v2#gettingStarted>.
- Alternativa sin registro: [Open-Meteo Historical Weather API](https://open-meteo.com/en/docs/historical-weather-api).

Unir por fecha (`start_dt.dt.date`) contra el clima del día correspondiente.

## Cómo reproducir

```bash
pip install -r requirements.txt
jupyter nbconvert --to notebook --execute --inplace notebooks/eda_hubway.ipynb
```

## Informe

`report/informe.tex` sigue la misma estructura que pide la guía de laboratorio (Paso 0 a Paso 4 +
Conclusión) y referencia las figuras ya generadas en `report/figures/`. Compilar con `pdflatex` o
`latexmk` (requiere el paquete `babel` con soporte de español).
