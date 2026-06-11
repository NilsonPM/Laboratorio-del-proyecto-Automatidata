# Proyecto Automatidata — Análisis de Taxis Amarillos de NYC (2017)

Este repositorio contiene la fase inicial del proyecto de consultoría de datos desarrollado por **Automatidata** para la **Comisión de Taxis y Limusinas de la Ciudad de Nueva York (NYC TLC)**. El objetivo principal es inspeccionar, limpiar y preparar el conjunto de datos de viajes de taxi del año 2017 para construir un modelo predictivo que estime las tarifas de taxi de manera precisa.

El proyecto está estructurado bajo el marco de resolución de problemas **PACE** (*Planear, Analizar, Construir y Ejecutar*).

---

## 📋 Estructura del Repositorio

* **[Automatidata_Laboratorio_Python_ES.ipynb](Automatidata_Laboratorio_Python_ES.ipynb)**: Cuaderno de Jupyter estructurado con el código en Python para la exploración, filtrado y primeras estadísticas descriptivas del conjunto de datos.
* **[2017_Yellow_Taxi_Trip_Data.csv](2017_Yellow_Taxi_Trip_Data.csv)**: Conjunto de datos en formato CSV con 22,699 registros y 18 columnas que detallan los viajes de taxi.
* **[images/](images/)**: Recursos visuales que ilustran el flujo y las etapas metodológicas de PACE utilizadas en el proyecto.

---

## 📊 Diagnóstico y Estadísticas Clave de los Datos

Tras inspeccionar el dataset de 2017, se identificaron los siguientes aspectos relevantes de calidad de datos (EDA):

* **Completitud:** El dataset consta de **22,699 filas y 18 variables**, con un 100% de registros completos (cero valores nulos).
* **Distribución de Proveedores (VendorID):**
  * `VendorID 2` (Verifone): **12,626** viajes (55.6%)
  * `VendorID 1` (Creative Mobile Technologies): **10,073** viajes (44.4%)
* **Métodos de Pago (payment_type):**
  * Tarjetas de Crédito (`1`): **15,265** viajes. Promedio de propina de **$2.73**.
  * Efectivo (`2`): **7,267** viajes. Promedio de propina de **$0.00** *(Nota: Las propinas en efectivo no se registran en los sistemas electrónicos de la TLC)*.
  * Otros métodos (Sin cargo/Disputas): **167** viajes.

---

## ⚠️ Anomalías Detectadas (Valores Atípicos)

Para asegurar el **rigor analítico**, se identificaron las siguientes inconsistencias en el conjunto de datos que deben ser tratadas antes de entrenar un modelo predictivo:

1. **Tarifas Negativas:** Se detectaron 14 viajes con cobros negativos (mínimo de `-$120.30`), representando devoluciones o disputas de cobro.
2. **Distancias en Cero:** 148 registros registran una distancia de viaje de `0.0` millas a pesar de tener cobros positivos en la tarifa.
3. **Duraciones de Viaje Incoherentes:**
    * Hay 1 viaje con duración negativa (`-16.98 minutos`) por errores en el ingreso de marcas de tiempo.
    * 26 viajes registran una duración de `0.0` minutos.
    * Varios viajes presentan duraciones de hasta `24 horas`, probablemente debido a taxímetros abiertos o fallas del sistema.

---

## 🚀 Próximos Pasos y Plan de Acción

* **Limpieza de Datos:** Eliminar registros atípicos (tarifas negativas, distancias $\le 0$ y duraciones incoherentes).
* **Ingeniería de Características:** Convertir las marcas de tiempo (`tpep_pickup_datetime` y `tpep_dropoff_datetime`) a tipos de datos `datetime` para extraer variables temporales de valor como la hora del día, el día de la semana y la duración real en minutos.
* **Modelado Predictivo:** Utilizar las variables predictoras clave `trip_distance` y la duración estimada del trayecto para predecir la tarifa base (`fare_amount`), excluyendo propinas y peajes opcionales.

---

## 🛠️ Requisitos e Instalación

Para ejecutar el cuaderno de análisis localmente, asegúrate de tener instalado Python 3.x y las siguientes librerías de manipulación de datos:

```bash
pip install pandas numpy
```

Abre tu entorno de Jupyter Notebook o JupyterLab y ejecuta [Automatidata_Laboratorio_Python_ES.ipynb](Automatidata_Laboratorio_Python_ES.ipynb).
