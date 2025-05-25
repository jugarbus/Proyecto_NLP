# Instalación de dependencias

Para instalar las dependencias necesarias para ejecutar el proyecto, puedes ejecutar el siguiente comando en la terminal (ya sea en Anaconda Prompt, VS Code o cualquier otra terminal):

```bash
pip install -r requirements.txt
```

# Descripción de los archivos

## fine_tunning_collab.ipynb
Este notebook contiene el código para realizar el **fine-tuning** de un modelo BERT preentrenado (`google-bert/bert-base-cased`).  
Está diseñado para ejecutarse en **Google Colab**, facilitando el entrenamiento y ajuste fino del modelo sobre nuestro conjunto de datos específico, con el objetivo de mejorar su rendimiento en tareas de Procesamiento de Lenguaje Natural (NLP).

---

## proyecto_NLP.ipynb
Este notebook es el archivo principal del proyecto, donde se desarrolla el pipeline completo y el análisis relacionado con el proyecto de NLP.  
Incluye la preparación de datos, extracción de características, entrenamiento y evaluación de modelos, entre otros procesos fundamentales para el desarrollo integral del proyecto.

# Descripción de los datasets

En la carpeta `data` se encuentran los archivos CSV con los datos utilizados en el proyecto. A continuación se detalla el contenido y propósito de cada uno:

- **reviews_*.csv**  
  Son las reseñas en crudo extraídas mediante web scraping de forma iterativa. Este proceso se realizó varias veces debido a su duración, generando múltiples archivos que luego se concatenaron para formar el conjunto completo de reseñas.

- **reviews_finales_bad_mixed_only.csv**  
  Este archivo es el resultado de extraer únicamente reseñas negativas y mixtas con el fin de equilibrar el desbalance original entre etiquetas positivas, neutras y negativas. Se añadieron solo reseñas negativas y neutras para mejorar la representatividad del dataset.

- **df_final.csv**  
  Dataset postprocesado y preparado para las etapas posteriores de análisis y modelado.

- **df_rango_final.csv**  
  Versión del dataset que incluye una columna adicional con un score de coherencia asignado a cada reseña, útil para evaluar la calidad del texto.

- **16k_Movies.csv**  
  Dataset complementario obtenido de Kaggle, que contiene información sobre géneros de películas. Se utilizó para enriquecer los datos y facilitar la construcción del sistema recomendador.


# Diagrama
![Diagrama de flujo](diagrama_flujo.png)



