# Unidad 3

## 🔎 Fase: Set + Seek

### Actividad integradora de investigación

#### A. Predicción
##### ¿Cuál será la salida final en la consola de este programa?
Este programa va poco a poco cambiando variables y en general aplicando cosas vistas en las actividades anteriores, primero da unas variables y las usa como parámetros en diferentes funciones que hacen diferentes cosas con estos valores, algunos cambiando la variable original y otros creando copias de esta dentro de si. Y por último ejecuta una función que va sumando valores a una variable estática, esta se va sumando y no se reinicia cada vez que se ejecuta la función, esto debido a su naturaleza estática que solo se inicializa una vez y dura toda la ejecución del programa-
##### Escribe la salida completa que esperas.
```` c++
--- Experimento con paso de parámetros ---
Valor inicial de val_A: 20
-> Dentro de sumaPorValor, 'a' ahora es: 30
Valor final de val_A: 20
Valor inicial de val_B: 20
-> Dentro de sumaPorReferencia, 'a' ahora es: 30
Valor final de val_B: 30
Valor inicial de val_C: 20
-> Dentro de sumaPorPuntero, '*a' ahora es: 30
Valor final de val_C: 30
--- Experimento con variables estáticas ---
-> Llamada a ejecutarContador. Valor de contador_estatico: 1
-> Llamada a ejecutarContador. Valor de contador_estatico: 2
-> Llamada a ejecutarContador. Valor de contador_estatico: 3
````
##### Dibuja un mapa de memoria conceptual de este programa justo antes de que main finalice.
```` c++
+-------------------------------+
|       Segmento de código      |
las funciones y el texto, como
ejecutarContador() , sumaPorValor() , sumaPorReferencia(), sumaPorPuntero(), main()          
+-------------------------------+
| Variables globales y estáticas|
estas se mantienen durante todo el programa y se guardan aquí
contador_global, contador_estatico
+-------------------------------+
|           Heap                | 
|          no hay               |
|                               |
+-------------------------------+
|           Stack               | 
Aquí estan las que se definen dentro de las funciones como parámetros y no son estáticas:
val_A, val_B, val_C, el parámetro a de la función sumaPorValor
+-------------------------------+
````
#### B. Verificación y análisis (usando el depurador)
Este es el primer paso, las variables dentro del main estan definidas y se muestra el valor actual de ``val_A``
<img width="1577" height="867" alt="image" src="https://github.com/user-attachments/assets/8b6c3d5a-0575-4fb2-ac32-e3e10f9024f3" />

Ahora que se ejecuta el siguiente paso podemos ver como ``val_A`` no cambia de valor y sin embargo se imprime el valor de ``a`` como 30, esto refiriendose a la copia creada dentro de ``sumaPorValor`` la cual no afecta a la variable original
<img width="1570" height="832" alt="image" src="https://github.com/user-attachments/assets/19aac69b-6d7d-470a-bdcd-84bfac283f5a" />

Ahora vemos que efectivaente se imprime el valor final de ``val_A`` como 20 y pasamos al siguiente con ``val_B`` teniendo como valor inicial 20
<img width="1682" height="828" alt="image" src="https://github.com/user-attachments/assets/38106db1-f36d-4245-a9b5-ee0e45da75b3" />

En el siguiente paso vemos como la variable ``val_B`` si es afectada directamente en su posición original y se le suma 10, esto porque ``sumaPorReferencia`` si altera directamente la dirección original.
<img width="1743" height="816" alt="image" src="https://github.com/user-attachments/assets/62b0b05a-09a6-4c00-8f14-bc10eab573ad" />

Valor inicial de ``val_C`` que según mi predicción tambien debería cambiar a 30
<img width="1741" height="828" alt="image" src="https://github.com/user-attachments/assets/7bd46492-3ccc-405e-a503-d67170846550" />

Valor final de ``val_C`` efectivamente se le sumó 30, esta vez usando punteros y no referencias.
<img width="1665" height="860" alt="image" src="https://github.com/user-attachments/assets/268e9c50-9b10-4023-8c44-53913168e8d8" />

El siguiente paso es ya en la siguiente parte, aqui ejecuto la primera función, según lo predicho ``contador_estatico`` deberia irse sumando y no reiniciarse en cada instancia
<img width="1770" height="848" alt="image" src="https://github.com/user-attachments/assets/91e1d116-884d-4c10-a018-58c6458be66d" />

Efectivamente el valor final aumentó en 1 cada vez, por lo que no hay diferencia con mi predicción
<img width="1849" height="795" alt="image" src="https://github.com/user-attachments/assets/bf7c967e-9d08-43f2-a994-b9664667d350" />

Este sería el resultado final, que no difiere de mi prediccion:
<img width="1135" height="408" alt="image" src="https://github.com/user-attachments/assets/9b5ab700-c8d1-4c7a-8a40-a6d7b3879e31" />

##### Describe qué demuestran estas capturas sobre la diferencia entre los diferentes tipos de paso por parámetros analizados.
Como se explicaba en otras actividades y se demostró aquí existe una diferencia entre loq ue ocurre según el tipod e parámetro se use, en ``sumaPorValor`` este creaba una copia que solo se mantenía en el stack y no afectaba a la variable original, mientras que en las otras dos sumas si se afectaba la dierección original, aqui la diferencia radicaba en el como, en una era por referencia mientras que en otra era por el uso de punteros.
##### Explica con tus propias palabras el comportamiento de contador_estatico. 
Esto es debido a su naturaleza de ``static`` ya que las variables estáticas se diferencian de las normales, esta se diferencia en el hecho de que al crearse se almacena junto a las globales y se conserva durante todo el programa hasta que se termine, además que su valor como se puede observar se conserva entre llamadas lo que permite que no se reinicie constantemente, de lo contrario el resultado hubiera sido 1 en todas.




