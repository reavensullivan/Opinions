# Opinions
Actividad 4, detección de emociones en reseñas
# Comparación de modelos preentrenados

Este repositorio contiene un flujo de trabajo para evaluar y comparar el rendimiento de tres arquitecturas de Procesamiento del Lenguaje Natural (NLP) preentrenadas y optimizadas de Hugging Face para la tarea de **Análisis de Sentimientos**.

## 1. Título y descripción
**Proyecto:** *Actividad 4: Comparación de Modelos Preentrenados para Análisis de Sentimientos (SST-2)*

Este proyecto evalúa y compara de manera cuantitativa tres modelos populares de la librería transformers utilizando una fracción del conjunto de datos **SST-2 (Stanford Sentiment Treebank)**. El objetivo es analizar el balance o *trade-off* entre la precisión de las predicciones (Accuracy, F1-Score) y la eficiencia computacional (Latencia de Inferencia por registro).

## 2. Tecnologías utilizadas
* **Lenguaje:** Python 3.x
* **Entorno:** Google Colab / Jupyter Notebooks
* **Librerías Clave:**
  * transformers (Hugging Face) para cargar los modelos y realizar inferencia mediante pipeline.
  * datasets para el manejo de conjuntos de datos.
  * pandas y numpy para la manipulación y estructuración de los datos y métricas.
  * scikit-learn para el cálculo de las métricas de evaluación (accuracy_score, precision_recall_fscore_support).
  * torch (PyTorch) como motor de ejecución (Backend).

## 3. Estructura del proyecto
El flujo de ejecución está organizado de la siguiente manera:
1. **Configuración del Entorno:** Verificación de disponibilidad de GPU e instalación silenciosa de dependencias.
2. **Carga de Librerías:** Importación de módulos requeridos para el análisis de datos y procesamiento de NLP.
3. **Carga y Preparación del Dataset:** Carga del split de validación del dataset SST-2 (primeras 300 muestras como muestra representativa) utilizando un método principal vía Parquet y un mecanismo de respaldo por URL.
4. **Evaluación de Modelos:** Inferencia secuencial utilizando tres modelos específicos:
   * **DistilBERT:** distilbert-base-uncased-finetuned-sst-2-english
   * **RoBERTa:** siebert/sentiment-roberta-large-english
   * **MobileBERT:** Alireza1044/mobilebert_sst2
5. **Consolidación de resultados:** Construcción de una tabla comparativa con métricas de clasificación y latencia promedio.

## 4. Instrucciones de uso
1. Abre este cuaderno en Google Colab.
2. Asegúrate de configurar el entorno de ejecución (se recomienda activar la GPU para acelerar la evaluación, aunque el script cuenta con un respaldo automático para CPU).
3. Ejecuta las celdas secuencialmente desde el inicio hasta el final.
4. Al finalizar la ejecución de la sección 4, se generará y visualizará el cuadro comparativo en la sección 5.

## 5. Resultados obtenidos
A continuación se presentan las métricas de rendimiento recolectadas sobre las 300 muestras evaluadas:

| Modelo | Accuracy | Precision | Recall | F1-Score | Latencia Promedio (ms) |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **DistilBERT** | 0.9067 | 0.8944 | 0.9290 | 0.9114 | 166.07 |
| **RoBERTa** | 0.9167 | 0.9062 | 0.9355 | 0.9206 | 604.05 |
| **MobileBERT** | 0.8933 | 0.8868 | 0.9097 | 0.8981 | 59.59 |

### Conclusiones del análisis:
* **Mayor Precisión:** **RoBERTa** ofrece las métricas más altas en Accuracy (91.67%) y F1-Score (92.06%), pero a cambio de la mayor latencia de inferencia (~604 ms/reg).
* **Mejor Eficiencia / Velocidad:** **MobileBERT** destaca por su extrema rapidez, registrando una latencia promedio de tan solo ~59.6 ms por registro, reteniendo un desempeño muy competitivo (89.33% de Accuracy).
* **Punto de Equilibrio:** **DistilBERT** ofrece un balance ideal, alcanzando métricas muy cercanas a RoBERTa (~90.67% de Accuracy) con un tercio de su tiempo de respuesta (~166 ms).
