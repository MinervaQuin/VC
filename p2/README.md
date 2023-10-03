# VC
En el cuaderno que se adjunta en la carpeta se adjuntas todas las tareas que se han pedido para la práctica 2 de la asignatura Visión por Computador

### Tarea: Realiza la cuenta de píxeles blancos por filas, determina el máximo para filas y columnas (uno para cada) y muestra el número de valores que superan en cada caso 0.95*máximo.
Para la primera tarea, se ha utilizado la función reduce() y cambiado el argumento de 0 a 1, para que contase por filas. Luego se ha normalizado al valor maximo del pixel y se ha utilizado np.max() para hallar el valor máximo tanto en filas como en columnas.
Luego se ha calculado el umbral (0.54*max_value) y contado la cantidad de filas y columnas que superan ese valor respectivamente.
A continuación, se han obtenido las filas y las columnas que superaban esos valores para poder dibujarlas en la gráfica. Copiamos canny para poder dibujar las lineas encima.
Por último, pasamos por todas las filas y las columnas que superaban el valor y dibujamos en la imagen una linea por cada fila y col.


### Tarea: Elige otra imagen, muestra el contenido de alguna de las imágenes resultado de Sobel antes y después de ajustar la escala
Para la segunda tarea, solo hemos tenido que añadir la siguiente línea: cv2.convertScaleAbs(sobel), para mostrar sobelx y sobely correctamente ajustadas y combinadas.

### Tarea: Aplica umbralizado a la imagen resultante de Sobel (valores 0 a 255 y convertida a 8 bits por ejemplo sobel8 = np.uint8(sobel)), y posteriormente realiza el conteo por filas y columnas similar al realizado en el ejemplo con la salida de Canny. Calcula los máximos por filas y columnas, y determina las filas y columnas por encima del 0.95*máximo. Remarca con alguna primitiva gráfica dichas filas y columnas sobre la imagen ¿Cómo se comparan los resultados obtenidos a partir de Sobel y Canny?
Para la tercera tarea, se ha cogido la nueva imagen y se han calculado de nuevo los gradientes x e y, y luego combinado. A continuación se ha convertido esto a 8bits, a lo que llamaremos sobel8. A continuación, se hará el umbralizado. Para ello se ha declarado un umbral que puede varias, en este caso, de 100. y se ha umbralizado la imagen con cv2.threshold(). Después de esto, se repite el mismo proceso de conteo de filas y columnas que en la primera tarea.

### Tarea: Tras ver los vídeos [My little piece of privacy](https://www.niklasroy.com/project/88/my-little-piece-of-privacy), [Messa di voce](https://youtu.be/GfoqiyB1ndE?feature=shared) y [Virtual air guitar](https://youtu.be/FIAmyoEpV5c?feature=shared) propongan (los componentes de cada grupo) una reinterpretación del procesamiento de imágenes con las técnicas vistas o que conozcan.
Para la cuarta tarea, en este caso, hemos querido detectar objetos de un cierto color y figurar por encima una imagen, que se escala automáticamente para cubrir toda el área del objeto.
