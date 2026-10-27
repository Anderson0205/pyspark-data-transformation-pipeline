# Pipeline de Transformación e Integración de Datos con PySpark

Proyecto práctico de ingeniería de datos orientado al procesamiento, transformación, integración y persistencia de información mediante Apache Spark y PySpark.

La solución procesa dos fuentes de datos en formato CSV, aplica transformaciones utilizando la API de DataFrames, integra la información mediante una clave común, genera agregaciones y almacena los resultados utilizando Hive, HDFS, Parquet y CSV.

El entorno completo se ejecuta mediante Docker para proporcionar una configuración reproducible de PySpark y Hadoop sin depender de instalaciones locales de Spark.

## Arquitectura

```text
Fuentes CSV remotas
        │
        ▼
Almacenamiento temporal
        │
        ▼
      PySpark
        │
        ├── Limpieza y transformación
        ├── Variables temporales
        ├── Integración mediante joins
        ├── Filtrado
        └── Agregaciones
        │
        ▼
   Persistencia
        │
        ├── Hive
        │     ├── customer_totals
        │     └── quarterly_averages
        │
        └── HDFS
              ├── Parquet
              │   └── filtered_data
              │
              └── CSV
                  └── total_value_per_year
```

## Tecnologías utilizadas

- Python 3.10
- Apache Spark 4.2.0
- PySpark
- Spark SQL
- Apache Hadoop 3.5.0
- HDFS
- Hive
- Parquet
- JupyterLab
- Docker
- Docker Compose

## Procesamiento realizado

El flujo implementado contempla:

- carga de datasets desde fuentes externas;
- inspección y validación de esquemas;
- conversión de columnas de fecha;
- obtención de año y trimestre;
- renombrado de columnas;
- eliminación de atributos innecesarios;
- integración de DataFrames mediante `customer_id`;
- filtrado de transacciones según monto;
- agregaciones por cliente;
- clasificación de transacciones de alto valor;
- cálculo de promedios trimestrales;
- cálculo de totales anuales;
- persistencia de resultados en Hive;
- almacenamiento de información en HDFS;
- exportación en formatos Parquet y CSV.

## Entorno Docker

El proyecto utiliza tres servicios principales:

```text
Docker Compose
│
├── notebook
│   ├── Python
│   ├── PySpark
│   ├── Java
│   └── JupyterLab
│
├── namenode
│   └── Hadoop HDFS
│
└── datanode
    └── Hadoop HDFS
```

La información de HDFS se mantiene mediante volúmenes Docker persistentes.

## Estructura del proyecto

```text
pyspark-data-transformation-project/
├── docker/
│   └── hadoop/
│       ├── core-site.xml
│       └── hdfs-site.xml
├── notebooks/
│   └── proyecto_final_pyspark.ipynb
├── .dockerignore
├── .env.example
├── .gitignore
├── docker-compose.yml
├── Dockerfile
├── README.md
└── requirements.txt
```

## Configuración

Las URLs utilizadas para obtener los datasets se gestionan mediante variables de entorno.

Crea un archivo `.env` a partir de `.env.example`:

```env
DATASET_1_URL=
DATASET_2_URL=
```

El archivo `.env` no forma parte del repositorio.

## Ejecución

Construir el entorno por primera vez:

```bash
docker compose up --build -d
```

En ejecuciones posteriores:

```bash
docker compose up -d
```

Comprobar los servicios:

```bash
docker compose ps
```

JupyterLab estará disponible en:

```text
http://localhost:8888
```

La interfaz web del NameNode estará disponible en:

```text
http://localhost:9870
```

## Resultados almacenados

El proyecto genera dos tablas mediante Hive:

```text
customer_totals
quarterly_averages
```

Además, almacena en HDFS:

```text
/data/filtered_data
/data/total_value_per_year
```

El primer conjunto se almacena en formato Parquet y el segundo en formato CSV.

## Validación en HDFS

Los resultados pueden verificarse desde el NameNode:

```bash
docker compose exec namenode hdfs dfs -ls /data
```

## Detener el entorno

```bash
docker compose down
```

Los volúmenes de HDFS se conservan entre ejecuciones.

Para eliminar también los volúmenes:

```bash
docker compose down -v
```

> Este último comando elimina los datos persistidos en HDFS.

## Propósito

Este proyecto forma parte de mi portafolio de Ingeniería de Datos y tiene como objetivo demostrar el uso práctico de PySpark para procesamiento distribuido, transformación de información, integración de fuentes y persistencia sobre tecnologías del ecosistema Hadoop.
