# Práctica 5. Reconocimiento de matrículas

## Tarea 1. Reconocimiento de matrículas sin YOLO entrenado

En esta tarea se ha tenido que buscar la mátricula de un coche y utilizar tesseract para traducir la imagen a string sin entrenar un modelo de yolo anteriormente. Para ello se ha aproximado la localización de la matrícula teniendo en cuenta que va a estar dentro del cuadrado mínimo que rodea a un coche y luego que tiene una forma rectangular.

### Reconocimiento de coches únicamente
El primer paso es detectar los coches de la imagen. Para ello omitimos todas aquellas detecciones cuya clase no coincida con car:
``` python
car_detections = [box for r in results for box in r.boxes if classNames[int(box.cls[0])] == "car"]

# Dibujar las detecciones de la clase "car"
for box in car_detections:
```

### Búsqueda de contornos similar a la matrícula

Habiendo detectado el coche, obtenemos los valores que determinan el rectángulo. Esto nos servirá para crear una imagen a partir de estos y la imagen original. Es en esta imagen donde intentaremos hubicar un rectángulo del tamaño de una matrícula.
``` python
        # Conseguir rectángulo mínimo que contiene al coche
        roi = img[y1:y2, x1:x2]

        # Convertir la ROI a escala de grises
        gray_roi = cv2.cvtColor(roi, cv2.COLOR_BGR2GRAY)

        # Aplicar umbralización
        _, threshold = cv2.threshold(gray_roi, 127, 255, cv2.THRESH_BINARY)

        # Encontrar contornos en la imagen umbralizada
        contours, _ = cv2.findContours(threshold, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)
```
Una vez hecho esto, se pasa la imagen a gris, y se encuentran los contornos. Y vamos buscando por cada contorno aquellos que 

---
## Tarea 2. Entrenamiento de un modelo de YOLOv8

### Selección de imágenes para el entrenamiento
<!--[YOLOv7](#52-yolov7) 
https://platesmania.com/albumlistall.php?start=9

### División del database y entrenamiento por CPU
yolo detect train model=yolov8n.pt data="E:\p5\dataset\paths.yml" imgsz=300 batch=4 device=CPU epochs=40

### Prueba con imágenes
 -->
---
## Incidencias

En el apartado 1, en un primero momento se intentó utilizar la variables confidence para descartar objetos del tipo car que en realidad no lo fueran. Sin embargo, nos dimos cuenta rápidamente que YOLO no detecta demasiado bien ciertos coches, hasta el punto de tener que recortar la imagen para que detectara el que tuviera delante y no una parte lateral de un coche aparcado al lado como el coche principal.
