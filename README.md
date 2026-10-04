# 🌡️ Índice de calor en Iquitos (2000–2024): ¿cuándo es más peligroso el calor?

![Estado](https://img.shields.io/badge/Estado-Completado-brightgreen?style=flat-square)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat-square&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=flat-square&logo=numpy&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557C?style=flat-square&logo=python&logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-4C72B0?style=flat-square&logo=python&logoColor=white)

Análisis de 23 años de observaciones horarias de la estación meteorológica del aeropuerto de Iquitos para identificar en qué meses y horas el calor alcanza niveles de riesgo, y cómo pueden usar esa información sectores como salud, educación, trabajo, energía y comercio.

![Heatmap del índice de calor](images/heatmap_indice_calor.png)

## 🎯 Pregunta de análisis

¿En qué meses y horas el calor en Iquitos alcanza niveles de riesgo para las personas, y cómo pueden distintos sectores usar esa información para planificar sus actividades?

Se usa el **índice de calor** en lugar de la temperatura, porque combina temperatura y humedad y refleja mejor la sensación térmica en una ciudad amazónica donde la humedad relativa mediana es de **88.7%**.

## 📊 Resultados principales

1. **El calor intenso está presente casi todo el año.** Incluso en el mes más fresco hay más de **4 horas diarias** con índice de calor en *precaución extrema* (≥ 32 °C).
2. **El pico ocurre de setiembre a noviembre**, entre las 12:00 y las 15:00. Setiembre (**6.9 h/día**) y octubre (**6.8 h/día**) son los meses más críticos.
3. **Junio y julio son la única temporada más fresca**, con 4.4 y 4.5 horas diarias de precaución extrema.
4. **La humedad eleva la sensación térmica hasta 4.5 °C** por encima de la temperatura real, con la mayor diferencia a las 13:00.
5. **Hay 1,543 horas en categoría de *peligro* (≥ 41 °C)**, el 0.78% del total. Más de la mitad (**54.5%**) ocurre de setiembre a noviembre, mientras que junio y julio suman solo 35 horas.

### El día típico en Iquitos

![Perfil horario](images/perfil_horario.png)

El índice de calor alcanza su máximo alrededor de las 14:00. De madrugada, aunque la humedad está cerca del 95%, ambas curvas casi se juntan: la humedad solo intensifica la sensación de calor cuando la temperatura ya es alta.

### Horas de precaución extrema por mes

![Horas de calor extremo](images/horas_calor_extremo.png)

Agosto es el primer mes que supera claramente el promedio anual de 5.7 h/día: marca el inicio de la temporada de mayor calor.

## 💡 Implicaciones por sector

Los resultados describen cuándo el calor es más intenso. Estas son posibles aplicaciones para distintos sectores en Iquitos:

| Sector | Qué hacer | Cuándo |
|---|---|---|
| 🏥 **Salud pública** | Reforzar campañas de hidratación y prevención del golpe de calor, con atención a adultos mayores, niños y personas con enfermedades crónicas | Setiembre–noviembre, especialmente de 12:00 a 15:00 |
| 👷 **Trabajo al aire libre** | Programar las tareas físicas más pesadas (construcción, carga, reparto) antes de las 10:00 o después de las 16:00, con pausas e hidratación en las horas centrales | Todo el año; con más rigor de agosto a noviembre |
| 🏫 **Educación** | Evitar educación física y actividades al aire libre en las horas de mayor calor | 12:00–15:00, sobre todo de setiembre a noviembre |
| ⚡ **Energía** | Anticipar picos de consumo eléctrico por ventiladores y aire acondicionado, y programar el mantenimiento de la infraestructura en la temporada fresca | Picos: tardes de setiembre a noviembre · Mantenimiento: junio–julio |
| 🛒 **Comercio y climatización** | Asegurar stock de ventiladores, equipos de aire acondicionado y bebidas antes del alza, considerando los tiempos de llegada de mercadería a Iquitos por vía fluvial o aérea | Abastecerse antes de agosto |
| 🎉 **Turismo y eventos** | Programar actividades al aire libre por la mañana o al final de la tarde, y aprovechar la temporada más fresca para eventos masivos | Junio–julio es la temporada más favorable |

## 🗂️ Datos

| | |
|---|---|
| **Fuente** | [NOAA NCEI – Global Hourly (ISD)](https://www.ncei.noaa.gov/products/land-based-station/integrated-surface-database) |
| **Estación** | Aeropuerto Internacional Crnl. FAP Francisco Secada Vignetta |
| **Códigos** | ICAO: SPQT · ID NOAA: 84377099999 |
| **Periodo descargado** | 2000 – agosto de 2025 |
| **Periodo analizado** | 2000–2024 (23 años, 197,457 horas) |
| **Variables** | Temperatura y punto de rocío, observaciones horarias |

Es la única estación de la NOAA en un radio de unos 100 km alrededor de Iquitos.

## 🧹 Metodología

**Limpieza** (`01_exploracion.ipynb`)

1. Búsqueda de la estación en el catálogo de la NOAA por su código ICAO.
2. Descarga automatizada de un archivo por año.
3. Decodificación de los valores de la NOAA: vienen multiplicados por 10 y con un código de calidad (`+0275,1` equivale a 27.5 °C con calidad aceptada).
4. Eliminación de faltantes (`+9999`) y de valores con códigos de calidad sospechosos o erróneos.
5. Conversión de UTC a hora de Lima (UTC−5).
6. Evaluación de cobertura por año, considerando solo horas con temperatura y punto de rocío válidos y años bisiestos. Se incluyen los años con al menos 90% de cobertura.
7. Agregación a una fila por hora, para que los años con más reportes por hora no pesen más en los promedios.

**Variables y valores atípicos** (`02_analisis.ipynb`)

8. Cálculo de la **humedad relativa** a partir del punto de rocío con la fórmula de Magnus.
9. Cálculo del **índice de calor** con el algoritmo del Servicio Meteorológico Nacional de EE. UU. (NWS), incluido su ajuste para humedad alta.
10. Detección de **picos aislados**: valores que saltan más de 5 °C respecto a la hora anterior y a la siguiente, en la misma dirección. El umbral se eligió con un análisis de sensibilidad (3 °C marcaba 111 picos; 6 °C, solo 6). Se eliminaron 14 horas (0.007%), entre ellas un probable error de digitación de 33 °C a las 3:00 a. m.

**Visualización** (`03_visualizacion.ipynb`)

11. Perfil horario, heatmap de mes por hora, y horas de *precaución extrema* y *peligro* por mes según las categorías de índice de calor del NWS.

### Años excluidos

| Año | Cobertura | Motivo |
|---|---|---|
| 2001 | 87.9% | Faltantes de temperatura y punto de rocío concentrados entre mayo y julio |
| 2020 | 80.1% | Horas sin reporte en junio, setiembre y octubre, probablemente por la reducción de operaciones durante la pandemia |
| 2025 | 63.6% | Año incompleto (datos hasta el 24 de agosto) |

## ⚠️ Limitaciones

- **El análisis muestra cuándo hace más calor, no sus efectos.** Las implicaciones por sector son aplicaciones de los resultados, no impactos medidos. Validarlas requeriría cruzar estos datos con información de cada sector, como atenciones médicas o consumo eléctrico.
- La estación está en el aeropuerto, a unos 7 km del centro de la ciudad, por lo que puede no reflejar el efecto de isla de calor urbana.
- Algunas horas de 2022–2024 registran puntos de rocío de 28–29 °C, inusualmente altos. Se conservaron porque aparecen agrupados en días consecutivos y en horas lógicas, lo que sugiere un evento real y no un error.
- La detección de picos compara cada hora con la fila vecina; si falta una hora, la comparación se hace con un registro más distante.
- Los años analizados no son consecutivos. No afecta a los resultados, que son un perfil por mes y hora y no una tendencia en el tiempo.

## 📁 Estructura del proyecto

```
clima-iquitos/
├── data/
│   ├── raw/
│   │   └── iquitos_spqt_2000_2025.csv   # Datos originales de la NOAA
│   └── processed/
│       ├── iquitos_horario.csv          # Una fila por hora, datos validados
│       └── iquitos_indice_calor.csv     # Con humedad e índice de calor
├── images/                              # Gráficos del análisis
├── notebooks/
│   ├── 01_exploracion.ipynb             # Descarga, limpieza y cobertura
│   ├── 02_analisis.ipynb                # Humedad, índice de calor y picos
│   └── 03_visualizacion.ipynb           # Gráficos y conclusiones
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

Luego ejecuta los notebooks en orden: `01`, `02` y `03`. El primero descarga los datos directamente de la NOAA.

## 🔭 Próximos pasos

- Cruzar el índice de calor con datos de salud (atenciones por golpe de calor o deshidratación) o de consumo eléctrico, para medir su impacto real.
- Analizar si el índice de calor en Iquitos ha aumentado en las últimas décadas: las horas más calurosas del registro son de 2022 a 2024.
- Comparar los datos de esta estación con los de la estación San Roque del SENAMHI, ubicada dentro de la ciudad.

## 👤 Autor

**David Saccsara** · Data Analyst en formación · Maestría en Ciencia de Datos e IA (UTP, en curso)

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/davidsacc/)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/David-Sac)