# PI_Mineria_Datos_1

**Proyecto Integrador - Minería de Datos 1**

Análisis exploratorio de usuarios de una plataforma de streaming: EDA, calidad de datos, PCA y visualización interactiva con Streamlit.

---

## Información General

- **Integrantes:** [Nombres del grupo]
- **Comisión:** [Comisión]
- **Fecha:** [Fecha de entrega]
- **Repositorio:** [damianexequielia/PI_Mineria_Datos_1](https://github.com/damianexequielia/PI_Mineria_Datos_1)
- **App Streamlit:** [Enlace a la app en Streamlit Cloud]
- **Informe final:** [Enlace al informe PDF](reports/informe_final.pdf)
- **Log ETL:** [Enlace al log ETL](logs/pipeline_log.csv)

---

## Objetivo del proyecto

Analizar el nivel de actividad mensual de los usuarios de una plataforma de streaming, comparando el tiempo de visionado según el plan de suscripción y el país de residencia, y evaluando la calidad y coherencia de los datos registrados para construir conclusiones confiables sobre patrones de uso. El enfoque está en análisis exploratorio estructurado, con preparación de datos, visualizaciones, PCA y comunicación de resultados, sin modelos predictivos.

---

## Dataset

El dataset contiene registros de usuarios de una plataforma de streaming, con información sobre edad, plan de suscripción, país de residencia, tiempo mensual de visionado, género favorito, fecha de último inicio de sesión y tickets de soporte. El dataset presenta problemas de calidad típicos de datos reales: inconsistencias de codificación en variables categóricas, valores imposibles en numéricas, formatos de fecha inconsistentes y datos faltantes con distintos mecanismos (MCAR, MAR, MNAR). La calidad inicial requiere una etapa de preparación antes de cualquier análisis.

---

## Estructura del repositorio

```
PI_Mineria_Datos_1/
├── README.md
├── requirements.txt
├── data/
│   ├── raw/          # Dataset original JSON sin modificaciones
│   └── processed/    # Dataset procesado y limpio
├── notebooks/
│   ├── 01_inspeccion_inicial.ipynb
│   ├── 02_calidad_y_limpieza.ipynb
│   ├── 03_eda.ipynb
│   ├── 04_pca.ipynb
│   └── 05_conclusiones.ipynb
├── app/
│   ├── Home.py
│   └── pages/
│       ├── 01_Dataset.py
│       ├── 02_EDA.py
│       ├── 03_PCA.py
│       └── 04_Conclusiones.py
├── reports/
│   └── informe_final.pdf
└── logs/
    └── pipeline_log.csv
```

---

## Preparación y calidad de datos

El dataset presenta problemas de calidad típicos de datos reales: inconsistencias de codificación en variables categóricas (plan, país, género), valores imposibles en numéricas (edad 0, 130; watch_time negativo), formatos de fecha inconsistentes y datos faltantes con distintos mecanismos (MCAR, MAR, MNAR). Se aplicó un pipeline de limpieza con auditoría completa registrada en `logs/pipeline_log.csv`, siguiendo el principio de mostrar evidencia antes de cada decisión, acción y verificar el impacto de cada transformación. Cada decisión de limpieza se justificó con evidencia extraída del dataset, no con reglas automáticas.

---

## Resumen del EDA

El análisis exploratorio reveló patrones claros de actividad de usuarios: los usuarios de planes Premium tienden a tener mayor tiempo de visionado mensual que los de planes Básico y Estándar, con diferencias significativas en la mediana y dispersión. Por país, se observan diferencias en los patrones de uso, con algunos países mostrando mayor concentración de usuarios activos. El análisis multivariado (scatter con hue por plan y size por tickets) permitió identificar perfiles de usuarios: usuarios jóvenes con planes Premium y alta actividad, usuarios con alta actividad pero también muchos tickets de soporte, y segmentos de usuarios con baja actividad que podrían estar en riesgo de abandono. Las visualizaciones incluyen análisis univariado (distribución de tiempo de visionado, distribución por plan), bivariado (plan vs tiempo, país vs tiempo) y multivariado (scatter con hue y size).

---

## Reducción de dimensionalidad

Se aplicó PCA sobre las variables numéricas de engagement (edad, tiempo de visionado, tickets de soporte, recencia de login) tras aplicar escalamiento Z-score. El análisis de varianza explicada permitió identificar que los primeros componentes capturan la mayor parte de la varianza, permitiendo reducir la dimensionalidad sin perder información crítica. Los componentes principales se interpretaron como perfiles de usuarios: un componente de "intensidad de uso" (combinación de edad, tiempo de visión y tickets) y otro de "recencia de actividad". Esta reducción permite visualizar perfiles de usuarios en espacios de menor dimensión y facilita la identificación de segmentos naturales en el dataset.

---

## Visualización interactiva

La aplicación Streamlit permite explorar los resultados del análisis de forma interactiva, con cinco visualizaciones EDA (2 univariadas, 2 bivariadas, 1 multivariada) y hasta 2 visualizaciones de PCA. Cada visualización incluye interpretación conectada a las preguntas de análisis, conectando los resultados técnicos con decisiones de negocio relevantes para la plataforma de streaming.

---

## Cómo ejecutar localmente

1. Clonar el repositorio: `git clone https://github.com/damianexequielia/PI_Mineria_Datos_1.git`
2. Crear entorno virtual: `python -m venv venv && source venv/bin/activate`
3. Instalar dependencias: `pip install -r requirements.txt`
4. Ejecutar la app: `cd app && streamlit run Home.py`

---

## Conclusiones

El análisis exploratorio reveló que los planes de suscripción son un factor clave en la actividad de usuarios, con usuarios Premium mostrando mayor tiempo de visionado. Los patrones por país muestran diferencias en los comportamientos de uso, sugiriendo oportunidades de segmentación y personalización. La calidad de datos fue un aspecto crítico: la limpieza y preparación fueron fundamentales para obtener resultados confiables. Limitaciones incluyen la naturaleza del dataset (muestra, posible sesgo de selección) y la ausencia de variables temporales que permitan análisis de series temporales. Como próximos pasos, se podrían incorporar más variables de comportamiento, análisis de series temporales y modelos de segmentación.
