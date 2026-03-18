📄 Archivo docker-compose.yml

```bash
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
🔍 Explicación detallada de cada componente
1. 🔢 version: '3.8'
❓ ¿Qué es y para qué sirve?

Especifica la versión del formato de archivo de Docker Compose que se está utilizando 

La versión 3.8 es compatible con Docker Engine 19.03.0+ 

💡 Importancia:

Diferentes versiones soportan diferentes características y sintaxis 🎯

La versión 3.8 incluye soporte para:

⚙️ Configuraciones avanzadas de recursos

📋 Perfiles de servicios

🔗 Mejor manejo de dependencias entre contenedores

🌍 Variables de entorno extendidas

2. 🛠️ services:
❓ ¿Qué hace esta sección?

Define los contenedores que se van a ejecutar como parte de la aplicación 🐳

En este caso, hay un solo servicio llamado pyspark-jupyter 📌

Cada servicio representa un contenedor independiente 📦

💡 Importancia:

Permite definir múltiples servicios que pueden trabajar juntos  🤝

Facilita la orquestación de aplicaciones multicontenedor 🎼

Define cómo cada contenedor debe ser configurado y ejecutado ⚙️

3. 🖼️ image: jupyter/pyspark-notebook:latest
❓ ¿De dónde viene esta imagen?

Es una imagen preconstruida disponible en Docker Hub 🌐

jupyter/ es el usuario/organización oficial en Docker Hub 👤

pyspark-notebook es el nombre específico de la imagen 📛

latest es el tag que indica la versión más reciente ✨

📦 Contenido de la imagen:

📓 Jupyter Notebook / JupyterLab

⚡ Apache Spark preinstalado y configurado

🐍 PySpark para trabajar con Spark desde Python

📊 Python con bibliotecas científicas (NumPy, Pandas, Matplotlib, etc.)

🔧 Kernel de Scala para notebooks

💻 Herramientas de línea de comandos para Spark

🎯 Origen y mantenimiento:

Mantenida oficialmente por el proyecto Jupyter 👨‍💻

Actualizada regularmente con las últimas versiones 🔄

Ampliamente utilizada en entornos académicos y profesionales 🎓

4. 🔌 ports: "8888:8888"
❓ ¿Qué significa el mapeo de puertos?

Formato: "puerto_host:puerto_contenedor" 📍

8888:8888 mapea el puerto 8888 del contenedor al puerto 8888 de tu máquina local 💻

📝 Explicación detallada:

Jupyter corre en el puerto 8888 dentro del contenedor 🏠

Sin mapeo, el servicio estaría aislado e inaccesible 🚫

Con el mapeo, puedes acceder desde tu navegador usando http://localhost:8888 🌐

💡 Importancia:

Permite la comunicación entre el contenedor y el exterior 📡

Facilita el acceso a servicios web dentro del contenedor 🌍

Puedes mapear múltiples puertos si es necesario (ej: 4040 para Spark UI) 🔢

5. 💾 volumes:
```bash
volumes:
  - ./notebooks:/home/jovyan/work/notebooks
  - ./data:/home/jovyan/work/data
```

¿Qué hacen?

Crean un "puente" o montaje entre tu máquina local y el contenedor

Formato: "ruta_en_host:ruta_en_contenedor"

💡Sincronizan archivos entre ambos sistemas en tiempo real

Primer volumen: ./notebooks:/home/jovyan/work/notebooks

Monta la carpeta local ./notebooks en el contenedor

💡Los notebooks que crees se guardarán automáticamente en tu máquina local

Puedes usar tu editor favorito (VS Code, etc.) para editar los notebooks

Segundo volumen: ./data:/home/jovyan/work/data

🔢 Monta la carpeta local ./data en el contenedor

Los archivos de datos (CSV, JSON, etc.) que coloques aquí serán accesibles desde el contenedor

Ideal para datasets que necesitas procesar con Spark

¿Por qué son importantes? (Beneficios clave)

🔢 Persistencia de datos:

Si borras el contenedor, tus notebooks y datos no se pierden

Todo queda guardado en tu máquina local

Compartir archivos bidireccional:

Puedes crear/modificar notebooks desde el contenedor y verlos en tu máquina

Puedes copiar datasets a ./data y el contenedor los verá automáticamente

Control de versiones:

Puedes versionar tus notebooks con git desde tu máquina local

Los cambios se reflejan inmediatamente en ambos lados

Flexibilidad de desarrollo:

Usa Jupyter para ejecutar código

Usa tu editor local para editar

Lo mejor de ambos mundos

Separación de concerns:

Código en ./notebooks

Datos en ./data

Organización clara del proyecto

6. environment: JUPYTER_ENABLE_LAB=yes
¿Para qué sirve esta variable de entorno?

Función principal:

Activa JupyterLab en lugar del clásico Jupyter Notebook

JupyterLab es la interfaz moderna y más completa del proyecto Jupyter

Características de JupyterLab:

✅ Interfaz con múltiples pestañas

✅ Arrastrar y soltar celdas

✅ Vista de archivos integrada

✅ Múltiples kernels en la misma ventana

✅ Extensiones y plugins

✅ Mejor manejo de grandes conjuntos de datos

✅ Terminal integrado

✅ Editor de texto con resaltado de sintaxis

✅ Sistema de paneles divididos


┌─────────────────────────────────────────────────────────┐
│                    TU MÁQUINA LOCAL                      │
│  ┌─────────────────────────────────────────────────────┐ │
│  │  📁 ./notebook  ←→  📓 Jupyter Notebooks           │ │
│  │  📁 ./data       ←→  📊 Datasets                    │ │
│  └─────────────────────────────────────────────────────┘ │
│                      🔌 Puerto 8888                       │
└─────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────┐
│                 CONTENEDOR DOCKER                        │
│  ┌─────────────────────────────────────────────────────┐ │
│  │  🐍 PySpark + JupyterLab                            │ │
│  │  📊 Procesamiento de datos                          │ │
│  │  📓 Notebooks en /home/jovyan/work/notebooks        │ │
│  │  📁 Datos en /home/jovyan/work/data                 │ │
│  └─────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────┘
