# Pipeline de Transformación de Datos con PySpark

Proyecto práctico de ingeniería de datos desarrollado con **PySpark**, orientado a la transformación, integración y almacenamiento de información.

El flujo procesa dos fuentes CSV, aplica limpieza y transformaciones, integra los datos mediante `customer_id`, genera agregaciones y almacena los resultados utilizando **Hive, HDFS, Parquet y CSV**.

## Tecnologías

- Python
- PySpark
- Apache Spark
- Apache Hadoop
- HDFS
- Hive
- Docker
- JupyterLab

## Flujo del proyecto

```text
CSV
 ↓
PySpark
 ↓
Transformación y limpieza
 ↓
Join y filtrado
 ↓
Agregaciones
 ↓
Hive / HDFS
 ↓
Parquet / CSV
```

Entre las principales operaciones realizadas se encuentran:

- transformación de fechas;
- creación de variables temporales;
- renombrado y eliminación de columnas;
- integración de DataFrames;
- filtrado de transacciones;
- agregaciones por cliente, trimestre y año;
- clasificación de transacciones de alto valor;
- persistencia de resultados en Hive y HDFS.

## Entorno

El proyecto utiliza Docker Compose para levantar un entorno reproducible compuesto por:

```text
Jupyter + PySpark
        │
        ▼
      HDFS
   ┌────┴────┐
NameNode   DataNode
```

## Ejecución

Crea un archivo `.env` a partir de `.env.example` y configura las fuentes de datos.

Luego ejecuta:

```bash
docker compose up --build -d
```

JupyterLab estará disponible en:

```text
http://localhost:8888
```

El notebook principal se encuentra en:

```text
notebooks/proyecto_final_pyspark.ipynb
```

## Objetivo

Este proyecto forma parte de mi portafolio de Ingeniería de Datos y demuestra el uso de PySpark para procesamiento distribuido, transformación de datos e integración con tecnologías del ecosistema Hadoop.
