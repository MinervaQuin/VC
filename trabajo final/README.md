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

## Resultados
