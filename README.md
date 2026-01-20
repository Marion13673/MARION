**Notebook_flight_on_time.ipynb**
# ✈️ FlightOnTime API

## 📌 Descripción
FlightOnTime es una aplicación que permite **predecir retrasos de vuelos** a partir de datos como aerolínea, origen, destino, fecha de partida y distancia.

El proyecto combina:
- **Backend en Spring Boot** para exponer endpoints REST y formularios web con Thymeleaf.
- **Modelo de Machine Learning en Python (scikit-learn)** entrenado con datos históricos de vuelos.

---

## 🛠️ Tecnologías utilizadas
- **Java 17** + **Spring Boot 3.3.1**
- **Thymeleaf** para vistas HTML
- **Maven** para gestión de dependencias
- **Python 3.x** + **scikit-learn**, **pandas**, **numpy**, **catboost**
- **Joblib** para exportar el modelo entrenado
- **Git LFS** para manejar datasets grandes

---


## 📂 Estructura del proyecto
````
Prediccion-de-Retrasos-de-Vuelos/
├── be/                          # Backend en Spring Boot
│   ├── pom.xml                  # Configuración de Maven
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/com/flightontime/
│   │   │   │   ├── controller/
│   │   │   │   │   ├── @RestController.java
│   │   │   │   │   ├── PredictController.java
│   │   │   │   │   ├── StatsController.java
│   │   │   │   │   └── WebController.java
│   │   │   │   ├── dto/
│   │   │   │   │   ├── FlightInput.java
│   │   │   │   │   └── PredictionOutput.java
│   │   │   │   ├── exception/
│   │   │   │   │   └── GlobalExceptionHandler.java
│   │   │   │   ├── service/
│   │   │   │   │   └── DsClient.java
│   │   │   │   └── FlightOnTimeApplication.java
│   │   │   └── resources/
│   │   │       ├── application.yml
│   │   │       └── templates/
│   │   │           ├── form.html
│   │   │           └── result.html
│   └── target/
│       ├── classes/
│       │   ├── application.yml
│       │   ├── com/flightontime/
│       │   │   ├── controller/
|       |   |   |   |__ @RestController.class 
│       │   │   │   ├── PredictController.class
│       │   │   │   ├── StatsController.class
│       │   │   │   └── WebController.class
│       │   │   ├── dto/
│       │   │   │   ├── FlightInput.class
│       │   │   │   └── PredictionOutput.class
│       │   │   ├── exception/
│       │   │   │   └── GlobalExceptionHandler.class
│       │   │   ├── service/
│       │   │   │   └── DsClient.class
│       │   │   └── FlightOnTimeApplication.class
│       │   └── templates/
│       │       ├── form.html
│       │       └── result.html
│       ├── generated-sources/
│       │   └── annotations/
│       └── maven-status/
│           └── maven-compiler-plugin/
│               └── compile/
│                   └── default-compile/
│                       ├── createdFiles.lst
│                       └── inputFiles.lst
├── ds/                          # Data Science / Machine Learning
│   ├── app/
│   │   ├── dashboard.py
│   │   ├
│   │   └── main.py
│   ├── data/
│   │   └── flights2015.csv
│   ├── model/
│   │   └── flight_delay_model.joblib
│   ├── notebook_flight_on_time.ipynb
│   └── requirements.txt
├── README.md                    # Documentación del proyecto
└── .gitignore                   # Archivos ignorados por Git
````

## 🔎 Explicación:
- be/ → Todo el backend en Spring Boot (controladores, DTOs, vistas Thymeleaf, configuración).
  - ds/ → Todo lo relacionado con el modelo de ML (dataset, notebooks, scripts, modelo exportado).
- templates/ → Vistas HTML (form.html y result.html).
- model/ → Carpeta donde se guarda el modelo entrenado (flight_delay_model.joblib).
- README.md → Guía de uso y documentación del proyecto.


## 🚀 Cómo ejecutar

**1. Entrenar el modelo en Python**

```bash
cd ds
pip install -r requirements.txt
````

**2. Entrenar el modelo**

```bash
python entrenar.py
````

**Esto genera el archivo:**

model/flight_delay_model.joblib

**3. Ejecutar el backend**

```bash
cd be
mvnd spring-boot:run
````

**El servidor se levanta en:**

```bash
http://127.0.0.1:5000/docs
mvnd spring-boot:run
````

**📑 Endpoints**

**REST API**
**- POST /predict**

**Recibe un JSON con los datos del vuelo y devuelve la predicción.**

{
  "aerolinea": "LATAM",
  "origen": "SCL",
  "destino": "JFK",
  "fecha_partida": "2026-01-10T15:00:00",
  "distancia_km": 8200
}

**- Respuesta:**

{
  "prevision": "Retrasado",
  "probabilidad": 0.821,
  "features": {
    "aerolinea": "LATAM",
    "origen": "SCL",
    "destino": "JFK",
    "distancia_km": 8200,
    "dia_semana": 6
  }
}

**Interfaz Web**

- GET /form → muestra formulario HTML.
- POST /form → procesa datos y muestra resultado en result.html.

**📊 Modelo de Machine Learning**
**- Features utilizadas:**

  > - Aerolínea
  > - Origen
  > - Destino
  > - Hora de partida
  > - Día de la semana
  > - Distancia (km)

**- Target:** `RETRASO_GRAVE`  
(0 = vuelo puntual, 1 = retraso grave ≥ 30 minutos)

**- Algoritmo:** CatBoostClassifier  
Maneja variables categóricas de forma nativa (`cat_features`), sin necesidad de OneHotEncoder.

**- Métricas de evaluación:**  
- Accuracy  
- Precision  
- Recall  
- F1-score  
- ROC-AUC (para medir capacidad de discriminación global)

**⚠️ Notas**

- Los datasets grandes están versionados con Git LFS.
Asegúrate de ejecutar:

git lfs install
git lfs pull

**🤝 Contribución**

- Haz un fork del repositorio.
- Crea una rama (feature/nueva-funcionalidad).
- Haz commit de tus cambios.
- Haz push a la rama.
- Abre un Pull Request.
## 🤝 Contribución

¡Gracias por tu interés en contribuir! Para mantener un flujo de trabajo ordenado:

1. Haz un **fork** de este repositorio.
2. Crea una rama descriptiva para tu aporte:
     
   ```bash
   git checkout -b feature/nueva-funcionalidad
   ````
3. Realiza tus cambios y haz commit con mensajes claros:
    
    ```bash
   git commit -m "Agrega validación de retrasos graves en API"
   ````
4. Haz push a tu rama:
   
   ```bash
   git push origin feature/nueva-funcionalidad
   ````
5. Abre un Pull Request explicando:
   
    - Qué problema resuelve.
    - Qué cambios introduces.
    - Cómo probarlos.

**🌙 En resumen:**

 Este README da una guía para entrenar el modelo, correr el backend y usar tanto la API REST como el formulario web.  


**📜 Licencia**
Este proyecto se distribuye bajo la licencia MIT.








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



