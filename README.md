# Data Science Portfolio — Joaquín Bocco

[![Python](https://img.shields.io/badge/python-3.10%2B-blue)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/license-MIT-green)](LICENSE)
[![Open Clustering in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/JoaquinBocco/Data-science-portfolio/blob/main/Joaquin_Bocco_Clustering_Vinos.ipynb)
[![Open ML Supervisado in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/JoaquinBocco/Data-science-portfolio/blob/main/Joaquin_Bocco_ML_Supervisado_Vinos.ipynb)
[![Open Autos in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/JoaquinBocco/Data-science-portfolio/blob/main/Joaquin_Bocco_Analisis_Autos_Usados.ipynb)

Proyectos de análisis de datos y Machine Learning desarrollados durante la Diplomatura Universitaria en Data Science & Machine Learning (ICARO / UNC - FCEFyN).

Estudiante de la Licenciatura en Física (UNC - FaMAF), con formación complementaria en análisis de datos, Machine Learning y visualización.

**Stack:** Python · Pandas · NumPy · Matplotlib/Seaborn · scikit-learn · XGBoost · SHAP

---

## 📁 Estructura del repositorio

```
Data-science-portfolio/
├── README.md
├── LICENSE
├── requirements.txt
├── Joaquin_Bocco_Clustering_Vinos.ipynb
├── Joaquin_Bocco_ML_Supervisado_Vinos.ipynb
├── Joaquin_Bocco_Analisis_Autos_Usados.ipynb
└── Vehicle_Sales_Data_Final.pptx      # presentación de resultados del EDA de autos
```

## ⚙️ Cómo reproducir los notebooks

```bash
git clone https://github.com/JoaquinBocco/Data-science-portfolio.git
cd Data-science-portfolio
pip install -r requirements.txt
```

Los datasets no están incluidos en el repo (uno tiene licencia de Kaggle, el otro se
descarga directo por URL dentro del propio notebook):

- **Vinos** (clustering y ML supervisado): se bajan automáticamente desde el [UCI Machine
  Learning Repository](https://archive.ics.uci.edu/dataset/186/wine+quality) al correr la
  celda de carga de datos — no requiere ningún paso manual.
- **Autos usados**: dataset ["Vehicle Sales Data"](https://www.kaggle.com/datasets/syedanwarafridi/vehicle-sales-data)
  de Kaggle (requiere cuenta). Descargá `car_prices.csv` y colocalo en la raíz del repo
  antes de correr `Joaquin_Bocco_Analisis_Autos_Usados.ipynb`.

---

## 📊 Proyectos

### 1. Clustering y Reducción de Dimensionalidad — Wine Quality
`Joaquin_Bocco_Clustering_Vinos.ipynb`

Análisis no supervisado sobre el dataset "Wine Quality" (~6.500 vinos tintos y blancos, 11 variables fisicoquímicas).

- Apliqué **KMeans** y **DBSCAN**, comparando su desempeño con Silhouette Score, Calinski-Harabasz y Davies-Bouldin. El umbral `eps` de DBSCAN se detecta de forma automática y reproducible (método Kneedle sobre el K-distance plot), no a ojo.
- Usé **PCA**, **t-SNE** y **UMAP** para visualizar la estructura de los clusters en 2D.
- **Resultado:** KMeans (K=3) da la segmentación más estable e interpretable (Silhouette = 0.235); DBSCAN, con estos parámetros, no logra separar más de un cluster denso. UMAP es la técnica de visualización que mejor preserva la separación entre vinos tintos y blancos.

<img src="images/clustering_umap.png" width="500" alt="Proyección UMAP coloreada por tipo de vino">


### 2. Machine Learning Supervisado — Clasificación y Regresión de Vinos
`Joaquin_Bocco_ML_Supervisado_Vinos.ipynb`

Flujo de trabajo de ML de punta a punta sobre el mismo dataset, con dos tareas:

| Tarea | Mejor modelo | Métrica (test) | Validado con CV (5-fold) |
|---|---|---|---|
| Clasificación (tinto/blanco) | XGBoost | Accuracy 0.997, F1 1.00 | ✅ |
| Regresión (calidad) | Random Forest | MAE 0.441, R² 0.489 | ✅ |

- Ambos modelos ganadores se comparan contra baselines simples (Regresión Logística / Lineal) y se optimizan con `GridSearchCV`.
- Los resultados de test se validan con **cross-validation** (media ± desvío en 5 folds) para descartar que el número de test sea un golpe de suerte del split.
- Interpretabilidad con **SHAP** (TreeExplainer) sobre los modelos ganadores: qué variables fisicoquímicas pesan más para distinguir tipo de vino y para explicar la calidad predicha — no solo *cuánto* acierta el modelo, sino *por qué*.
- Clasificar el tipo de vino resulta una tarea mucho más fácil para los modelos que predecir la calidad, consistente con que esta última es una variable parcialmente subjetiva (puntaje sensorial humano) con relaciones no lineales más débiles respecto a las variables fisicoquímicas.

<img src="images/ml_shap_clasificacion.png" width="600" alt="Importancia de variables SHAP para XGBoost">


### 3. Análisis Exploratorio de Datos — Precios de Autos Usados
`Joaquin_Bocco_Analisis_Autos_Usados.ipynb`

EDA sobre ~480.000 registros (tras limpieza) de ventas de autos usados en EE.UU.

- Limpieza de datos, detección de valores centinela (ej. odómetro con lecturas placeholder tipo 999999) y tratamiento de outliers por IQR sobre precio y kilometraje.
- Análisis de correlaciones entre año, kilometraje y precio de venta.
- Identificación de qué marcas y décadas concentran mayor valor de reventa, y cómo transmisión y kilometraje impactan el precio.
- Presentación de resultados: `Vehicle_Sales_Data_Final.pptx`.

<img src="images/autos_precio_vs_km.png" width="600" alt="Precio de venta vs. kilometraje, coloreado por década">


---

## 📫 Contacto

- Email: joacobocco@gmail.com
- LinkedIn: [linkedin.com/in/joaquín-bocco-659386429](http://www.linkedin.com/in/joaqu%C3%ADn-bocco-659386429)
