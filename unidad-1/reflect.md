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

#### ¿Cómo se implementa un salto condicional en Hack? Describe un ejemplo (p. ej., saltar si el valor de D es mayor que cero).
