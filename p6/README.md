# Práctica 5. Reconocimiento con Deepface

## Tarea 1. Reconocimiento de emociones humanas


En esta práctica se ha hecho uso de deepface para dtectar emociones humanas, en concreto, la más dominante, en fotos con personas posando y con emociones bastante obvias. Sin embargo, se ha notado que deepface no es demasiado bueno detectando emociones debido a que muchas de ellas cuando estaban triste se las detectaba feliz, y viceversa, qué ironía.

El código se divide en 3 partes: obtener todas las imágenes de la carpeta, detectar la emoción y plasmarla en la foto.
En la primera función se recorren todos los archivos de la carpeta.
En la segunda función, se ha hecho uso de un if/elif statement para detectar la emoción dominante de la persona en esa foto:
![image](https://github.com/MinervaQuin/VC/assets/100958927/931eef75-8220-4b33-ba79-7ab3976e00c3)
En la tercera, se hace uso de YOLO para obtener el segmento que rodea a la persona. Con ese segmento, lo utilizamos de mácara para colorear esa zona de un color que represente la emoción que se ha detectado: rojo para el enfado, azul para la tristeza, amarillo para la felicidad, naranja para la sorpresa, verde para el asco, y lila para el miedo.
![image](https://github.com/MinervaQuin/VC/assets/100958927/f2814da4-9c97-48d9-8e8d-f92541d912c3)
En esta función se añade el color a ese segmento de una forma transparente y se añade el texto con la emoción dictada
Por último sólo por motivo estético, pensamos que quedaba bien hallar una máscara con zonas que cumplan con el color de la piel en un rango determinado. Esta mascara colorea esa regiones sin transparencia, dándole un toque artístico, nada más. Por último se muestra la imagen con imshow() de toda la vida.
