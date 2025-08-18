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

