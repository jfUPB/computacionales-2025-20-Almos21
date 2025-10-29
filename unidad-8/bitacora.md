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

Lo primero que podía esperar era pensar que el tiempo usado aumentaría, ya que de manera secuencial este era 0.1 seg, al ejecutar pero ahora con 6 hilos me encontre con que paso del tiempo anterior a estos 0.66 seg, esto debe ser debido a que al usar menor cantidad de hilos 

<img width="1016" height="753" alt="image" src="https://github.com/user-attachments/assets/17c092b4-dfe9-4399-b945-fd3f7c72d0c0" />

Lo bajé después a 2 hilos únicamente y obtuve este tiempo

<img width="355" height="134" alt="image" src="https://github.com/user-attachments/assets/38c699a6-6709-41fb-9e57-c25ca45b6f96" />

Este experimento me sirvió para entender como afecta el uso de diferentes cantidades de hilos en el programa y que tanto impactan a el programa final, esto es algo que a esta escala puede parecer muy poco pero estoy seguro que el uso de esto para procesos mucho más grandes puede ser mucha más que unicamente 0.04 segs de diferencia.

