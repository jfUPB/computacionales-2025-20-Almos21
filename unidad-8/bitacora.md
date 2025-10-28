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
