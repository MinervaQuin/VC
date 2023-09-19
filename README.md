# VC
En el cuaderno que se adjunta en la carpeta se adjuntas todas las tareas que se han pedido para la práctica 1 de la asignatura Visión por Computador

### Tarea: crear imagen con textura de ajedrez
Para la primera tarea se ha utilizado dos bucles for que recorran toda la matriz de pixeles y vayan conformando los sucesivos recuadros en saltos de 25px en px por columna y de 50 por fila

### Tarea: Replicar a Mondrian
Para la segunda tarea se ha ido creando "a mano", sin uso de funciones de genración automática, cuadrados de diferentes colores para replicar la obra "Piet Mondrian". Aquí se adjunta enlace: Cuadro Piet Mondrian: https://media.vogue.mx/photos/61805037530d745b9ecd49f2/master/w_1600,c_limit/Piet-Mondrian-composicio%CC%81n-en-rojo-amarillo-y-azul.jpg

### Tarea: Crear una imagen que utiliza funciones varias de OpenCV
Para la tercera tarea se han ido utilizando las funciones de circle(), fillPoly() y triangle() para recrear el logo de OpenCV.

### Tarea: Hallar los píxeles más claros y más oscuros (Matrices 8x8)
Para la cuarta tarea se ha pasado la imagen de color a gris, y con la ayuda de la función cv2.minMaxLoc(gray_image), hemos hallado los píxeles de mayor valor y menor valor, respectivamente el más claro y el más oscuro. Para hallar, en vez de los píxeles, la matriz 8x8, se han conformado dos bucles que recorren la matriz tanto por filas como por columnas, asegurandonos que siempre halla hueco para pillar una matriz de ese tamaño. En cada bucle se visualiza si el valor hallado nuevo es mayor al valor anterior hallado y si es cierto se actualizan los valores. Por último, se crean las figuras (circulo o cuadrado) para demostrar los datos hallados. La imagen que se ha utilizado ha sido la siguiente: fondo link: https://img.freepik.com/fotos-premium/patron-marmol-natural-fondo_1258-22160.jpg

### Tarea: Transformar un plano de color de una imagen
Para la quinta actividad, se han creados un filtro de color que impondremos a una máscara HSV (Hue, Saturatio,Value), para luego aplicar esta máscara a la imagen y obtener otra imagen distinta de vuelta. Luego se han modificado los valores para modificar la imagen, en este caso intercambiando las zonas amarillas por las azules y viceversa. Se ha utilizado una foto de "La noche estrellada" de Vincent Vangoh.

### Tarea: Crear una visión pop-art similar a Andy Warhol
Para la sexta actividad, se ha utilizado una tecnica similar a la actividad anterior, donde se aplica una máscara cada fotograma, que nos devuelve una imagen binaria. Esta imagen sustituirá a cada capa rgb. Se varían los valores para obtener la misma imagen pero en distintos tonos, y recibir una imagen similar a un cuadro de Andy Warhol
