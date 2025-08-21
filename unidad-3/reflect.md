# Unidad 3


## 🤔 Fase: Reflect

### Explica con tus propias palabras qué es el stack y qué es el heap en C++.
El stack y el heap son espacios reservados en la memoria que almacenan diferentes tipos de variables o funciones. El stack es el encargado de guardar las variables temporales cuya vida en la memoria se restringe a unicamente dentro de la función en la que es creada la memoria, despues de esta lo guardado en el stack se libera. El heap por su lado es para crear variables dinámicas cuya vida en la memoria persiste hasta que sean liberadas con un ``delete[]``

### Describe las tres formas de pasar parámetros a una función en C++ (valor, referencia y puntero). Para cada una, explica qué sucede en memoria y cuándo usarías cada método.
#### Valor: 
Cuando se pasa un parámetro a una función por medio de esta forma lo que se hace es crear una copia de la variable original y usarla como parámetro, esto significa que aunque este parámetro se edite dentro de la función solo se estaría editando la variable copia creada dentro del stack y no la variable original.

#### Referencia: 
Esta forma de pasar un parámetro a una función lo que hace es crear una referencia a la variable original referenciando directamente a la dirección de memoria original de la variable, esto permite editar la variable original directamente desde la funcióin sin la necesidad de crear punteros.

#### Punteros: 
Esta forma lo que hace es usar como parámetro un puntero que apunte a la variable original, haciendo que al editarlo tambien sea posible editar la dirección de memoria original, junto con la referencia esta forma de pasar parámetros permite que en la memoria sea editada la variable original y no una copia de esta.

### ¿Qué diferencia hay entre una variable local, una variable global y una variable local estática? ¿En qué segmento del mapa de memoria se almacena cada una?
#### Local: 
Una variable local se guarda en el stack y existe unicamente dentro de la función donde fue creada, esta se almacena en su espacio designado en el stack y cuando se sale de la función este espacio de memoria se libera.

#### Global:
Esta variable al crearse perdura durante todo el programa y se almacena en el espacio de memoria designado para este tipo de variables y las estáticas.

#### Estáticas:
Este tipo de variables se almacenan junto con las globales en su espacio de memoria designado y duran allí toda la ejecución del programa, estas pueden ser creadas dentro de funciones al igual que las locales pero son especificadas con ``static`` al momento de ser instanciadas. También poseen la cualidad de mantener su valor entre diferentes llamadas de la misma función, lo que permite que cada vez que esta sea llamda la variable no se reinicie desde cero sino que siga tomando en cuenta el valor ecistente al momento de la llamada.

### Explica qué es un objeto en C++ desde la perspectiva de memoria. ¿Dónde se almacenan los miembros de instancia y dónde los miembros estáticos?



### De todos los conceptos que exploraste en esta unidad (stack vs heap, paso de parámetros, ciclo de vida de objetos, etc.), ¿Cuál consideras que es el más crítico para evitar errores en programas reales? ¿Por qué?

Para mi los más importantes son el entender el ciclo de vida de los objetos y el paso de parámetros, hay que estar pendiente de si alguna parte del código es capáz de causar una fuga por no cerrar correctamente un ciclo de vida del objeto y tambien es vital saber si lo que se esta editando es la variable original o si se estan creando multiples copias que terminarían en un uso execivo de la memoria y enredo al momento de3 acceder y editar a las varibales.
