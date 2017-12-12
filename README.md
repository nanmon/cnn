# Red neuronal convolucional: Chihuahua o muffin

## ¿Como funciona la red neuronal convolucional?

Esta conformada por 4 elementos principales:
- Convoluciones
- Max Pooling
- Flattening
- Full-Connection  
EXTRA: Dropout

### Convolución
En una convolución se identifican las características principales de la imagen a travez de filtros,
se elige cuantos filtros se usaran en cada convolución, de que tamaño serán, entre otras cosas (stride, padding),
y en el entrenamiento se aprenderan los valores de cada filtro.

### Max Pooling
Cada convolución debería venir acompañada de un max-pooling. El max-pooling reduce las imagenes de caracteristicas
resultado de la convolución, dado un tamaño de pool se queda con las caracteristicas mas importantes.

### Flattening
Después de todas las convoluciones y sus respectivos max-pooling, nos quedamos con varias imagenes de caracteristicas, 
osea varias matrices, el flattening distribuye las imagenes en un vector para entrar en la siguiente fase.

### Full-connection
Una simple red por capas

### Dropout
Si se asigna un porcentaje de dropout a una capa, se eligen ese porcentaje de neuronas de esa capa de forma
aleatoria y no se usan para esa iteración del entrenamiento

## Chihuahua o muffin
![meme](https://github.com/ieee8023/deep-learning-datasets/blob/master/chihuahua-muffin/full.jpg?raw=true)

### Dataset
Se usaron los datos del [meme original](https://github.com/ieee8023/deep-learning-datasets) y otras imagenes 
encontradas en [image-net](http://image-net.org). El dataset completo lo subí a 
[google drive](https://drive.google.com/open?id=1PLPNu73zZZNXaxv_4S51P4Ris9FvUs4F) con un total de 1984 imagenes

### Arquitectura de la red
- Recibe imagenes de 150x150 rgb
- Primera convolución de 32 filtros de 3x3 y max-pooling de 2x2 con stride de 2
- Segunda convolución de 64 filtros de 3x3 y max-pooling de 2x2 con stride de 2
- Flattening
- Primera capa oculta de 64 neuronas con activación relu y dropout de 30%
- Segunda capa oculta de 64 neuronas con activación relu
- Capa de salida con dos neuronas softmax
- Optimizador adam y función loss 'categorical_crossentropy'

## Primeras pruebas
Con la arquitectura que tengo no estaba obteniendo buenos resultados:  
`loss: 0.2288 - acc: 0.9071 - val_loss: 0.5439 - val_acc: 0.8105`  
Asi que entrené la red varias veces con ligeros cambios en la red (mas/menos convoluciones, 
mas/menos filtros, mas/menos capas ocultas), pero los resultados no mejoraban y ademas tuve problemas con
mi computadora porque mi tarjeta gráfica solo tiene 2gb de memoria, así que decidí graficar las
curvas de aprendizaje con la arquitectura original

## Curvas de aprendizaje
Los tamaños del conjunto de entrenamiento usados fueron `[194, 644, 1091, 1537, 1984]` y cada uno con 10-fold cross validation
y los resultados fueron los siguientes:
![curves](https://github.com/nanmon/cnn/blob/master/curves.png?raw=true)

## Conclusión
Necesito mucho mas datos, pero ya se hacer las curvas de aprendizaje yey
