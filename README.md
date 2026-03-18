# 📊 Parcial 1 - Análisis Exploratorio con PySpark

Repositorio del **Parcial 1 de Machine Learning**, donde se realiza un **Análisis Exploratorio de Datos (EDA)** utilizando **PySpark**, ejecutado en un entorno **Docker + JupyterLab**.

El objetivo es analizar un dataset de canciones de Spotify utilizando herramientas de procesamiento de datos a gran escala.

```bash

# 📁 Estructura del repositorio
parcial1-pyspark-usuario/
│
├── docker-compose.yml
├── README.md
│
├── data/
│ └── spotify_songs.csv
│
└── notebooks/
└── analisis_exploratorio.ipynb
```
**Descripción de carpetas**

| Carpeta | Descripción |
|--------|-------------|
| `data/` | Contiene el dataset utilizado para el análisis |
| `notebooks/` | Notebook con todo el análisis exploratorio realizado en PySpark |
| `docker-compose.yml` | Configuración del entorno Docker |
| `README.md` | Documentación del proyecto |

---

# 🐳 Infraestructura con Docker

El proyecto utiliza **Docker Compose** para crear un entorno reproducible con:

- Python
- PySpark
- JupyterLab
- Librerías de análisis de datos

Esto permite ejecutar el análisis **sin instalar dependencias manualmente**.

---

# 📄 Archivo `docker-compose.yml`

```yaml
version: '3.8'

services:
  pyspark-jupyter:
    image: jupyter/pyspark-notebook:latest
    container_name: pyspark_parcial1
    ports:
      - "8888:8888"
    volumes:
      - ./notebooks:/home/jovyan/work/notebooks
      - ./data:/home/jovyan/work/data
    environment:
      - JUPYTER_ENABLE_LAB=yes
```

🔍 Explicación de cada componente
1️⃣ version: '3.8'

Define la versión del formato de Docker Compose que se está utilizando.

La versión 3.8 es compatible con versiones modernas de Docker Engine y permite usar configuraciones avanzadas.

🔍Importancia

1. Define la sintaxis disponible

2. Habilita funcionalidades avanzadas

3. Mantiene compatibilidad con Docker

2️⃣ services

La sección services define los contenedores que se ejecutarán como parte del proyecto.

En este caso se define un único servicio:
```bash
pyspark-jupyter
```

Este servicio ejecuta el entorno de trabajo con PySpark y JupyterLab.

Ventajas

1.Permite ejecutar múltiples contenedores

2. Facilita la orquestación de servicios

3. Define cómo se ejecuta cada contenedor

4️⃣ ports: 8888:8888

Define el mapeo de puertos entre el contenedor y la máquina local.

Formato:
```bash
puerto_host : puerto_contenedor
```
En este caso:
```bash
8888:8888
```

Significa que el puerto 8888 del contenedor se conecta con el puerto 8888 de tu computadora.

Esto permite acceder a Jupyter desde el navegador:
```bash
http://localhost:8888
```


5️⃣ volumes

volumes:

```bash
  - ./notebooks:/home/jovyan/work/notebooks
  - ./data:/home/jovyan/work/data
```
Los volumes conectan carpetas de tu computadora con el contenedor.

Formato:

ruta_local : ruta_contenedor

📁 Primer volumen

```bash
./notebooks → /home/jovyan/work/notebooks
```
Guarda los notebooks del proyecto.

Los archivos se almacenan directamente en tu computadora.

📁 Segundo volumen

```bash
./data → /home/jovyan/work/data
```
Contiene los datasets utilizados en el análisis.

Los archivos colocados en esta carpeta pueden ser leídos por Spark dentro del contenedor.

📁¿Por qué son importantes los volumes?

1. Persistencia de datos

- Si el contenedor se elimina, los archivos no se pierden.

- Todo queda guardado en tu computadora.

2. Sincronización automática

- Los cambios hechos en el contenedor aparecen en tu máquina y viceversa.

3. Control de versiones

- Los notebooks pueden ser versionados con Git.

6️⃣ environment

```bash
JUPYTER_ENABLE_LAB=yes
```
Esta variable activa JupyterLab en lugar del Jupyter Notebook clásico.

-Ventajas de JupyterLab

1.Interfaz moderna

2. Soporte para múltiples pestañas

3. Explorador de archivos integrado

4. Terminal dentro del navegador

5. Editor de código avanzado

6. Mejor manejo de proyectos

⚙️ Cómo ejecutar el proyecto

1️⃣ Clonar el repositorio
```bash
git clone https://github.com/chechitoooo/parcial1-pyspark-usuario
```
2️⃣ Entrar al directorio

```bash
cd parcial1-pyspark-usuario
```
3️⃣ Ejecutar Docker Compose

```bash
docker-compose up
```

4️⃣ Abrir en el navegador
```bash
http://localhost:8888
```

🖥️ Arquitectura del entorno

```bash
TU COMPUTADORA
│
├── notebooks/
│     └── analisis_exploratorio.ipynb
│
├── data/
│     └── spotify_songs.csv
│
└── Puerto 8888
        ↓
CONTENEDOR DOCKER
│
├── PySpark
├── JupyterLab
├── Notebooks → /home/jovyan/work/notebooks
└── Datos → /home/jovyan/work/data
```
