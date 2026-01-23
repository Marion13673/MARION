# ✈️FlightOnTime
# VARIABLES EXPLICATIVAS DE LAS CAUSAS

# INTRODUCCIÓN 🚀

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



# Características ✨

Manipular datos en **flights2015.parquet**, contribuye a mejorar:

1.- Formato:Binario, columnas

2.- Compresión:Alta compresión, ocupa mucho menos

3.- Lectura/Escritura:Optimizado para lectura selectiva

4.- Estructura:Mantiene tipos (int, float, string, etc.)

5.- Escalabilidad:Ideal para big data y sistemas distribuidos

6.- Compatibilidad:Requiere librerías (pandas, pyarrow, spark)

# Estructura de datos: 📑

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



# DESCRIPCIÓN 🖌️

1.- El dataset contiene más de 5.8 millones de vuelos.

2.- ATL (Atlanta) es el aeropuerto más importante tanto en salidas como en llegadas.

3.- La flota tiene casi 5,000 aviones distintos, pero algunos operan mucho más que otros.

4.- Más del 98% de los vuelos no se cancelan, lo que indica que las cancelaciones son excepcionales.

5.- Análisis para reconocer las variables que influyen en los retrasos graves, para ello se realiza un gráfico de barra que se muestra a continuación:

📘 [Causa_más_común_retraso](images/Causa%20más%20común%20retraso.png)

 

Análisis del desempeño geográfico Se utiliza los datos de latitud (lat) y longitud (lon) para mapear las ventas de cada tienda y analizar la distribución geográfica de los productos vendidos.

Generando gráfico Se generarón tres gráficos:

Gráfico de torta que visualiza la distribución de los ingresos por ventas en cada tienda.
Gráfico de línea de tiempo "Tendencia de las categoría de los ingresos por venta y año" y " Tendencia de las cantidades vendidas por categorías y año".
Gráfico de heatmaps que visualiza los ingresos por ventas por zona geográfica limitada por año.
CONCLUSIÓN 💿

Análisis detallado basádose en los resultados obtenidos en las 4 tiendas en los ingresos por ventas, cantidades vendidas, costos incurridos en el envío de los productos a los clientes, calificación promedio de satisfacción que los clientes tienen acerca de cada tienda y producto vendido, como un mapeo acercá de la zona geográfica a la cual venden más y obtienen mayores ingresos. De tal foma de entregar una conclusión consistente a qué tienda se debe cerrar de acuerdo a los resultados obtenidos.

Archivos del Proyecto 📂

CSV: Archivos que contienen las bases de datos de cada tienda, utilizados para el análisis.
Jupyter Notebook: Proyecto desarrollado en Google Colaboratory, utilizando Python y bibliotecas como Pandas para realizar el análisis de datos.
Lenguaje y Bibliotecas Utilizadas 💻

Lenguaje:

Python
Bibliotecas Principales:

Pandas: Manipulación y análisis de datos estructurados.
NumPy: Trabajo con arrays multidimensionales y cálculos matemáticos.
Matplotlib: Creación de gráficos y visualizaciones de datos.
Seaborn: Biblioteca avanzada para visualizaciones estadísticas y estilizadas, ideal para explorar datos y destacar relaciones entre variables.
Instalación 💽

Ejecuta el siguiente comando para instalar las bibliotecas necesarias:

pip install pandas numpy matplotlib

**Instrucciones para Ejecutar** 🚀

Clona este repositorio en tu máquina local: ´´´bash
git clone https://github.com/Marion13673/Analisis-ventas-por-tienda.git
Abre el archivo index.html en tu navegador para ver y usar la aplicación.

**Contribuciones** 🤝

💡 ¡Las contribuciones son bienvenidas! Si deseas contribuir a este proyecto, por favor sigue estos pasos:

**Haz un fork del repositorio.**
Crea una rama con tu nueva característica (git checkout -b feature/nueva-caracteristica).
Realiza tus cambios y haz un commit (git commit -m 'Añadir nueva característica').
Envía tu rama al repositorio remoto (git push origin feature/nueva-caracteristica).
Abre una Pull Request.

**Licencia** 📜

📄 Este proyecto está licenciado bajo la Licencia MIT. Consulta el archivo LICENSE para más información.
