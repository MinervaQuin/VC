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
Una vez hecho esto, se pasa la imagen a gris, y se encuentran los contornos. Y vamos buscando por cada contorno aquellos que coinciden por area > 1000 y la relación anchura por altura mayor a 3.


---
## Tarea 2. Entrenamiento de un modelo de YOLOv8

### Selección de imágenes para el entrenamiento
Para entrenar un modelo de YOLOv8 se tiene que crear un database y repartirlo en 3 carpetas (test, val y train). A su vez estas imagenes tienen que tener un archivo txt asociado estableciendo la clase o clases (en este caso soo una clase: plate) y las coordenadas del objeto y la imagen.
Se ha intentado elegir imágenes que dejasen seleccionar la matrícula con un rectángulo. Cuyo angulo no fuera incómodo, y no dejase demasiado del coche que no fuera una matrícula dentro del rectángulo. Osea, imágenes frontales y con poco ángulo.
Para hallar imágenes fuimos a la página [platesmania](https://platesmania.com/albumlistall.php?start=9) y descargamos alrededor de 350 imágenes. 
![Platesmania](https://github.com/MinervaQuin/VC/assets/100958927/61a12ccd-a43f-430c-aa72-34d9131af092)


Para etiquetar cada imagen se ha utilizado [labelImg](https://github.com/HumanSignal/labelImg), un programa que te deja crear el txt directamente para la utilización de YOLO sin tener que modificarlo.


### División del database y entrenamiento por CPU
Una vez terminada la selección de imágenes, y una vez clasificada entre las carpetas train, val y test, procedemos a entrenar a yolo. En este caso elegimos el modelo principal "yolov8n.pt". También le indicamos el archivo yml, en este caso llamado "path.yml" indicando los directorios de donde se carga el dataset, el número de clases, etc. se ha entrenado este modelo nuevo sólo con CPU y con los valores estándares.

```
yolo detect train model=yolov8n.pt data="E:\p5\dataset\paths.yml" imgsz=300 batch=4 device=CPU epochs=40
```

### Resultado con imágenes
Cuando observamos los resultado después del entrenamiento, podemos ver como la curva de confianza crece exponencialmente hasta quedarse en un valor de 1 constante. El dataset no era demasiado grande y sin embargo los resultados son muy buenos. También hay que tener en cuenta que ya estamos utilizando un modelo preentrenado:
![P_curve](https://github.com/MinervaQuin/VC/assets/100958927/40a1e07d-f53f-404a-ab2d-f4ddd9aaeda0)
Y como observamos tiene muy buenos resultados comparando el training vs val:

![train_batch1230](https://github.com/MinervaQuin/VC/assets/100958927/3de37f06-ebd6-49a3-b55c-64a466005b90)

![val_batch0_labels](https://github.com/MinervaQuin/VC/assets/100958927/01a8bec0-e0e5-4be8-a33e-8caa8bed1066)


---
## Incidencias

En el apartado 1, en un primero momento se intentó utilizar la variables confidence para descartar objetos del tipo car que en realidad no lo fueran. Sin embargo, nos dimos cuenta rápidamente que YOLO no detecta demasiado bien ciertos coches, hasta el punto de tener que recortar la imagen para que detectara el que tuviera delante y no una parte lateral de un coche aparcado al lado como el coche principal.
