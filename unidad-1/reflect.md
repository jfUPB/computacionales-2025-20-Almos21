# Unidad 1

## 🤔 Fase: Reflect

### Actividad 05
#### Describe con tus palabras las tres fases del ciclo Fetch-Decode-Execute. ¿Qué rol juega el Program Counter (PC) en este ciclo?
En Fetch el sistema busca la información fijandose en que lugar es que debe buscarla, en el decode obtiene lo que se buscó y empieza a decodificarlo, identificando que acciones e instrucciones debe cumplir y en el excecute ejecuta estas instrucciones. El PC funciona en el primer paso, para identificar cual es el siguiente punto de instruccion que necesita leer.

#### ¿Cuál es la diferencia fundamental entre una instrucción-A (que empieza con @) y una instrucción-C (que involucra D, M, A, etc.) en el lenguaje ensamblador de Hack? Da un ejemplo de cada una.
La primera asigna valores al registo A mientras que la siguiente aprovecha estos valores y demás para realizar relaciones entre D, M, A, etc. asignando tambien valores o relizando operaciones, comparaciones, etc.
ejemplos: - @12 (asigna el valor 12 a A) 
- M= D-A (Asigna en M el valor de la resta entre los valores de D y A, la direccion de memoria en RAM de M esta definido por el valor de A en esa instancia)

#### Explica la función de los siguientes componentes del computador Hack: el registro D, el registro A y la ALU.
El registro D tiene la capacidad de poder asignarle valores con los cuales ejecutar después las instrucciones, el registro A sirve para que el sistema tenga de referencia a que puntos debe guardar los datos o la información, o en general para las instrucciones. La ALU es la encargada de las operaciones lógicas que realiza el programa.

#### ¿Cuál es la diferencia entre la instrucción D=M y la instrucción M=D?
D=M asigna a el registro D el valor que haya en la dirección de memoria indicada por A, mientras que en M=D ocurre lo contrario, el computador identifica una dirección de memoria indicada por A y asigna a esta dirección el valor almacenado en el registro D.

#### Describe brevemente qué se necesita para leer un valor del teclado (KBD) y para “pintar” un pixel en la pantalla (SCREEN).
Para leer alguna tecla del teclado el programa necesita obtener el valor de la tecla presionada esto a través de codigos que hay asignados para cada tecla, en cuanto a poder pintar un pixel el programa necesita un valor que instruya que grupo de pixeles es necesario pintar al momento de activar la instrucción.

#### ¿Cuál fue el concepto o actividad más desafiante de esta unidad para ti y por qué?
La actividad 02, fue complicado y no logré del todo deducir como funcionaban las instrucciones, estuve bastante tiempo mirando a la pantalla releyendo el programa intentando entender como hacía lo que hacía.

#### La metodología de “predecir, ejecutar, observar y reflexionar” fue central en nuestras actividades. ¿En qué momento esta metodología te resultó más útil para entender algo que no tenías claro?
En la mayoria de actividades, más que nada en las primeras 2

#### Describe un momento “¡Aha!” que hayas tenido durante estas dos semanas. ¿Qué estabas haciendo cuando ocurrió?
En la primera actividad cuando entendi los funcionamientos de los registros.

#### Pensando en la próxima unidad, ¿Qué harás diferente en tu proceso de estudio para aprender de manera más efectiva?
Tener mejor en cuenta los tiempos de entrega.
