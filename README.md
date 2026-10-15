# Reto Mechatronics AI: detector de objetos en vivo

Proyecto desarrollado en equipo para el reto **Mechatronics AI** del **Hack Knights IA Challenge 2026** (8–10 de octubre de 2026), donde obtuvo el **3.er lugar**.

El código completo, el modelo entrenado y el conjunto de prueba están en el repositorio del equipo:
**https://github.com/issxccrrll/mechatronics-ai**

## Descripción

Sistema que detecta en vivo, desde una webcam o la cámara de un celular, cinco clases de objetos: **taza, botella, tijeras, destornillador y celular**. Cualquier otro objeto se marca como `desconocido` y nunca recibe una clase oficial. El sistema se ejecuta en CPU.

## Cómo funciona

```
Cámara (hilo) → Detector (YOLO11n) → Verificador (opcional) → Filtros → Interfaz + registro CSV
```

- **Modelo:** YOLO11n con transfer learning, entrenado con fotos tomadas con la misma webcam de la demostración.
- **Inferencia en CPU:** el modelo se exporta a OpenVINO para ganar velocidad.
- **Filtros contra falsos positivos:** rechazo de objetos desconocidos, umbral de confianza por clase, filtro de área y proporción, y persistencia de la detección en varios cuadros con seguimiento ByteTrack.

## Resultados

| Medición | Valor |
|---|---|
| mAP50 global en test (471 imágenes) | 0.74 |
| Inferencia con OpenVINO | ~47.6 FPS |
| Pipeline completo en vivo | 16–30 FPS (el reto exigía 15) |

## Tecnologías

- Python
- YOLO11 (Ultralytics)
- OpenVINO
- OpenCV

## Cómo ejecutarlo

Requiere Python 3.11 y Git. En PowerShell:

```powershell
git clone https://github.com/issxccrrll/mechatronics-ai.git
cd mechatronics-ai
py -3.11 -m venv venv
.\venv\Scripts\Activate.ps1
pip install torch torchvision --index-url https://download.pytorch.org/whl/cpu
pip install -r requirements.txt
python main.py --source 0
```

El modelo ya viene incluido en el repositorio. Para salir de la ventana, presiona `q`. Las instrucciones detalladas están en el README del repositorio del equipo.

## Mi rol

Desarrollador del equipo, en la elaboración del sistema con YOLO y los scripts en Python.

## Reconocimiento

3.er lugar en el reto Mechatronics AI, hackathon Hack Knights IA Challenge 2026.

Se usaron asistentes de IA como apoyo en el desarrollo y la documentación; el código fue revisado y probado por el equipo.
