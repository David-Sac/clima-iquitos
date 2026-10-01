# Índice de calor en Iquitos (2000-2024)


![Estado](https://img.shields.io/badge/Estado-En%20progreso-yellow?style=flat-square)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat-square&logo=pandas&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=flat-square&logo=jupyter&logoColor=white)

Análisis de 23 años de observaciones horarias de la estación meteorológica del aeropuerto de Iquitos para identificar cuándo el calor es más intenso y anticipar la demanda de servicios de climatización.


## 🎯 Pregunta de negocio
 
¿En qué meses y horas el calor en Iquitos es más intenso, y cómo puede un negocio de aire acondicionado usar esa información para planificar stock, personal técnico y campañas de mantenimiento?

Se usa el **índice de calor** en lugar de la temperatura, porque combina temperatura y humedad y refleja mejor la sensación térmica en una ciudad amazónica.

## 📊 Resultados principales
 
> 🚧 En construcción. Esta sección se completará al terminar el análisis.
 
<!-- Aquí irán 3 o 4 hallazgos con números concretos y el gráfico principal:
![Heatmap del índice de calor](images/heatmap_indice_calor.png) -->
 
## 💡 Recomendaciones
 
> 🚧 En construcción.
 
## 🗂️ Datos
 
| | |
|---|---|
| **Fuente** | [NOAA NCEI – Global Hourly (ISD)](https://www.ncei.noaa.gov/products/land-based-station/integrated-surface-database) |
| **Estación** | Aeropuerto Internacional Crnl. FAP Francisco Secada Vignetta |
| **Códigos** | ICAO: SPQT · ID NOAA: 84377099999 |
| **Periodo descargado** | 2000 – agosto de 2025 |
| **Periodo analizado** | 2000–2024 (23 años) |
| **Variables** | Temperatura y punto de rocío, observaciones horarias |
 
Es la única estación de la NOAA en un radio de unos 100 km alrededor de Iquitos.
 
## 🧹 Metodología
 
1. **Búsqueda de la estación** en el catálogo de la NOAA por su código ICAO.
2. **Descarga automatizada** de un archivo por año.
3. **Decodificación** de los valores de la NOAA: vienen multiplicados por 10 y acompañados de un código de calidad (por ejemplo, `+0275,1` equivale a 27.5 °C con calidad aceptada).
4. **Limpieza:** los faltantes (`+9999`) y los valores con códigos de calidad sospechosos o erróneos se marcan como vacíos.
5. **Conversión de zona horaria** de UTC a hora de Lima (UTC−5).
6. **Evaluación de cobertura:** porcentaje de horas de cada año con temperatura y punto de rocío válidos, considerando años bisiestos.
7. **Selección del periodo:** se incluyen solo los años con al menos 90% de cobertura.
### Años excluidos
 
| Año | Cobertura | Motivo |
|---|---|---|
| 2001 | 87.9% | Faltantes concentrados entre mayo y julio |
| 2020 | 80.1% | Probable reducción de reportes durante la pandemia |
| 2025 | 63.6% | Año incompleto (datos hasta el 24 de agosto) |
 
## ⚠️ Limitaciones
 
- La estación está en el aeropuerto, a unos 7 km del centro de la ciudad, por lo que puede no reflejar el efecto de isla de calor urbana.
- Los años analizados no son consecutivos (se excluyen 2001 y 2020). No afecta al análisis, que es un perfil por mes y hora y no una tendencia en el tiempo.
## 📁 Estructura del proyecto
 
```
clima-iquitos/
├── data/
│   ├── raw/           # Datos originales de la NOAA (no se modifican)
│   └── processed/     # Datos limpios
├── images/            # Gráficos del análisis
├── notebooks/
│   └── 01_exploracion.ipynb   # Descarga, limpieza y evaluación de cobertura
├── requirements.txt
└── README.md
```
 
## ▶️ Cómo reproducirlo
 
```bash
git clone https://github.com/David-Sac/clima-iquitos.git
cd clima-iquitos
python -m venv .venv
.venv\Scripts\activate          # En Windows
pip install -r requirements.txt
```
 
Luego abre `notebooks/01_exploracion.ipynb` y ejecuta todas las celdas. El notebook descarga los datos directamente de la NOAA.
 
## 👤 Autor
 
**David Saccsara** · Data Analyst en formación · Maestría en Ciencia de Datos e IA (UTP)
 
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/davidsacc/)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/David-Sac)
 