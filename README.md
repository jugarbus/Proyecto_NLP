Para instalar las dependencias ejecutar "pip install -r requirements.txt" en la terminal (anaconda o VS) o en una celda del código de "proyecto_NLP.ipynb"

```mermaid
graph TD
    A[Inicio] --> B{Recolección de Datos};

    B --> B1[Definir páginas de Metacritic y límite de 24 películas por página]
    B1 --> B2[Configurar cabecera HTTP personalizada (simular navegador)]
    B2 --> B3[Extraer enlaces de películas con BeautifulSoup (primeras 24)]
    B3 --> B4[Generar URLs para secciones de reseñas (filtros específicos)]
    B4 --> B5[Extraer reseñas con Selenium (manejo de contenido dinámico)]
    B5 --> B6[Extraer info clave: usuario, fecha, puntuación, texto]
    B6 --> B7{Fases de Scraping};
    B7 -- Fase 1: Positivas, Neutras, Negativas inicial --> B8[Conjunto inicial de datos]
    B7 -- Fase 2: Ampliar muestras --> B9[Desequilibrio detectado (más positivas)]
    B7 -- Fases 3 y 4: Filtrar Neutras y Negativas --> B10[Equilibrar conjunto de datos (aprox. 10,000 reseñas)]
    B10 --> B11[Limitar extracción a 50 reseñas por película]
    B11 --> B12[Combinar reseñas en DataFrame de Pandas]
    B12 --> B13[Revisar calidad y coherencia de datos]
    B13 --> C{Preprocesamiento de Texto};

    C --> C1[Cargar y Consolidar 4 archivos CSV en un único DataFrame]
    C1 --> C2[Detectar y revisar filas duplicadas]
    C2 --> C3[Extraer y transformar nombre de película de URLs (expresiones regulares)]
    C3 --> C4[Eliminar filas vacías o con "SPOILER ALERT"]
    C4 --> C5[Detectar idioma de cada reseña y filtrar solo inglés]
    C5 --> C6[Asignar etiquetas de sentimiento (0-3 NEG, 4-6 NEU, 7-10 POS)]
    C6 --> C7[Importar stopwords en inglés (spaCy)]
    C7 --> C8[Calcular y visualizar porcentaje de stopwords vs. contenido (por sentimiento)]
    C8 --> C9[Normalizar y Lematizar texto];
    C9 --> C9.1[Eliminar números]
    C9.1 --> C9.2[Tokenizar y Lematizar con spaCy]
    C9.2 --> C9.3[Eliminar puntuación, espacios innecesarios y stopwords]
    C9.3 --> C9.4[Convertir a minúsculas]
    C9.4 --> C9.5[Reconstruir texto limpio (con y sin lematización)]
    C9.5 --> D{Análisis Exploratorio};

    D --> D1[Tokenización con spaCy (crear columna 'tokens')]
    D1 --> D2[Analizar longitud de textos (palabras por reseña)]
    D2 --> D3[Generar histogramas de longitud por sentimiento y global]
    D3 --> D4[Generar Nubes de Palabras (WordClouds)];
    D4 --> D4.1[Eliminar palabras más frecuentes del conjunto general]
    D4.1 --> D4.2[Agrupar palabras restantes por clase de sentimiento]
    D4.2 --> D4.3[Generar WordClouds individuales]
    D4 --> D5[Generar y Visualizar N-gramas (Bigramas y Trigramas)];
    D5 --> D5.1[Extraer tokens por clase de sentimiento]
    D5.1 --> D5.2[Calcular frecuencia de bigramas y trigramas]
    D5.2 --> D5.3[Seleccionar los 10 más comunes por clase]
    D5.3 --> D5.4[Visualizar en gráficos de barras horizontales]
    D5.4 --> D6[Analizar Distribución de Muestras por Clase];
    D6 --> D6.1[Generar diagramas de barras para sentimiento (POS, NEU, NEG)]
    D6.1 --> D6.2[Generar histograma para puntuaciones (score 0-10)]
    D6.2 --> E{Extracción de Características};

    E --> E1[Características Sparse (dispersas)];
    E1 --> E1.1[Aplicar TF-IDF (Term Frequency-Inverse Document Frequency)]
    E1.1 --> E1.2[Establecer max_features=1000 (palabras más frecuentes)]
    E1 --> E2[Características Dense (densas)];
    E2 --> E2.1[GloVe Embeddings (modelo preentrenado 50 dimensiones)]
    E2.1 --> E2.1.1[Calcular promedio de vectores por reseña]
    E2.1 --> E2.2[BERT Embeddings (modelo 'all-mpnet-base-v2' de sentence-transformers)]
    E2.2 --> E2.2.1[Generar embedding para cada reseña completa (768 dimensiones)]
    E2.2.1 --> F{Modelos};

    F --> F1[Modelos Entrenados desde Cero];
    F1 --> F1.1[TF-IDF + Regresión Logística (LR)]
    F1.1 --> F1.2[TF-IDF + Topic Modeling (LSA) + LR (reducir a 15 dimensiones)]
    F1.2 --> F1.3[TF-IDF + Topic Modeling (LSA) + XGBoost]
    F1.3 --> F1.4[GloVe Embeddings + LR]
    F1.4 --> F1.5[BERT Embeddings + LR]
    F1.5 --> F1.6[BERT Embeddings + LR (class_weight=balanced)]
    F1 --> F2[Modelos Preentrenados];
    F2 --> F2.1[Pipeline RoBERTa preentrenado (cardiffnlp/twitter-roberta-base-sentiment)]
    F2.1 --> F2.2[BERT preentrenado con Fine-tuning (google-bert/bert-base-cased)]
    F2.2 --> G{Resultados y Mejoras};

    G --> G1[Análisis de Modelos de Clasificación de Sentimiento]
    G1 --> G1.1[Comparar Accuracy y F1-score por clase (NEG, NEU, POS)]
    G1.1 --> G1.2[Identificar el mejor modelo (BERT Fine-tuning)]
    G1 --> G2[Análisis de Modelos de Predicción de Puntuación]
    G2 --> G2.1[TF-IDF + LR y BERT + LR (rendimiento bajo)]
    G2.1 --> G2.2[Observar concentración de predicciones en 0, 6 y 10]
    G2.2 --> G2.3[Relacionar con desequilibrio de clases en los datos]
    G2.3 --> G3[Análisis de Errores de Clasificación (Matriz de Confusión TF-IDF + LR)]
    G3 --> G3.1[Identificar errores en la clase NEU (clasificada como POS/NEG)]
    G3.1 --> G3.2[Revisar ejemplos de reseñas mal clasificadas]
    G3.2 --> H{Recomendador de Películas};

    H --> H1[Enriquecimiento del dataset con géneros de películas (Kaggle)]
    H1 --> H2[Transformar géneros a formato one-hot encoding]
    H2 --> H3[Seleccionar usuario aleatorio con al menos 10 reseñas]
    H3 --> H4[Filtrar películas reseñadas por el usuario y con géneros]
    H4 --> H5[Construir perfil del usuario (vector de preferencias por género)]
    H5 --> H6[Calcular puntuaciones de recomendación para todas las películas]
    H6 --> H7[Normalizar puntuaciones]
    H7 --> H8[Seleccionar las 5 películas mejor puntuadas como recomendación]
    H8 --> I[Fin];
