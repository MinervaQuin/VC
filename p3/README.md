# VC
## Tarea 1: Conteo de número de monedas y de dinero en total
Para el conteo de monedas se ha hecho uso principalmente de cvzone, una librería que extiende ciertas funciones que tiene cv2. En principio, se utilizan ColorFinder() para detectar regiones donde coincidan los valores de tono, saturación y valor (HSV) que indiquemos anteriormente. Y, por otro lado, findContours, que se llama igual que la función de cv2. Esta devuelve, sin embargo, tanto el contorno, como el area directamente, además de otros datos que no nos interesarán tanto. 
En primer lugar, se hace un preprocesado, donde diguminamos la imagen con la función GaussianBlur(), y luego utilizamos Canny() para sobresaltar los bordes de las monedas. Se hace uso de la función dialte para hacer el contrate más obvio con un kernel (3,3) y luego nos aseguramos que se cierren todos los contornos detectados.
Luego se hace uso de findContours() obligando a que el area detectada sea minima de 30, ya que se estaban detectando manchas muy pequeñas, sobre todo en la segunda tarea.
Luego se hace uso de colorFinder para ver el resultado final de los colores detectados en la foto completa, sin ir contorno por contorno, Esto es lo que se muestra al final de la ejecución.

![image](https://github.com/MinervaQuin/VC/assets/100958927/a1624f42-e17f-4c29-a399-b6a17753c588)

A continuación, entramos en el bucle de los contornos, de los cuales obtenemos el area, obtenemos la parte de la imagen donde está el area detectada y la almacenamos en imgCrop. Ahora, detectaremos los colores en imgCrop, lo que nos ayudará a clasificar luego las monedas según area y color. Cada vez que se detecte una moneda, se sumará a la variable totalValue que se imprime al final: ![image](https://github.com/MinervaQuin/VC/assets/100958927/a5f9f117-e306-4c93-a323-ecef6c4f2e12)

Para detectar los colores correctos de Canny como de HSV para el ColorFinder() se ha hecho uso del código al final de notebook, que con trackingbars, se iba viendo qué píxeles se resaltaban con qué valores, así se han conseguido unos valores muy satisfactorios.
![image](https://github.com/MinervaQuin/VC/assets/100958927/03eaad75-d03d-4586-a4e4-919e43a9bcc2) imagen de datos obtenidos para hsv


Principales dificultades
- Cuando las monedas tenían una sombra, aunque fuera pequeña, los círculos ya no se detectaban, o se detectaban a medias, y los cálculos se torcían, y no se acababa de detectar bien ni las monedas ni el dinero total.
- 

## Tarea 2: Clasificación de microplásticos. 
Para la tarea de clasifcicación, a falta de saber cómo detectar texturas, se ha obtado por clasificar los microplásticos en dos catégorías. En primer lugar, se clasficaría si el microplástico es circular u ovalado. En segundo lugar, se clasificaría en si es de color o negro. De esa forma, se clasificaría si es Pellet > Alquitrán > Fragmento como en el siguiente diagrama:

[![](https://mermaid.ink/img/pako:eNpVjk1qw0AMha8yaJ1cwIuWEtOsCoVk1U4XYkZ2BmYkd34IwfZhcpJCc7GOk5a2Wgjpfe8JjWDEEjTQeTmaA8as9q1mVevWn5yJMvjLOWVnJKn1-k5txs-PnbCKZIWtpPv55t0sdEpuUu3rM3lP-e0vYJnU9jvK1Mff4PZ69pp88O_F5Xg5s_rHlvBjxD4Q5_rGwmAFgWJAZ-v_46JoyAcKpKGpo6UOi88aNM_ViiXL7sQGmhwLraAMFjO1DvuIAZoOfarqgPwi8rPPX9ydYGY?type=png)](https://mermaid.live/edit#pako:eNpVjk1qw0AMha8yaJ1cwIuWEtOsCoVk1U4XYkZ2BmYkd34IwfZhcpJCc7GOk5a2Wgjpfe8JjWDEEjTQeTmaA8as9q1mVevWn5yJMvjLOWVnJKn1-k5txs-PnbCKZIWtpPv55t0sdEpuUu3rM3lP-e0vYJnU9jvK1Mff4PZ69pp88O_F5Xg5s_rHlvBjxD4Q5_rGwmAFgWJAZ-v_46JoyAcKpKGpo6UOi88aNM_ViiXL7sQGmhwLraAMFjO1DvuIAZoOfarqgPwi8rPPX9ydYGY)

Se ha hecho uso de HoughCircles para la primera etapa. Se ha utiizado la misma lógica que en el primer apartado: se ha cropeado la imagen del area del contorno. Luego se identifica si hay una forma circular, y si no, se miran la cantidad de pixeles negros, y se clasifican entre alquitrán y fragmento.

Principales dificultades:
- Se quiso utilizar el detector de eclipses para obtener un resultado más ajustado ya que HoughCicles() no es un buen método, o no lo hemos sabido ajustar correctamente para detectar los pellet, sobre todo porque muchos son más ovalados que circulares y por lo tanto no los iba a detectar. Sin embargo, algunos pellet que claramente eran circulares tampoco los detectaba. Sin embargo, getEllipse() detectaba aún peor, teniendo en cuenta que detectaba elipse en todo o en nada, ningún valor se ajustaba correctamente.
  
