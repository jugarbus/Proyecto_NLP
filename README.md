Para instalar las dependencias ejecutar "pip install -r requirements.txt" en la terminal (anaconda o VS) o en una celda del código de "proyecto_NLP.ipynb"

```mermaid
graph TD
    A[Análisis de reseñas en películas] --> B[Web Scrapping]
    B --> C((Película, Usuario, Fecha, Puntuación, Reseña))
    B --> D[Preprocesamiento]
    D --> E[Análisis exploratorio]
    D --> F[Extracción de características]
    F --> G[Modelos de clasificación]
    A --> H[Objetivo]
    H --> I((Análisis de sentimientos))
    H --> J[Recomendador de películas]
    I --> K[Añade una idea relacionada]
```

```mermaid
mindmap
  root((Análisis de reseñas en películas))
    Objetivo
      Sentimientos(Análisis de sentimientos)
      Recomendador(Recomendador de películas)
    WebScrapping(Web Scrapping)
      Datos[Película, Usuario, Fecha, Puntuación, Reseña]
    Preprocesamiento
      Exploratorio(Análisis exploratorio)
      Características(Extracción de características)
        Modelos(Modelos de clasificación)
          NoPreentrenados(No preentrenados)
          Preentrenados(Preentrenados)
```
```mermaid
graph TD
    A[Análisis de reseñas en películas] --> B(Objetivo)
    B --> C[Recomendador de películas]
    B --> D[Análisis de sentimientos]
    
    C --> E[Web Scrapping]
    D --> E
    
    E --> F[Datos: Película, Usuario, Fecha, Puntuación, Reseña]
    E --> G[Kaggle Dataset]
    E --> H[Recomendación de películas a usuario]
    
    E --> I[Preprocesamiento]
    I --> J[Análisis exploratorio]
    I --> K[Extracción de características]
    
    K --> L[Modelos de clasificación]
    L --> M[No preentrenados]
    L --> N[Preentrenados]
    M --> O[Clasificación de sentimientos]
    N --> O
```
![Diagrama de flujo](diagrama_flujo.png)
