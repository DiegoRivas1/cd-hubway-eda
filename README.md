# cd-hubway-eda

Análisis Exploratorio de Datos (Data Wrangling) sobre el dataset **Hubway**, el sistema de bicicletas
compartidas de Boston (2011–2013).

Práctica de Laboratorio — Curso *Ciencia de Datos & Big Data*, Maestría en Ciencia de la Computación,
Universidad Nacional de San Agustín de Arequipa. Docente: Ana María Cuadros Valdivia.

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

`hubway_trips.csv` pesa ~150 MB, por encima del límite de 100 MB por archivo de GitHub, así que está
excluido en `.gitignore`. Opciones:

- Usar [Git LFS](https://git-lfs.com/) para versionarlo (`git lfs track "data/*.csv"`).
- Dejarlo fuera del repo y documentar aquí de dónde se descarga (o subirlo a Drive/Kaggle y enlazarlo).

`hubway_stations.csv` (12 KB) sí se puede versionar normalmente.

## Cómo reproducir

```bash
pip install -r requirements.txt
jupyter nbconvert --to notebook --execute --inplace notebooks/eda_hubway.ipynb
```

## Informe

`report/informe.tex` sigue la misma estructura que pide la guía de laboratorio (Paso 0 a Paso 4 +
Conclusión) y referencia las figuras ya generadas en `report/figures/`. Compilar con `pdflatex` o
`latexmk` (requiere el paquete `babel` con soporte de español).
