# 📊 Challenge TelcomX LATAM - Parte 2

Este proyecto forma parte del **Challenge TelcomX LATAM**, orientado a aplicar técnicas de análisis exploratorio de datos (EDA), limpieza y preprocesamiento de datos con el objetivo de preparar un dataset para futuros modelos predictivos en el ámbito de telecomunicaciones que ayuden a detectar aquellos clientes más propensos al abandono de empresa (churn).

---

## 🧠 Objetivo

Analizar y transformar un conjunto de datos previamente tratado (`datos_tratados_parte1.csv`) con el fin de:

- Realizar un análisis exploratorio de datos (EDA).
- Identificar patrones o tendencias relevantes.
- Preparar el dataset para modelos de predicción enfocados en *churn* (abandono de clientes).
- Generar recomendaciones basadas en el estudio y los resultados arrojados por el modelo predictivo.

---

## 📊 Fuente de datos

Los datos utilizados en este análisis provienen del archivo `datos_tratados_parte1.csv`, que contiene información de clientes de Telcom X Latam, incluyendo datos demográficos, servicios, información de contrato y cargos.

---

## 🛠️ Metodología y procesamiento de datos

El procesamiento de datos y la metodología aplicada incluyeron los siguientes pasos clave:

- Carga e inspección inicial del dataset.
- Eliminación de columnas no relevantes.
- Codificación de variables categóricas.
- Definición de variable objetivo y características.
- Aplicación de transformaciones y escalado.
- División del dataset para entrenamiento y prueba (80/20).
- Manejo del desbalance de clases con SMOTE.

---

## 🔍Análisis y hallazgos clave

Los análisis realizados y los hallazgos clave incluyen:


- **Análisis EDA y preparación de datos:** Se inició el análisis cargando y explorando el conjunto de datos trabajado en el primer desafío. Se realizó un análisis de la distribución de variables numéricas y categóricas para comprender la composición de la base de clientes e identificar posibles sesgos o anomalías. Se observó un desbalance de clases significativo en la variable objetivo 'AbandonoEmpresa', con aproximadamente un 26.5% de clientes que abandonaron. Las variables irrelevantes para el modelado predictivo, como 'IDCliente', 'Rango_MesesAntiguedad', 'Cuentas_Diarias' y 'CargosMensuales_por_MesesAntiguedad', fueron eliminadas debido a que no proveen información nueva o bien útil para el estudio. Se aplicó codificación One-Hot a las variables categóricas y se utilizó imputación por la media para tratar los valores faltantes en 'CargosTotales'.

- **Factores clave que influyen en la cancelación:** El análisis de correlación y la importancia de variables derivada de los modelos (coeficientes para Regresión Logística, importancia por permutación para KNN e importancia de características para Árbol de Decisión) han permitido identificar los factores más influyentes en el abandono de clientes:

1.   **Antigüedad del cliente:** Consistentemente, la antigüedad emergió como uno de los predictores más fuertes. Los clientes con menos tiempo en la empresa son significativamente más propensos a abandonar. Esto indica la importancia de las primeras etapas de la relación con el cliente.

2.   **Tipo de Contrato:** El tipo de contrato tiene un impacto sustancial. Los contratos mensuales están fuertemente asociados con una mayor probabilidad de abandono, mientras que los contratos a largo plazo (dos años) son un factor de retención clave.

3.   **Servicio de Internet:** El tipo de conexión a internet también es relevante. Los clientes con servicio de Fibra Óptica mostraron una mayor tendencia al abandono, mientras que aquellos sin servicio de internet eran los menos propensos a irse. Esto sugiere la necesidad de investigar la satisfacción con el servicio de Fibra Óptica. (seria interesante en un futuro producir una tabla con el título 'Satisfacción cliente')

4.   **Cargos (`CargosTotales`, `CargosMensuales`):** Los cargos mensuales más altos se asociaron con una mayor probabilidad de abandono, mientras que los cargos totales más altos (generalmente ligados a una mayor antigüedad) se asociaron con una menor probabilidad de abandono. 

5.   **Método de Pago:** El método de pago también influye, con el pago electrónico mostrando una asociación con una mayor probabilidad de abandono en algunos modelos.(Árbol de Decisión y KNN)

---

## 💻Procesamiento y elección del modelo predictivo

- **Modelado predictivo del abandono:** Para abordar el desbalance de clases, se aplicó la técnica SMOTE al conjunto de entrenamiento. Se dividió el conjunto de datos en conjuntos de entrenamiento y prueba manteniendo la proporción de la clase objetivo.
Se evaluaron tres modelos de clasificación: Regresión Logística, K-Nearest Neighbors (KNN) y Árbol de Decisión. Se construyeron pipelines que incluyeron pasos de escalado (StandardScaler para LR, MinMaxScaler para KNN) y el clasificador. Se realizó sintonización de hiperparámetros utilizando GridSearchCV con F1-score como métrica principal en validación cruzada para optimizar el rendimiento, especialmente en la clase minoritaria. También se exploró el impacto de ajustar el umbral de decisión, el cual afecto positivamente las métricas del modelo KNN.

- **Modelo recomendado:** Se seleccionó la **Regresión Logística sintonizada** como el modelo recomendado por su balance de métricas, capacidad para identificar churn (**Recall**) e interpretabilidad de coeficientes.
  
- **Conclusión:** El análisis identificó los impulsores clave del abandono (antigüedad, contrato, servicios, cargos, pago). El modelo de Regresión Logística sintonizada es una herramienta predictiva útil. Se recomienda implementar estrategias de retención dirigidas y monitorear continuamente.

---

## 💡Estrategias de retención propuestas:
Basándonos en los factores clave de abandono identificados y el modelo predictivo seleccionado, se proponen las siguientes estrategias de retención:

1.  **Enfoque en clientes nuevos:** Implementar programas de bienvenida y "onboarding" proactivos durante los primeros 6-12 meses para asegurar la satisfacción del cliente, resolver dudas y ofrecer soporte adicional. Considerar incentivos para compromisos a más largo plazo al inicio.

2.  **Incentivos para contratos a largo plazo:** Promocionar activamente los contratos anuales y de dos años, ofreciendo descuentos o beneficios adicionales en comparación con los contratos mensuales.

3.  **Mejora del Servicio de Fibra Óptica:** Realizar encuestas de satisfacción específicas para usuarios de Fibra Óptica e investigar posibles problemas de calidad o percepción de valor. Considerar ajustes en la oferta o comunicación para este segmento. Sería interesante ofrecer un servicio de soporte técnico exclusivo 24/7.

4.  **Gestión de Cargos Mensuales altos:** Para clientes con cargos mensuales elevados (especialmente si son nuevos), considerar ofertas personalizadas, planes de pago flexibles o comunicación proactiva sobre el valor del servicio para justificar el costo.

5.  **Análisis del comportamiento por Método de Pago:** Investigar las razones detrás de la mayor tasa de abandono en clientes que pagan electrónicamente.(¿Habrá algun problema técnico recurrente?) 

6.  **Campañas de retención dirigidas:** Utilizar el modelo de Regresión Logística sintonizada para identificar a los clientes con alta probabilidad de abandono. Diseñar campañas de retención personalizadas basadas en los factores de riesgo específicos de cada cliente.

---

## ⚙️ Dependencias

Las dependencias principales utilizadas en este proyecto son:

- pandas
- numpy
- scikit-learn
- imbalanced-learn
- matplotlib
- seaborn
- joblib

---

## 🚀 Cómo ejecutar el proyecto

Para ejecutar este proyecto, sigue estos pasos:

1. Clona este repositorio.
2. Asegúrate de tener Python y las dependencias instaladas.
3. Descarga el archivo de datos `datos_tratados_parte1.csv` y colócalo en la ubicación esperada (`/content/datos_tratados_parte1.csv` o actualiza la ruta en el código).
4. Ejecuta el notebook `Challenge_TelcomX_parte2_Latam.ipynb` en un entorno como Google Colab o Jupyter Notebook para reproducir el análisis y el modelado.

---

## ❗ Posibles problemas y soluciones

Algunos posibles problemas que podrías encontrar y sus soluciones:

- **Ruta del archivo de datos:** Asegúrate de que la ruta al archivo `datos_tratados_parte1.csv` en el notebook sea correcta.
- **Dependencias faltantes:** Instala todas las librerías necesarias (`pip install -r requirements.txt`).
- **Recursos computacionales:** Algunos pasos de modelado y sintonización de hiperparámetros pueden requerir tiempo y recursos significativos.

---

