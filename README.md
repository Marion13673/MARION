# ✈️ Predicción de Retrasos de Vuelos con CatBoost

## 📌 Descripción
Este proyecto implementa un modelo de **Machine Learning** para predecir retrasos graves de vuelos (≥ 30 minutos).  
Se utiliza **CatBoostClassifier** con ingeniería de variables de fecha, hora y características del vuelo.

---

## 🚀 Cómo ejecutar el proyecto

**1. Clonar el repositorio:**
   
   ```bash
   git clone <URL-del-repo>
   cd BackEnd/Prediccion-de-Retrasos-de-Vuelos/ds
   ````

**2. 	Instalar dependencias:**
   
   ```bash
    pip install -r requirements.txt
   ````
   
**3. 	o directamente:**

    ```bash
    pip install catboost scikit-learn pandas numpy matplotlib seaborn
    ````

**4. 	Ejecutar el script de entrenamiento:**
   
   ```bash
    python modelos_retraso.py
   ````

**5. 	El modelo entrenado se guarda en:**

    ```bash
    ds/model/cat_model.joblib
    ````
---    
## 🛠️ Dependencias y versiones- Python 3.10+

- pandas 2.x
- numpy 1.26+
- scikit-learn 1.4+
- catboost 1.2+
- matplotlib 3.8+
- seaborn 0.13+
  
--- 
## 📡 Ejemplo de petición y respuesta

**Entrada (features de un vuelo):**

```bash
{
  "AEROLINEA": "LATAM",
  "AEROPUERTO_ORIGEN": "SCL",
  "AEROPUERTO_DESTINO": "JFK",
  "DISTANCIA": 8200,
  "DIA_SEMANA": 2,
  "MES_PARTIDA": 1,
  "ES_FIN_DE_SEMANA": 0,
  "TEMPORADA": "Verano",
  "HORA_LLEGADA": 14,
  "FRANJA_HORARIA_LLEGADA": "Tarde",
  "LLEGADA_PROGRAMA": 13,
  "FRANJA_LLEGADA_PROGRAMA": "Tarde"
}
 ````
**Salida (predicción del modelo):**

```bash
{
  "prevision": "Retrasado",
  "probabilidad": 0.82
}
````

**📊 Resultados del modelo- Umbral fijo: 0.7912**
- Precisión: 0.76
- Recall: 0.77
- F1-score: 0.76
- ROC-AUC: 0.97
  
**Matriz de confusión**

```bash
[[1002183   31512]
 [  29915  100206]]
````
--- 
## 📂 Dataset utilizado

Se emplea el dataset de vuelos históricos de EE.UU. (2015), disponible en el repositorio del Bureau of Transportation Statistics (BTS):

👉 On-Time Performance Dataset (transtats.bts.gov in Bing)

Variables principales:

- Aerolínea
- Aeropuerto origen/destino
- Fecha y hora de partida/llegada
- Retrasos por causa (clima, aerolínea, sistema aéreo, seguridad, avión tardío)

**📜 LicenciaEste proyecto se distribuye bajo la licencia MIT.**



