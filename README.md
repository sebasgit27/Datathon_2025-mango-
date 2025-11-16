# Mango Datathon 2024: Predicción de Producción

## Resumen del Proyecto

Este proyecto aborda el desafío de predecir la **cantidad de unidades a producir (`Production`)** para los modelos de prendas de Mango. El enfoque se centra en transformar los datos históricos de ventas y demanda a nivel semanal en *features* predictivas de alta calidad a nivel de producto (`ID`), utilizando el algoritmo de regresión **LightGBM (LGBM)**.

El objetivo principal es construir un modelo robusto que minimice el error de producción, optimizando el *Feature Engineering* y los hiperparámetros del *boosting*.

---

## Estrategia de Modelado

### 1. Feature Engineering (Agregación)

El *Feature Engineering* se basa en resumir las series de tiempo (ventas y demanda semanales) en métricas a nivel de producto (`ID`):

* **Métricas de Tendencia y Volatilidad:** Cálculo de la suma, media y la **desviación estándar (`std`)** de las ventas para medir la inestabilidad de la demanda histórica.
* **Restricción de Stock:** Inclusión del **Ratio Demanda/Venta** para cuantificar cuánto la venta real se vio limitada por la falta de *stock*.

### 2. Entrenamiento y Optimización

* **Algoritmo Base:** **LightGBM**, elegido por su velocidad, eficiencia con datos categóricos y excelente rendimiento en problemas de regresión.
* **Tuning de Hiperparámetros:** Se realiza un **Tuning Fino** del hiperparámetro `num_leaves` del LGBM en dos fases para optimizar la complejidad del árbol, minimizando el **RMSE** (Error Cuadrático Medio de la Raíz) en la validación.
* **Tratamiento Categórico:** Las *features* categóricas se convierten a tipo `category`, permitiendo a LGBM manejarlas eficientemente sin necesidad de *One-Hot Encoding*.

---

## Próximos Pasos (Ideas para Implementación Futura)

Las siguientes ideas representan las áreas de mejora y exploración que no se pudieron implementar por las limitaciones de tiempo:

* **Explotación del *Image Embedding***:
    * Aplicación de **PCA** (Análisis de Componentes Principales) sobre los *embeddings* de imagen. Los componentes se utilizarían como *features* numéricas para capturar el **estilo visual** de cada prenda o para clusters.
* **Detección de Tendencias y Contexto:**
    * Creación de *clusters* de productos basados en `embedding` y `family` para detectar **tendencias de moda recientes** y sus efectos sobre la demanda, calcular las prendas similares a las más vendidas recientemente.
    * Implementación de **Target Encoding** para las categorías de alta cardinalidad, inyectando el conocimiento del rendimiento histórico promedio de cada categoría.
* **Integración de Datos de Ciclo de Vida:**
    * Exploración de *features* que capturen las devoluciones (si están disponibles) y su impacto en el ajuste de la producción final.
* **Modelos Alternativos y Ensembles:**
    * Experimentación con otros algoritmos como **XGBoost** y la construcción de un *ensemble* para promediar las predicciones y mejorar la robustez.
