# Bitácora de aprendizaje de la unidad 8
## Actividad 01
Al ejecutar el programa veo este circulo moviendose a lo largo del espacio, esto es parecido a lo que esperaba ver ya que mirando por muy encima el código vi como creaba un círculo y en la función Draw() se iba dibujando en diferente posición.

<img width="401" height="424" alt="image" src="https://github.com/user-attachments/assets/6dce72b3-7991-45ac-b3e4-88375fcbb8d1" />

Después pasó algo interesante y es que al apretar con click se congelaba todo y disminuía de tamaño la esfera, creo que ocurre porque alguna parte del código bloquea el programa, no permitiendo que se actualice correctamente.

<img width="394" height="427" alt="image" src="https://github.com/user-attachments/assets/2b97b545-f942-4668-ac7c-91360118cb36" />

Al cambiar el código y volver a ejecutar me encuentro con que el círculo no cambia de tamaño inmediatamente pero tampoco se congela el progrma, esperaba que si cambiara de forma inmediata. Al revisar la consola aparece lo siguiente

<img width="450" height="194" alt="image" src="https://github.com/user-attachments/assets/acb3ba0b-fa46-4d4e-ae99-76c691e0573b" />

Esto me hace pensar que lo que ocurre es que el hilo se ejecuta al mismo tiempo que el programa, pero igual y se demora en hacerlo, se queda pensando de fondo quizas porque requiere muchos recuersos o algo por el estilo.

La diferencia entre la concurrencia y un paralelismo se encuentra en que la concurrencia realmente no ejecuta dos procesos al mismo tiempo, sino que intercala entre ellos para dar una idea de simultaneidad. El paralelísmo por otro lado si ejecuta ambos procesos al mismo tiempo, esta diferencia es vital al momento de ejecutar un programa ya que una concurrencia puede ser menos eficiente y relentizar el funcionamiento del programa, al no estarse ejecutando al mismo tiempo con diferentes o múltiples núcleos lo que ocurre es que el rendimiento es menor.

## Actividad 02
- La variable esta siendo protegida en esta parte del código
```` c++
  lock();
    ofSeedRandom();
    circleSize = ofRandom(20, 70);
    unlock();
  std::cout << "Circle size: " << circleSize << std::endl;
````
- Pienso que el rendimiento del programa es posible que sea afectado al utilizar el mutex, esto debido a que según lo que se explica este obliga a los hilos a esperar que el otro termine de acceder a una variable para poder hacerlo. Esto afecta más que nada a un programa con paralelismo, ya que puede interrumpir este paralelismo, causando que los hilos deban esperar a uno de ellos para poder continuar, afectando así el rendimiento del programa y su paralelismo.
- Al cambiar de valor el useLock el programa funciona mal, usualmente cuenta hasta 4000000 y al reiniciarce vuelve a contar desde cero de manera correcta, al alternar entre los valores de useLock y volverlo falso deja de contar bien y para en otro número como este, además de no reiniciarse bien la cuenta, esto debe ser porque al poner el useLock falso la protección al counter y su acceso desaparece y se pierde el mutex, esto debe ser lo que cause una condición de carrera aquí.
  
  <img width="563" height="155" alt="image" src="https://github.com/user-attachments/assets/1f23b60b-1d0b-4491-aa42-f80e40df01b4" />
- Lo que ocurre en esta condición de carrera es que el counter al hacer su operación lo hace con tres pasos que son leer el contenido de la memoria, sumarle, y después poner el nuevo valor en el espacio de memoria anterior, aqui si dos hilos realizan esto a la misma vez pueden causar que no se sume bien, ya que si dos leen el mismo valor, lo suman y ponen en la memoria entonces no se va a perder una suma, ya que ambos terminaron realizando lo mismo a la vez, esto causa que se pierda el sentido de el paralelismo ya que es como si solo uno trabajara, pero gastando el doble de recursos.

Un ejemplo con esta condición sería por ejemplo que el counter esté en 7, y unos hilos A y B estan sumandole valores pero no hay nada que evite que a la vez accedan a el counter entonces ambos tomarán el valor 7, le sumarán 8 y pondran esto como el valor final, esto significando que se perdío una cuenta ya que de otra manera usando por ejemplo un mutex entonces se sumarían en total 2 al valor original.

## Actividad 03
Este es el resultado que se obtiene al realizar ambos códigos, cambiando los valores del cuadro y la rapidez del programa, el segundo lo sentí más rápido.
<img width="1020" height="761" alt="image" src="https://github.com/user-attachments/assets/0d5b95c9-f5e0-4813-beaa-5b11b5ecb42b" />

Para experimentar decidí intentar cambiar el número de hilos como se proponía en el texto, primero que nada los bajé a 6, para tener una primera idea este era el tiempo que aparecía anteriormente al usar la cantidad normal (12)

<img width="350" height="133" alt="image" src="https://github.com/user-attachments/assets/b1317f8d-7d49-49f7-a3df-fd5d9ac776ae" />

Lo primero que podía esperar era pensar que el tiempo usado aumentaría, ya que de manera secuencial este era 0.1 seg, al ejecutar pero ahora con 6 hilos me encontre con que paso del tiempo anterior a estos 0.66 seg, esto debe ser debido a que al usar menor cantidad de hilos el programa se demora más haciendo los procesos ya que lo divide entre menor cantidad de hilos.

<img width="1016" height="753" alt="image" src="https://github.com/user-attachments/assets/17c092b4-dfe9-4399-b945-fd3f7c72d0c0" />

Lo bajé después a 2 hilos únicamente y obtuve este tiempo

<img width="355" height="134" alt="image" src="https://github.com/user-attachments/assets/38c699a6-6709-41fb-9e57-c25ca45b6f96" />

Este experimento me sirvió para entender como afecta el uso de diferentes cantidades de hilos en el programa y que tanto impactan a el programa final, esto es algo que a esta escala puede parecer muy poco pero estoy seguro que el uso de esto para procesos mucho más grandes puede ser mucha más que unicamente 0.04 segs de diferencia.

## Actividad 04
Estos son los datos del programa con un solo hilo al inicio y al aumentar hasta cierto punto
<img width="132" height="57" alt="image" src="https://github.com/user-attachments/assets/dcbdd1f7-a415-49eb-ab8a-9561f35f94c4" />
<img width="133" height="82" alt="image" src="https://github.com/user-attachments/assets/29e28eca-3c69-405c-b9ba-703d4498e6ed" />

Estos los del que tiene varios hilos a casi el mismo punto que la segunda imagen del anterior
<img width="126" height="57" alt="image" src="https://github.com/user-attachments/assets/5c93f658-ca68-4cd1-a744-198e2325e6ec" />

### 1. 
La estructura de datos principal que contiene la información de todos los boids y que es accedida por múltiples hilos es ``vector<Boid> boids;`` aquí se guardan todas las instancias de los boids activos, esta es accedida por el hilo que dibuja en el draw, para recorrer y dibujar cada boid, y por el hilo trabajador en ``Flock::threadedFunction()`` donde va actualizando la simulación

### 2.
Primero que nada se utiliza el lock y unlock para asegurarse de que un hilo trabaje a la vez con el recurso ``vector<Boid> boids`` que ambos comparten, después a cada boid se le aplica el ``b.run(boids)`` donde se leen sus propiedades y en update se actualizan para simular correctamente su siguiente estado respecto a el estado anterior.
- La función draw se encarga de recorrer cada boid con un for, para poder llamar ``b.draw()`` en cada uno, el hilo principal lee los datos de cada boid para poder dibujarlos en pantalla, no modifica el vector ni los boids mismos.
- El ``Flock::addBoid()`` bloquea el acceso a el vector y crea un nuevo void para después desbloquearla de nuevo y la función ``ofApp::mouseDragged()`` llama al ``flock.addBoid()`` cada que se arrastra el mouse, esta función se ejecuta desde el hilo principal.

### 3.
El escenarío es uno donde no haya sincronización entre el hilo de actualización y el del mouse, si no esta esta mientras el hilo X está recorriendo el vector, el hilo Y modifica la estructura interna del std::vector al añadir un nuevo elemento causan dos problemas graves, el primero es la invalidación de iteradores y referencias donde std::vector puede reasignar memoria al crecer, todos los iteradores y referencias (Boid& b) usados por el hilo X quedan inválidos, el hilo X sigue usando esas referencias como si fueran válidas causando que puede acceder a memoria que ya no pertenece al vector. El segundo error es la inconsistencia lógica, donde el tamaño del vector (boids.size()) cambia mientras el hilo X lo recorre, el hilo puede intentar acceder a un índice fuera de rango o saltarse elementos causando que algunos boids puedan leerse dos veces o no actualizarse en absoluto.
Una situación donde ago así pase sería algo como: El hilo X está ejecutando Boid& b = boids[37]; Mientras tanto, el hilo Y hace boids.emplace_back(x, y); y el vector se redimensiona. Ahora boids[37] apunta a una posición de memoria que ya fue movida. Cuando el hilo X intenta acceder a b.position, accede a basura.

### 4.
Las llamadas son en ``Flock::addBoid()``  ``Flock::threadedFunction()`` y ``ofApp::draw()``

### Justifiación
Para el caso del punto 3 por ejemplo, si el hilo trabajador recorre el vector boids mientras el hilo principal añade un nuevo boid con emplace_back(), el vector podría cambiar de tamaño y dañar los iteradores. El uso de lock() y unlock() hacen que solo un hilo a la vez pueda acceder o modificar los boids, evitando que se lea mientras otro hilo lo cambia y, por tanto, previniendo cualquier fallo o comportamiento extraño.

### 5.
Lo que pasa es que si muchos hilos compiten por el mismo lock, solo uno puede acceder al vector a la vez, haciendo que los demás esperen. Esto convierte el trabajo paralelo en algo casi secuencial, reduciendo el beneficio que trae el usar el paralelismo.

- Las diferencias entre el flocking con y sin hilos son que en el flocking sin hilos todo se ejecuta de manera secuencial, esto lo vuelve algo más lento pero a la vez seguro, no hay posibilidad de que ocurra una condición de carrera o algo por el estilo, mientras que al utilizar el flocking con hilos el trabajo de divide en dos hilos cada uno encargado de una cosa, pero brindandoles a ambos el acceso a un mismo recurso, esto vuelve necesario el uso de un mutex o de lo contrario el código se vuelve fuertemente inseguro y pueden ocurrir condición de carrera, haciendo que por más que haya paralelismo sea necesaria la sincronización.
- Porque al agragar son más los boids que son necesarios actualizar, esto relentiza el proceso total tanto con y sin hilos, ya que al demorarse más tambien se demora más la sincronización, etc.
- Ese sleep(5) actúa como un pequeño respiro para el procesador y ayuda a mantener un equilibrio entre rendimiento, paralelismo y eficiencia.

