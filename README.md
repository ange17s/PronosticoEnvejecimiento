# Estimador de Edad Biológica Facial con Deep Learning

Este repositorio contiene la implementación completa de un sistema de **Regresión de Edad Biológica (Age Regression)** utilizando una **Red Neuronal Convolucional (CNN)** entrenada con TensorFlow/Keras y empaquetada en una aplicación de escritorio interactiva desarrollada con **Flet**.

---

## 📌 Información Técnica y Arquitectura del Proyecto

El proyecto utiliza técnicas de **Visión por Computadora** para predecir la edad biológica a partir de imágenes faciales.

---

## 🧠 Arquitectura del Modelo (CNN)

El modelo principal es una CNN diseñada para regresión continua:

- **Entrada:** Imágenes RGB de `128 × 128 × 3` normalizadas a `[0, 1]`.
- **Capas Convolucionales:**  
  Tres bloques secuenciales:  
  `Conv2D → MaxPooling2D → Dropout(0.25)`
- **Capas Densas:**  
  Después de `Flatten`, una capa densa de **512 neuronas**, activación **ReLU** y **Dropout(0.5)**.
- **Salida:**  
  Una neurona con activación **Lineal** (para regresión).
- **Compilación:**  
  - Optimizador: **Adam**  
  - Pérdida: **MAE (Mean Absolute Error)**

---

## ⚙️ Proceso de Implementación

### 1. Preprocesamiento de Datos
- Se carga el dataset **UTKFace**.  
- La edad se extrae del nombre del archivo.  
- Se recorta el rostro, se redimensiona a `128 × 128` y se normaliza.

### 2. Entrenamiento
- Función de pérdida: **MAE**  
- Técnica: **Early Stopping** con paciencia de 5 épocas  
- Métrica final: **MAE = 8.77 años** en el conjunto de prueba.

### 3. Evaluación
El modelo optimizado proporciona una predicción continua de la edad con buen desempeño general.

### 4. Integración
El modelo entrenado (`aging_estimator_model.keras`) se integra con una app en **Flet** para inferencia en tiempo real.

---

## 🗂️ Estructura de Módulos (Python)

### `preprocesamiento.py`
- Carga y preprocesamiento del dataset  
- Parsing de edad  
- Redimensionamiento y normalización  
- División train/test  

### `entrenamiento.py`
- Define la arquitectura de la CNN  
- Compila el modelo  
- Aplica EarlyStopping  
- Ejecuta `model.fit()`  
- Guarda el modelo en `.keras`

### `main_app.py`
- Implementación de la interfaz gráfica con Flet  

### `logic.py`
- Carga el modelo  
- Maneja la carga de imágenes  
- Ejecuta la inferencia  
- Muestra la predicción  

### `interfaz.py`
- Contiene los elementos visuales de la GUI  

### `generadorimagenes.py`
- Genera gráficos de la pérdida (MAE) durante entrenamiento y validación  

### `requirements.txt`
- Lista completa de dependencias  
- Asegura la compatibilidad del entorno  

---

## 🔄 Flujo de Arquitectura de la Aplicación

### **Flujo Offline (Entrenamiento)**
preprocesamiento.py → entrenamiento.py → aging_estimator_model.keras

### **Flujo Online (Inferencia / App)**
main_app.py ← (carga) ← aging_estimator_model.keras



---

## 🚀 Instrucciones de Instalación y Uso

### 1. Prerrequisitos
Debes tener **Python 3.8 o superior** instalado.

---

### 2. Clonar el Repositorio

```bash
git clone https://github.com/tu-usuario/nombre-del-repositorio.git
cd nombre-del-repositorio

### 3. Se recomienta usar un entorno virtual

# Crear entorno virtual
python -m venv venv

# Activar entorno en Linux/macOS
source venv/bin/activate

# Activar entorno en Windows
.\venv\Scripts\activate

# Instalar dependencias
pip install -r requirements.txt

# Moverse a la carpeta src
cd src

### 4. Obtención del Conjunto de Datos (UTKFace)

El entrenamiento del modelo requiere el dataset UTKFace. Este paso es obligatorio para ejecutar el script de entrenamiento (entrenamiento.py).

Utiliza el comando de clonación para descargar el dataset:

# COMANDO PARA CLONAR EL DATASET UTKFace
git clone [https://github.com/UTKFace/UTKFace_Dataset.git](https://github.com/UTKFace/UTKFace_Dataset.git) data/UTKFace


Asegúrate de que la carpeta de datos se encuentre en la ruta esperada por preprocesamiento.py.

### 5. Ejecución

Entrenar el Modelo (Opcional): Si deseas reentrenar el modelo, ejecuta el script:

python entrenamiento.py


Esto generará o actualizará el archivo aging_estimator_model.keras.

Ejecutar la Aplicación Demo: Para iniciar la interfaz gráfica:

flet run

La aplicación Flet se abrirá, permitiéndote cargar una imagen y recibir la predicción de edad.
