# Laboratorio-Redes-neuronales-artificiales
Perceptrón multicapa (MLP) con Keras/TensorFlow para clasificar el estado fetal (Cardiotocography, 3 clases) y estimar la humedad absoluta (Air Quality, regresión), evaluado con validación cruzada de 10 folds.
# Redes Neuronales Artificiales: Perceptrón Multicapa (MLP)

Proyecto de la asignatura de Machine Learning en la Universidad de Medellín. Implementa redes
neuronales feed-forward con Keras/TensorFlow para un problema de **clasificación multiclase**
y otro de **regresión**, y compara cómo afectan la arquitectura y el número de épocas
al desempeño y al costo computacional.

## Contenido

### 1. Clasificación: estado fetal (Cardiotocography, UCI)
- **Datos:** 2.126 cardiotocogramas con 21 características de frecuencia cardíaca fetal
  y contracciones uterinas.
- **Objetivo:** predecir el estado fetal NSP (Normal, Sospechoso, Patológico).
- **Preprocesamiento:** One-Hot Encoding de la variable de salida. Se excluye la variable
  `CLASS` para evitar fuga de información.
- **Modelo:** MLP con capa oculta ReLU y salida Softmax (3 neuronas), optimizador Adam y
  pérdida *categorical cross-entropy*.
- **Validación:** K-Fold con 10 particiones.

| Épocas | Capa oculta 1 | Capa oculta 2 | Accuracy (media ± desv.) | Tiempo (s) |
|-------:|--------------:|--------------:|-------------------------:|-----------:|
| 10 | 10 | – | 0.847 ± 0.030 | 46 |
| 30 | 10 | – | 0.869 ± 0.023 | 84 |
| **50** | **10** | **–** | **0.884 ± 0.020** | **132** |
| 10 | 10 | 2 | 0.778 ± 0.024 | 47 |
| 30 | 10 | 2 | 0.778 ± 0.033 | 90 |
| 50 | 10 | 2 | 0.873 ± 0.018 | 136 |

Agregar una segunda capa de solo 2 neuronas genera un cuello de botella. Con pocas épocas,
el modelo solo predice la clase mayoritaria (≈77.8 % de casos "Normal").

### 2. Regresión: humedad absoluta (Air Quality, UCI)
- **Datos:** ~9.300 registros horarios de sensores de calidad del aire.
- **Limpieza:** se eliminan los registros con salida faltante (`-200`) y se imputan con la
  media los faltantes en las características.
- **Modelo:** MLP con capa oculta ReLU y salida lineal, optimizador Adam.
- **Métrica:** Error Cuadrático Medio (ECM) con K-Fold de 10 particiones.

| Épocas | Neuronas ocultas | ECM (media ± desv.) | Tiempo (s) |
|-------:|-----------------:|--------------------:|-----------:|
| 10 | 10 | 432.49 ± 1101.61 | 66 |
| 10 | 20 | 68.51 ± 79.87 | 66 |
| **100** | **10** | **61.12 ± 73.08** | **443** |

Aumentar las neuronas reduce el error a una fracción del costo que implica aumentar las épocas.

## Tecnologías
Python · NumPy · pandas · scikit-learn · Keras · TensorFlow · Matplotlib · Google Colab

## Ejecución
1. Abre `Proyecto_sobre_RNA.ipynb` en Google Colab.
2. Sube `DB_Fetal_Cardiotocograms.txt` y `AirQuality.data` a `/content/`.
3. Ejecuta las celdas en orden.

## Créditos
Guía del laboratorio: Prof. Antonio Tamayo Herrera, Universidad de Medellín.
Datos: [UCI Machine Learning Repository](https://archive.ics.uci.edu/).
