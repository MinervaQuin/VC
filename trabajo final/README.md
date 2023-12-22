# Trabajo Final: FindYourself

## Descripción
Esta aplicación tiene como intención ser de utilidad cuando quieras encontrar a una determinada persona o pareja en fotos personales. Hay que recalcar que el programa no es perfecto en hallar siempre a las personas debido a angulos, rotaciones o cambios en las caras debido a problemas con la calidad de la imagen

## Código
El código se divide en dos grandes partes: la parte gráfica y las funciones lógicas. La parte gráfico son los dialogos. Hay 3: el diálogo principal donde se puede elegir una de las dos opciones: buscar una persona, o buscar una pareja. La primera opción crea una ventana donde se puede seleccionar una foto donde salga la persona a buscar, y otra opción donde elegir el directorio con las fotos que analizar. Las carpetas de la imagen y el directorio pueden coincidir sin problemas. La otra opción es similar, pero permite elegir dos imágenes.

Por otro lado, tenemos 2 funciones principales: search_face y search_two_faces. Estas se encargan, como bien indican sus nombres, de buscar una o dos caras en el directorio seleccionado. Las dos funciones devuelven un array con los path hacia las imágenes en las que se han encontrado similitudes.

``` python
def search_face(img1_p, directory):
    metrics = ["cosine", "euclidean", "euclidean_l2"]
    print(directory)
    #face recognition
    df = DeepFace.find(img_path = img1_p, 
            db_path = directory, 
            distance_metric = metrics[2],
            enforce_detection=False
    )

    img_paths = df[0]['identity']
    img_url = []

    for url in img_paths:
        # print(url)
        img_url.append(url)
        
    return img_url

def search_two_faces(img1_p, img2_p, directory):
    url_im1 = search_face(img1_p, directory)
    url_im2 = search_face(img2_p, directory)
    resultado = elementos_repetidos(url_im1, url_im2)
    return resultado
```

## Ejecución y Resultados

En primer lugar nos saldrá la pantalla para elegir que opción queremos elegir:

<img width="227" alt="image" src="https://github.com/MinervaQuin/VC/assets/100958927/a3d90f56-d8ff-4377-8083-6c06bf06354a">

Si seleccionamos la primera opción nos saldrá la siguiente pantalla:

<img width="425" alt="image" src="https://github.com/MinervaQuin/VC/assets/100958927/08c89cfa-4957-4dbf-a284-13c67045af17">

Donde podremos elegir el directorio y la imagen de la persona que queremos buscar (nuestro repositorio ya viene con imágenes para probar el funcionamiento del programa pero puede utilizar sus propias fotos).

<img width="425" alt="image" src="https://github.com/MinervaQuin/VC/assets/100958927/01ba0acd-d688-4860-b5d7-c5751ad799fb">

Y al darle al botón de buscar nos debe salir el listado de fotos que se han encontrado:

<img width="425" alt="image" src="https://github.com/MinervaQuin/VC/assets/100958927/9a6bfbc1-1191-414c-ae35-43a3f7b72feb">

Podemos pasar el ratón sobre el link hacia la imagen, y cuando se ponga en azul podemos clicar para que se nos habra en una ventana con nuestro visor de imágenes por defecto:

<img width="425" alt="image" src="https://github.com/MinervaQuin/VC/assets/100958927/bfd57eea-0a4b-4cb1-8f8a-3dfe7b8af80e">
<img width="425" alt="image" src="https://github.com/MinervaQuin/VC/assets/100958927/8aa5c85b-e4f0-47fd-8cc8-2b7153a7e367">

Como podemos observar, nos ha pillado dos, aunque en realidad hay dos imágenes más que podría haber detectado.

Si elegimos la segunda opción, podemos probar a hallar las fotos en las que los dos estén presentes:

<img width="425" alt="image" src="https://github.com/MinervaQuin/VC/assets/100958927/3fe93448-0b1f-4471-bcec-7486dc5c233c">

<img width="425" alt="image" src="https://github.com/MinervaQuin/VC/assets/100958927/d6dfed2d-2275-4d2c-889a-602295853e88">
<img width="425" alt="image" src="https://github.com/MinervaQuin/VC/assets/100958927/59cc9b57-66e7-492c-b4b8-dbde33fd7de0">

Y como vemos, nos halla la anterior.

---
Resultados:
Son bastante buenos con las caras de hombre. Sin embargo se aprecia un gran porcentaje de fallo con las caras de las mujeres. Aquí mostramos un ejemplo de como usando la cara de Brad Pitt nos haya casi todas las fotos en las que está con Angelina Jolie. Sin embargo, cuando utilizamos la foto de Angelina, sólo pilla una de las fotos en las que está con Brad Pitt y el resto es la misma que le introducimos para analizar y fotos de otras mujeres que no se parecen en nada.

<img width="425" alt="image" src="https://github.com/MinervaQuin/VC/assets/100958927/be588ca4-3d1b-471c-bed2-4e785d40d1e1">

<img width="425" alt="image" src="https://github.com/MinervaQuin/VC/assets/100958927/f4536ed7-f740-43b6-87ff-57dc97bdd1cc">

<img width="425" alt="image" src="https://github.com/MinervaQuin/VC/assets/100958927/c11b14e7-cb6a-4d43-903f-d3373a2108ee">

<img src="https://github.com/MinervaQuin/VC/assets/100958927/dbd7127f-374e-4c77-b5e0-71681fcad2c4" alt="Dibu" width="425"/>

Se puede hacer notar que la única imagen que sitúa a Angelina con Brad Pitt es la única que, cuando analizamos la foto de Brad Pitt, no aparece en la lista. Por lo tanto si hacemos el análisis de pareja, nos saldría la pantalla vacía, sin lista, ya que no encontraría coincidencias.

















































