# ✈️FlightOnTime
# 🚀 INTRODUCCIÓN 

El proyecto **FlightOnTime** consiste desarrollar una solución predictiva capaz de estimar si un vuelo va a despegar a tiempo o con retraso. 

# 🎯 Objetivos relacionados al cliente

## Para los pasajeros
- Recibir alertas tempranas sobre posibles retrasos antes de salir de casa.
- Tomar decisiones informadas sobre su itinerario y reducir tiempos de espera innecesarios.
## Para las aerolíneas
- Ajustar la operación en función de la probabilidad de retraso.
- Minimizar el impacto en la programación de vuelos y en la experiencia del cliente.
- Optimizar recursos como tripulación y mantenimiento preventivo.
## Para los aeropuertos
- Planificar mejor el uso de la infraestructura (puertas de embarque, pistas, personal).
- Reducir la congestión y mejorar la eficiencia operativa.
- Coordinar con aerolíneas y servicios de apoyo para anticipar escenarios críticos.

# 🎯 Objetivos de mercado
  
**1.- Validar la utilidad de la ciencia de datos en transporte aéreo**
Demostrar que la predicción de retrasos es una aplicación práctica y con impacto directo en la industria.

**2.- Generar un diferencial competitivo para aerolíneas y startups**
Ofrecer modelos predictivos que permitan anticipar riesgos y posicionarse como líderes en innovación.

**3.- Mejorar la puntualidad y planificación de flota**
Facilitar la toma de decisiones estratégicas en la operación diaria, optimizando recursos y horarios.

**4.- Reducir costos operativos y quejas de clientes**
Minimizar pérdidas asociadas a retrasos y mejorar la percepción del servicio.

**5.- Aumentar la satisfacción del cliente mediante transparencia**
Proveer información clara y anticipada que fortalezca la confianza en las aerolíneas.

**6.- Identificar patrones de riesgo en horarios y aeropuertos**
Usar incluso modelos simples para detectar puntos críticos, aportando valor inmediato al sector.

---
Notebook variables explicativas: causas de retrasos graves flights2015.ipynb
# VARIABLES EXPLICATIVAS DE LAS CAUSAS QUE INFLUYEN EN LOS RETRASOS GRAVES

# ✨ Características 

Base de datos: **flights2015.parquet**, contribuye a mejorar:

1.- Formato:  Binario, columnas

2.- Compresión:  Alta compresión, ocupa mucho menos espacio

3.- Lectura/Escritura:  Optimizado para lectura selectiva

4.- Estructura:  Mantiene tipos (int, float, string, etc.)

5.- Escalabilidad:  Ideal para big data y sistemas distribuidos

6.- Compatibilidad:  Requiere librerías (pandas, pyarrow, spark)

Cuando usar:
**Parquet**

- Cuando trabajas con grandes volúmenes de datos.
  
- En pipelines de machine learning y big data.
  
- Cuando la eficiencia y el rendimiento son prioritarios.


# 📑 Estructura de datos: 

El conjunto de datos incluye la siguiente información:


| NOMBRE |DESCRIPCIÓN                                          |
|--------|-----------------------------------------------------|
| AÑO    |  Año en que se realizó o estaba programado el vuelo.|
|MES  | Mes del vuelo (1 = enero, 12 = diciembre). |
|DÍA  | Día del mes en que ocurrió el vuelo. |
|DÍA_SEMANA  | Día de la semana (1 = lunes, 7 = domingo). |
| AEROLÍNEA |  Código de la aerolínea que opera el vuelo (ej. AA = American Airlines, WN = Southwest).|
|NÚMERO_VUELO  | Número de vuelo asignado por la aerolínea. |
| NÚMERO_DEL_AVIÓN  | Matrícula única del avión, como la “placa” de un automóvil (ej. N485HA). |
| AEROPUERTO_ORIGEN | Código IATA del aeropuerto desde donde despega el vuelo. |
| AEROPUERTO_DESTINO | Código IATA del aeropuerto donde aterriza el vuelo. |
| SALIDA_PROGRAMADA | Hora programada de salida (formato HHMM). |
| HORA_LLEGADA | Hora real en que el avión llegó al aeropuerto destino. |
|HORA_SALIDA | Hora real en que el avión sale del aeropuerto origen. |
| RETRASO_LLEGADA | Diferencia en minutos entre la hora real de llegada y la programada (positivo = retraso, negativo = adelantado). |
|DESVIADO  | Indica si el vuelo fue desviado a otro aeropuerto (1 = sí, 0 = no). |
|CANCELADO  | Indica si el vuelo fue cancelado (1 = sí, 0 = no). |
| RAZÓN_CANCELACIÓN |Motivo de cancelación: A = sistema aéreo, B = seguridad, C = aerolínea, D = clima.  |
| RETRASO_SISTEMA_AÉREO |Minutos de retraso atribuibles al sistema aéreo (congestión, control de tráfico aéreo).
|RETRASO_SEGURIDAD  |Minutos de retraso por controles o incidentes de seguridad.  |
| RETRASO_AEROLÍNEA | Minutos de retraso atribuibles a la aerolínea (tripulación, mantenimiento, logística interna). |
|RETRASO_AVIÓN_TARDÍO  | Minutos de retraso porque el avión llegó tarde de un vuelo anterior (efecto cascada). |
| RETRASO_CLIMA | Minutos de retraso por condiciones meteorológicas adversas (tormentas, nieve, niebla, viento). |
|TIEMPO_PROGRAMADO|Es la duración estimada del vuelo según el plan de la aerolínea (en minutos)|
|TIEMPO_TOTAL_REAL|Es el tiempo que realmente tomó el vuelo desde la salida hasta la llegada, incluyendo rodaje de salida y rodaje de entrada.|
|TIEMPO_EN_AIRE|Es el tiempo que el avión estuvo efectivamente volando, desde el despegue hasta el aterrizaje.|
|DISTANCIA|Registra la distancia de los vuelos en kilómetros|



# 🖌️ DESCRIPCIÓN 

1.- El dataset contiene más de 5.8 millones de vuelos.

2.- ATL (Atlanta) es el aeropuerto más importante tanto en salidas como en llegadas.

3.- La flota tiene casi 5,000 aviones distintos, pero algunos operan mucho más que otros.

4.- Más del 98% de los vuelos no se cancelan, lo que indica que las cancelaciones son excepcionales.

5.- Análisis para reconocer las variables que influyen en los retrasos graves, para ello se realiza un gráfico de barra que se muestra a continuación:

![Causa más común retraso](images/Causa_mas_comun_de_retraso.png)


**- RETRASO_AVIÓN_TARDÍO** no es una causa primaria, sino más bien un efecto acumulado. Se refiere a los minutos de retraso que un vuelo hereda porque el avión llegó tarde de un vuelo anterior. Ese retraso puede estar explicado por cualquiera de las otras causas:
  -  RETRASO_CLIMA → si el vuelo anterior se demoró por tormenta.
  -  RETRASO_AEROLÍNEA → si hubo problemas operativos o logísticos.
  -  RETRASO_SISTEMA_AÉREO → congestión en el tráfico aéreo.
  -  RETRASO_SEGURIDAD → inspecciones adicionales.

**📊 Interpretación de retrasos por rango de minuto consideradas en el proyecto para evaluar los retrasos graves.**

Esta clasificación no corresponde a un estándar oficial de la industria aérea. Se adopta como convención interna del proyecto, inspirada en prácticas comunes de aerolíneas y autoridades de transporte, para facilitar la interpretación y comunicación de los resultados.


| Categoría de retraso | Rango en minutos | Interpretación |
|----------------------|------------------|----------------|
|Puntualidad aceptada  | 0–15 | Normal, sin impacto significativo |
|Retraso leve  |16–30  | Aún tolerable, frecuente en operaciones |
|Retraso moderado  |31–60  | Ya afecta conexiones y logística |
| Retraso grave |  >60| Impacto fuerte en pasajeros y aerolínea |
|Retraso extremo|>180|Casos excepcionales, suelen implicar compensaciones|

**Factores correlacionados con retrasos superiores a 30 minutos:**

| Retrasos| Correlación|
|----------------|---------------|
|RETRASO_GRAVE|           1.000000|
|||
|RETRASO_AVIÓN_TARDÍO|    0.535315|
|||
|RETRASO_AEROLÍNEA|       0.389211|
|||
|RETRASO_SISTEMA_AÉREO|   0.248072|
|||
|RETRASO_CLIMA|           0.156599|
|||
|LLEGADA_PROGRAMA|        0.109532|
|||
|RETRASO_SEGURIDAD|       0.029881|

- Consistencia absoluta: **RETRASO_AVIÓN_TARDÍO y RETRASO_AEROLÍNEA** son los más fuertes en todos los métodos.
- Diferencias: CatBoost amplifica el rol de **SISTEMA_AÉREO y CLIMA**, lo que sugiere que captura mejor interacciones no lineales.
- Ruido: SEGURIDAD y LLEGADA_PROGRAMA son irrelevantes en todos los enfoques.

El modelo usado para clasificar los retrasos graves corresponde a **"Pipeline de machine learning XGBoost y CatBoost"**:

El pipeline completo incluye:

Entrenamiento de XGBoost y CatBoost con las variables más fuertes: RETRASO_AVIÓN_TARDÍO, RETRASO_AEROLÍNEA, RETRASO_SISTEMA_AÉREO, RETRASO_CLIMA.

Priorizar las dos variables clave (AVIÓN_TARDÍO y AEROLÍNEA).
Explorar interacciones con SISTEMA_AÉREO y CLIMA, que CatBoost detecta mejor.
Creación del ensemble (promedio de probabilidades). Esto suaviza las diferencias y equilibra recall y precisión.

**Rsultados otenidos:**
Evaluación final con el umbral 0.6 (matriz de confusión + reporte).

  ![Matriz_de_confusión](images/Matriz_de_confusion_final.png)

Métricas clave:

Precisión: 0.91 → mide cuántas predicciones positivas fueron correctas.

Recall: 0.90 → mide cuántos retrasos graves fueron detectados.

F1 Score: 0.91 → balance entre precisión y recall.

ROC-AUC: 0.97 → mide la capacidad del modelo para distinguir entre clases.



- Dataset limpio llamado: **flight_clean.csv**

 --- 
 Notebook_flight_on_time.ipynb 
# ✈️FlightOnTime
# PREDICCIÓN DE RETRASOS DE VUELOS

# ✨ Características 

Base de datos: **flight_clean.csv**:

1.- Formato:  Texto plano, filas

2.- Compresión:  Limitada, ocupa más espacio

3.- Lectura/Escritura:  Lento en grandes volúmenes

4.- Estructura:  No guarda tipos de datos, todo es texto

5.- Escalabilidad:  Adecuado para datasets pequeños/medianos

6.- Compatibilidad:  Universal, cualquier programa lo abre

Cuando usar:

**CSV**
- Cuando necesitas máxima compatibilidad (Excel, Notepad, cualquier lenguaje).
  
- Para compartir datos pequeños con usuarios no técnicos.


# 📑 Estructura de datos: 

- Unnamed: 0 → índice automático generado al exportar el archivo (no es una variable relevante).
- ANO → año del vuelo.
- MES → mes del vuelo.
- DIA → día del mes en que se realizó el vuelo.
- DIA_SEMANA → día de la semana (ej. 1 = lunes, 7 = domingo).
- AEROLINEA → código de la aerolínea (ej. AS = Alaska Airlines, AA = American Airlines).
- NUMERO_VUELO → número identificador del vuelo.
- NUMERO_DEL_AVION → matrícula o tail number del avión.
- AEROPUERTO_ORIGEN → código IATA del aeropuerto de salida (ej. ANC = Anchorage).
- AEROPUERTO_DESTINO → código IATA del aeropuerto de llegada (ej. SEA = Seattle).
  
**✈️ Variables de estado del vuelo**
- DESVIADO → indica si el vuelo fue desviado (1 = sí, 0 = no).
- CANCELADO → indica si el vuelo fue cancelado (1 = sí, 0 = no).
- RAZON_CANCELACION → motivo de cancelación (ej. “No Cancelado”, “Clima”, “Seguridad”).

**⏱️ Variables de retraso**
- RETRASO_SISTEMA_AEREO → minutos de retraso atribuibles al sistema aéreo (congestión, control de tráfico).
- RETRASO_SEGURIDAD → minutos de retraso por controles de seguridad.
- RETRASO_AEROLÍNEA → minutos de retraso por causas internas de la aerolínea (tripulación, mantenimiento).
- RETRASO_AVIÓN_TARDÍO → minutos de retraso porque el avión llegó tarde de un vuelo anterior.
- RETRASO_CLIMA → minutos de retraso por condiciones meteorológicas.

 **📈 Variables de resultado**
- HORA_LLEGADA → el dato observado, lo que efectivamente ocurrió.
- LLEGADA_PROGRAMA → hora de llegada programada (en formato decimal de horas).
- RETRASO_GRAVE → indicador binario (0/1) de si el retraso fue considerado grave según el umbral definido (>30 min).

🌌 El dataset combina datos básicos del vuelo, estado operativo (cancelado, desviado) y causas de retraso, lo que permite analizar tanto la puntualidad como los factores que afectan la operación.

**📊 Observaciones principales**

1. Variables más influyentes
- HORA_LLEGADA (51.6%) y LLEGADA_PROGRAMA (40.3%) concentran casi 92% de la importancia total.
  
👉 Esto indica que el modelo depende fuertemente de la hora real y la hora programada de llegada para explicar el fenómeno (probablemente retrasos o puntualidad).

- Estas dos variables dominan el comportamiento del modelo, lo que sugiere que la diferencia entre hora real y programada es el factor crítico.

2. Variables de importancia media
- FRANJA_HORARIA_LLEGADA (4.2%) y FRANJA_LLEGADA_PROGRAMA (2.6%) aportan algo de información adicional.

👉 Refuerzan la idea de que los patrones horarios (mañana, tarde, noche) influyen en la probabilidad de retrasos.

3. Variables con baja influencia
- AEROLINEA (0.53%), MES_PARTIDA (0.21%), AEROPUERTO_DESTINO (0.17%), DISTANCIA (0.08%), AEROPUERTO_ORIGEN (0.07%), TEMPORADA (0.03%), DIA_SEMANA (0.01%), ES_FIN_DE_SEMANA (0.001%).

👉 Estas variables apenas aportan información al modelo. Su peso es marginal y podrían considerarse prescindibles en una versión simplificada.


||Feature Id|	Importances|
|--|-------|----------------|
|0|	HORA_LLEGADA	|51.613366|
|1	|LLEGADA_PROGRAMA|	40.374843|
|2	|FRANJA_HORARIA_LLEGADA|	4.238255|
|3	|FRANJA_LLEGADA_PROGRAMA|	2.640583|
|4	|AEROLINEA	|0.539006|
|5	|MES_PARTIDA	|0.210461|
|6	|AEROPUERTO_DESTINO	|0.172964|
|7	|DISTANCIA	|0.084732|
|8	|AEROPUERTO_ORIGEN	|0.071130|
|9	|TEMPORADA	|0.036600|
|10|	DIA_SEMANA	|0.016485|
|11|	ES_FIN_DE_SEMANA	|0.001576|



# 🖌️ DESCRIPCIÓN 

- El dataset marca como RETRASO_GRAVE = 1 todos los vuelos con más de 30 minutos de retraso, y esa es la etiqueta que el modelo está aprendiendo a predecir.

**🧠 Análisis del modelo elegido:** **CatBoostClassifier**

1. Naturaleza del problema
- El objetivo es predecir si un vuelo tendrá un retraso grave (≥30 min), lo que constituye un problema de clasificación binaria.
- La variable objetivo (RETRASO_GRAVE) se construye a partir de múltiples causas, lo que implica complejidad multivariable.
2. Características del dataset
- Contiene una mezcla de variables categóricas y numéricas:
- Categóricas: aerolínea, aeropuerto, franja horaria, temporada, día de la semana.
- Numéricas: distancia, hora de llegada, mes, etc.
- Muchas variables categóricas tienen alta cardinalidad (ej. aeropuertos, vuelos), lo que puede dificultar el uso de modelos tradicionales como regresión logística o SVM ((Support Vector Machine)).
3. Ventajas de CatBoost

| **Ventaja técnica** | **¿Por qué es relevante aquí?** |
|--|--| 
|✅ Maneja variables categóricas sin necesidad de one-hot encoding|Evita explosión dimensional y simplifica el pipeline|
|✅ Robusto ante datos faltantes|El modelo puede imputar internamente sin perder precisión|
|✅ Evita overfitting con regularización por orden|Ideal para datos con patrones temporales o secuenciales|
|✅ Compatible con early stopping|Permite detener el entrenamiento si no mejora en el set de validación|
|✅ Soporta class_weights|Muy útil para problemas desbalanceados como este (más vuelos sin retraso que con retraso grave)|
|✅ Alta precisión y velocidad|Se adapta bien a entornos operativos con muchos vuelos|

**📈 Evaluación del modelo**

- Se usó un umbral personalizado (0.7912) para ajustar la sensibilidad del modelo.
- 
Se reportaron métricas clave:

- Precisión: 0.76 → mide cuántas predicciones positivas fueron correctas.
- Recall: 0.77 → mide cuántos retrasos graves fueron detectados.
- F1 Score: 0.76 → balance entre precisión y recall.
- ROC-AUC: 0.97 → mide la capacidad del modelo para distinguir entre clases.
  
   ![Curva_ROC](images/Curva_ROC.png)

**🔎 Conclusión técnica**

El modelo CatBoostClassifier fue seleccionado porque responde de manera óptima a las características del problema y del dataset:
1. Manejo eficiente de variables categóricas
- El dataset incluye múltiples variables categóricas de alta cardinalidad (aerolínea, aeropuerto de origen/destino, franjas horarias, temporada).
- CatBoost permite tratarlas directamente sin necesidad de aplicar one-hot encoding, evitando explosión dimensional y pérdida de información.
2. Robustez frente a datos faltantes y ruido
- El modelo maneja valores nulos y realiza imputaciones internas, lo que reduce la necesidad de preprocesamiento adicional.
- Esto es crítico en datos operativos de vuelos, donde los registros pueden estar incompletos.
3. Capacidad para trabajar con clases desbalanceadas
- La proporción de vuelos con retraso grave es menor que la de vuelos sin retraso.
- CatBoost permite ajustar class_weights, mejorando el recall de la clase minoritaria sin sacrificar precisión.
4. Regularización y prevención de overfitting
- El algoritmo utiliza ordered boosting, que reduce el riesgo de sobreajuste en datasets con dependencias temporales.
- Esto es importante en datos de vuelos, donde existen patrones estacionales y semanales.
- Rendimiento en métricas clave
5. El modelo mostró buen desempeño en métricas como ROC-AUC, F1 y recall, lo que indica capacidad para distinguir correctamente entre vuelos con y sin retraso grave.

 
  
- El ajuste de un umbral óptimo (0.7912) permitió balancear precisión y recall según las necesidades operativas.

  ![Matriz_de_confusión](images/confusion_matrix.png)
  
  
**RESUMEN DE LA CONCLUSIÓN**
  
Se eligió CatBoostClassifier porque ofrece un equilibrio técnico entre precisión, interpretabilidad y eficiencia computacional, adaptándose a un dataset con alta heterogeneidad de variables, presencia de datos faltantes y desbalance de clases. Su capacidad de manejar categóricas directamente y optimizar métricas críticas lo convierte en una herramienta adecuada para la predicción de retrasos graves en vuelos.

---
- El RETRASO_GRAVE ='RETRASO_SISTEMA_AEREO','RETRASO_SEGURIDAD',RETRASO_AEROLINEA','RETRASO_AVION_TARDIO','RETRASO_CLIMA'= RETRASO_TOTAL

**- GRÁFICOS QUE AYUDAN A DESCRIBIR LAS VARIABLES SIGNIFICATIVAS EN EL APRENDIZAJE DEL MODELO**
  
**🔍 Análisis comparativo entre aerolíneas:**

📊 Estructura del gráfico
- Eje X: códigos de aerolíneas (ej. AS, AA, DL, UA, etc.).
- Eje Y: minutos de retraso total (hasta 2000 minutos).
Cada boxplot representa:
- Mediana (línea central): el retraso típico.
- Caja: rango intercuartílico (IQR), donde se concentra el 50% de los datos.
- Bigotes: rango extendido sin outliers.
- Puntos individuales: vuelos con retrasos extremos (outliers).


![Distribución_retrasos_erolínea](images/Distribucion_de_retrasos_por_aerolinea.png)

1. Aerolíneas con menor dispersión
- AS (Alaska Airlines) y HA (Hawaiian Airlines) muestran cajas compactas y bajas medianas.
  
👉 Esto sugiere alta puntualidad y pocos retrasos extremos.
2. Aerolíneas con mayor dispersión
- EV, OO, MQ y F9 tienen cajas más altas y muchos puntos fuera del rango.
  
👉 Indican variabilidad alta y presencia frecuente de vuelos con retrasos graves.
3. Outliers frecuentes
- Algunas aerolíneas como UA, AA, DL muestran puntos muy altos (>1000 min).
  
👉 Estos podrían ser vuelos con desvíos, cancelaciones tardías o problemas operativos severos.
4. Comparación de medianas
- La mediana más baja parece estar en HA, mientras que aerolíneas como EV y MQ tienen medianas más elevadas.
  
👉 Esto refleja diferencias estructurales en la operación: rutas más cortas, mejor gestión, o menor congestión.

---
**🔍 Análisis interpretativo de la franja horaria**

📊 Estructura del gráfico
- Eje X: Franja horaria de llegada (Madrugada, Mañana, Tarde, Noche).
- Eje Y: Proporción de vuelos con retraso grave (mayor a 30 minutos), expresada como valor entre 0 y 1.
- Cada barra representa el porcentaje de vuelos en esa franja que sufrieron retrasos graves.


![Proporción_retrasos_graves_por_franja_horaria](images/Proporcion_de_retrasos_graves_por_franja_horaria.png)

1. Madrugada (≈ 0.48)
- Es la franja con mayor proporción de retrasos graves: casi el 48% de los vuelos que llegan en esta franja sufren retrasos significativos.
  
Esto puede deberse a:
- Efecto acumulativo de retrasos del día anterior.
- Menor disponibilidad operativa (menos personal, menos vuelos de respaldo).
- Condiciones climáticas nocturnas más impredecibles.
2. Mañana, Tarde y Noche (< 0.1)
- Estas franjas muestran proporciones mucho menores, todas por debajo del 10%.
  
Esto sugiere que:
- Las operaciones están más estabilizadas durante el día.
- Hay mayor capacidad de respuesta ante imprevistos.
- Los vuelos de la mañana y tarde suelen ser más monitoreados y ajustados.

  ---
  **🔍 Análisis interpretativo de la temporada**
  
📊 Estructura del gráfico
- Eje X: estaciones del año (Verano, Otoño, Invierno, Primavera).
- Eje Y: proporción de vuelos con retraso grave (mayor o igual a 30 minutos), expresada como valor entre 0 y 1.
- Cada barra representa el porcentaje de vuelos en esa estación que sufrieron retrasos significativos

![Proporción_retrasos_graves_por_temporada_horaria](images/Proporcion_de_retrasos_graves_por_temporada.png)
  
🔍 Análisis comparativo
1. Verano y Otoño (≈ 0.11–0.12)
- Estas estaciones muestran las proporciones más altas de retrasos graves.
  
Posibles causas:
- Verano: alta demanda turística, congestión en aeropuertos, mayor número de vuelos.
- Otoño: transición operativa, ajustes de itinerarios, feriados intermedios.
  
2. Invierno y Primavera (< 0.10)
- Proporciones más bajas, aunque no despreciables.
- Invierno: podría esperarse más retrasos por clima, pero quizás hay menos vuelos o mejor planificación.
- Primavera: periodo de recuperación operativa, menos saturación, clima más estable.
---
**🔍 Análisis interpretativo de de los días de la semana**

📊 Estructura del gráfico
- Eje X: días de la semana (Lunes a Domingo).
- Eje Y: proporción de vuelos con retraso grave (mayor a 30 minutos), expresada como valor entre 0 y 1.
- Cada barra representa el porcentaje de vuelos en ese día que sufrieron retrasos graves.

![Proporción_retrasos_graves_por_día](images/Proporcion_de_retrasos_graves_por_dia.png)

🔍 Análisis interpretativo
1. Distribución uniforme
- Las barras son relativamente similares en altura, lo que indica que no hay un día claramente más vulnerable que otro.
- Esto sugiere que los retrasos graves están distribuidos de forma homogénea durante la semana.
2. Ausencia de picos extremos
- No se observan días con proporciones cercanas a 0.2 o superiores.
- Esto indica que el sistema aéreo mantiene una estabilidad operativa sin sobresaltos marcados por día.
3. Ligeras variaciones
- Puede haber pequeñas diferencias entre días hábiles y fines de semana, pero no son significativas en este gráfico.
- Esto podría reflejar una buena planificación semanal por parte de las aerolíneas.

 
# 📂 Archivos del Proyecto 

Parquet y CSV: Archivos que contienen las bases de datos de cada aerolínea.

Jupyter Notebook: Proyecto desarrollado en Google Colaboratory, utilizando Python y bibliotecas como Pandas para realizar el análisis de datos.

# 💻Lenguaje y Bibliotecas Utilizadas 

Lenguaje:

- Python

**📚 Bibliotecas Principales:** 

- Pandas: Manipulación y análisis de datos estructurados.
- NumPy: Trabajo con arrays multidimensionales y cálculos matemáticos.
- Matplotlib: Creación de gráficos y visualizaciones de datos.
- Seaborn: Biblioteca avanzada para visualizaciones estadísticas y estilizadas, ideal para explorar datos y destacar relaciones entre variables.
- XGBoost: Biblioteca de Extreme Gradient Boosting, optimizada para velocidad y rendimiento en clasificación y regresión.
- CatBoost: Biblioteca de Categorical Boosting, especializada en manejar eficientemente variables categóricas y reducir el riesgo de overfitting.


# 💽 Instalación 

Ejecuta el siguiente comando para instalar las bibliotecas necesarias:

pip install pandas numpy matplotlib

# 🚀 Instrucciones para Ejecutar

Clona este repositorio en tu máquina local: ´´´bash
git clone https://github.com/Marion13673/Analisis-ventas-por-tienda.git

Abre el archivo index.html en tu navegador para ver y usar la aplicación.

# 🤝 Contribuciones

💡 ¡Las contribuciones son bienvenidas! Si deseas contribuir a este proyecto, por favor sigue estos pasos:

**Haz un fork del repositorio.**

Crea una rama con tu nueva característica (git checkout -b feature/nueva-caracteristica).

Realiza tus cambios y haz un commit (git commit -m 'Añadir nueva característica').

Envía tu rama al repositorio remoto (git push origin feature/nueva-caracteristica).

Abre una Pull Request.

# 📜 Licencia

📄 Este proyecto está licenciado bajo la Licencia MIT. Consulta el archivo LICENSE para más información.
