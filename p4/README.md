# VC
## Tarea 1: Diseñar y codificar un prototipo que haga uso de la información facial para un determinado fin de temática libre.

En esta tarea se ha creado un filtro de cara como los de instagram. En este caso simplemente coloca un gorro mejicano y un bigote en la cara del usuario cuando lo detecta.

En primer lugar, se jugó con los ajustes para la detection de la cara y de los ojos, y estos ajustes son los que se adaptaban mejor al dispositivo que teníamos:
``` python
    # Face detection and eye model setup
imodoF = 1
imodoE = 1
```
En segundo lugar, haciendo uso de shape[] y con el esquema de puntos de la cara reconocibles, detectamos los puntos centrales para el bigote: 
```python
center_nose = (shape[30][0], shape[30][1])
            left_nose = (shape[48][0], shape[48][1])
            right_nose = (shape[54][0], shape[54][1])
            nose_width = int(math.hypot(left_nose[0] - right_nose[0],
                            left_nose[1] - right_nose[1]) * 1.7)
```
Para ello hacemos uso de la imagen: ![image](https://github.com/MinervaQuin/VC/assets/100958927/ed716918-5d45-4fa5-998e-d0d4e4988690)

Con la imagen del sombrero hacemos algo similar, sin embargo para ajustar que el sombrero se quede por encima de los ojos top_left cambia de esta forma:
```python
top_left = (int(center_head[0] - head_width / 2),
                                int(center_head[1] - head_height + 20 ))
```

Y como el codigo suele dar problemas cuando el sujeto se mueve demasiado rápido para el procesamiento del ordenador hacemos uso de un try and except:

 ```python
 try:
  sombrero_area_no_nose = cv2.bitwise_and(sombrero_area, sombrero_area, mask=head_mask)
  final_head = cv2.add(sombrero_area_no_nose, sombrero_resized)            
  frame[top_left[1]: top_left[1] + head_height,
  top_left[0]: top_left[0] + head_width] = final_head
except:
   print("")
```





