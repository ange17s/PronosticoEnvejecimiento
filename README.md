🧬 Estimador de Edad Biológica Facial con Deep Learning

Este repositorio contiene la implementación completa de un sistema de Regresión de Edad Biológica (Age Regression) basado en Visión por Computadora, utilizando una Red Neuronal Convolucional (CNN) desarrollada con TensorFlow/Keras, integrada en una aplicación de escritorio construida con Flet.

📌 Descripción General

El proyecto estima la edad biológica facial a partir de una imagen, utilizando un modelo de Deep Learning entrenado con el dataset UTKFace.
Incluye todo el pipeline completo:

Preprocesamiento de datos

Entrenamiento con EarlyStopping

Evaluación del modelo

Aplicación de escritorio interactiva con Flet

Visualización de métricas de entrenamiento

🧠 Arquitectura del Modelo (CNN)

El modelo implementado es una CNN para regresión continua, con la siguiente estructura:

Entrada: imágenes RGB de 128 × 128 × 3, normalizadas.

Bloques Convolucionales:
Tres bloques:
Conv2D → MaxPooling2D → Dropout(0.25)

Capa densa oculta:

512 neuronas

Activación ReLU

Dropout(0.5)

Salida:

1 neurona con activación lineal

Compilación:

Optimizador: Adam

Pérdida: MAE (Mean Absolute Error)

🔧 Proceso de Implementación
1. Preprocesamiento

Carga de imágenes del dataset UTKFace

Extracción de la edad desde el nombre del archivo

Detección y recorte de rostro

Redimensionamiento a 128×128

Normalización

División en train / test

2. Entrenamiento

Uso de MAE como función de pérdida

EarlyStopping con paciencia = 5 (monitorizando val_loss)

Registro del historial de pérdidas

Guardado del modelo en:
aging_estimator_model.keras

3. Evaluación

El modelo final alcanza un MAE ≈ 8.77 años en test.

4. Integración con Flet

El modelo entrenado se integra en una app que permite:

Cargar imágenes

Procesarlas

Mostrar la predicción de edad biológica

📂 Estructura del Proyecto
📁 proyecto
 ├── 📁 data
 ├── 📁 src
 │    ├── preprocesamiento.py
 │    ├── entrenamiento.py
 │    ├── logic.py
 │    ├── interfaz.py
 │    ├── generadorimagenes.py
 │    └── main_app.py
 ├── aging_estimator_model.keras
 ├── requirements.txt
 └── README.md

Descripción de Módulos
Archivo	Descripción
preprocesamiento.py	Carga, limpieza y preparación del dataset (recorte, resize, normalización, labels).
entrenamiento.py	Construcción del modelo, entrenamiento, EarlyStopping y guardado del modelo.
logic.py	Inferencia: carga del modelo, procesar imagen y predecir edad biológica.
interfaz.py	Componentes visuales de la interfaz Flet.
main_app.py	Lógica principal de la aplicación Flet.
generadorimagenes.py	Gráficas de entrenamiento (MAE train/validation).
requirements.txt	Bibliotecas necesarias del proyecto.
🔄 Flujo de Arquitectura
🔹 Offline (Entrenamiento)
preprocesamiento.py → entrenamiento.py → aging_estimator_model.keras

🔹 Online (Aplicación)
aging_estimator_model.keras → main_app.py (App Flet)

🚀 Instalación y Uso
1. Prerrequisitos

Python 3.8+

2. Clonar el Repositorio
git clone https://github.com/tu-usuario/nombre-del-repositorio.git
cd nombre-del-repositorio

3. Crear y Activar Entorno Virtual
python -m venv venv


Linux/macOS

source venv/bin/activate


Windows

.\venv\Scripts\activate


Instalar dependencias:

pip install -r requirements.txt


Moverse a la carpeta de código:

cd src

4. Descargar el Dataset UTKFace
git clone https://github.com/UTKFace/UTKFace_Dataset.git data/UTKFace


Asegúrate de que la ruta coincida con lo indicado en preprocesamiento.py.

5. Ejecutar
🔧 Entrenar el modelo (opcional)
python entrenamiento.py


Esto generará o actualizará aging_estimator_model.keras.

🖥️ Ejecutar la aplicación Flet
flet run


Se abrirá la interfaz gráfica donde podrás cargar una foto y obtener la predicción.

🏁 Estado: Proyecto Funcional y Extensible

La arquitectura modular permite:

Reentrenar el modelo

Cambiar datasets

Modificar la interfaz

Exportar a aplicaciones móviles (Android/iOS) usando Fletndows Packaging Guide](https://flet.dev/docs/publish/windows/).
