# Bitácora de aprendizaje de la unidad 7

## Actividad 01
### 1.
<a name="1"></a>
Esto es lo que sale al momento de ejecutar el programa, un tirangulo naranja, no se si tendrá algo relacionado con el programa o algo que se vaya a explicar pero me percaté de que el tamaño del triángulo depende de el tamaño de la ventana, si esta se acorta este también, y no recuerdo si en programas pasados pasaba lo mismo o solo se reducia el rango de visión del programa sin afectar su tamaño.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/5019023a-b0b9-4c54-87fb-72aa1c81908a" />

<img width="872" height="964" alt="image" src="https://github.com/user-attachments/assets/abab76d8-6c38-490e-ab7f-0f36862b97f5" />

### 3.
-¿Porqué se utiliza repetidamente el "gl"?
-¿De donde saca los compíladores de shaders y en general todas estas referencias a objetos relacionados con renders?
-¿Que es VAO/VBO?

## Actividad 02
<a name="2"></a>
Para poder crear un proyecto de OpenGL se necesitan varias bibliotecas que entre sí permiten que un proyecto de estos pueda funcionar adecuadamente, la primera es ``opengl32.lib`` esta se encarga de crear el contexto inicial de OpenGL y tiene funciones muy básicas, de no ser por esta el proyecto no podría ser iniciado en absoluto, es como si creara el "terreno" base, se ejecuta en tiempo de compilación y enlace. La siguiente es ``GLFW`` esta se encarga de crear una ventana, manejar el teclado y en general configurar el contexto de OpenGl, esta tiene dos funciones muy importantes: ``glfw3.lib`` es aquella que le indica al compilador donde estan las funciones, mientras que ``glfw3.dll`` tiene el código real que se ejecuta, este es muy importante ya que para que el programa corra esta función debe estar junto al ejecutable. 
``GLAD`` viene de un OpenGL moderno, y no viene de ``opengl32.lib`` las funciones modernas se encuentran almacenadas en la GPU, es ``GLAD`` quien se encarga de preguntarle al sistema donde se encuentran estas funciones para cargarlas rápidamente, Para eso usas el archivo ``glad.c`` y sus encabezados (``glad.h``). Se usa en tiempo de ejecución, cuando se llama a ``gladLoadGL()`` todo esto permite el poder utilizar funciones modernas, de lo contrario solo se usarían funciones viejas. ``GLM`` es algo opcional que ayuda demasiado al momento de trabajar con vectores y matrices, solo es código fuente y es muy útil para las animaciones o transformaciones.
Por último pero no menos importante estan los drivers de la GPU que son los que realmente ejecutan todas las funciones modernas que ``GLAD`` encuentra, son estos los que hacen el trabajo real. Es así como todo se conecta para permitir dibujar en 3D, con ``GLFW`` y ``opengl32.lib`` permitan el acceso a ``OpenGL``, ``GLAD`` acceda a las funciones modernas, los drivers ejecuten y ``GLM`` permita facilitar el trabajo.

## Actividad 03
### Experimento
Al dividir por 2 y por 4 el triángulo que resulta es este respectivamente:

<img width="446" height="470" alt="image" src="https://github.com/user-attachments/assets/3b75e468-7b92-4424-b395-aeb3427c9dc8" />

<img width="447" height="473" alt="image" src="https://github.com/user-attachments/assets/f194a0fc-f6e2-4281-95f5-dc2e77a8b739" />

resulta más pequeño, esto seguramente es debido a que ocurre lo explicado de que el viewport no se ajusta al tamaño del framebuffer, causando que el triángulo se posicione y escale mal. Algo interesante es que al jugar con el tamaño de la ventana se restablece el triángulo a estar bien ubicado en el centro
### Resumen
<a name="3"></a>
Hasta ahora hemos aprendido como se establece el contexto inicial de OpenGL y que necesita para funcionar correctamente, ahora empezamos a entender como es que define un contexto en el cual "dibujar" para esto se ayuda de ``GLFW`` que fue algo definido anteriormente, esta le permite poder generar un contexto en el cual "dibujar" y es multiplataforma lo que evita tener que cuadrarlo para la plataforma específica donde se hace. OpenGL no es quien dibuja realente sino que lo hace la GPU pero es OpenGL quien le brinda el contexto y le "explica" como utilizarlo y como dibujar lo que le pedimos. El espacio donde dibuja esto es el framebuffer que es un espacio en la memoria designado para dibujar inicialmente lo que se desea hacer, esto se muestra finalmente en la pantalla, el viewport define que espacio del buffer es visible, debe de ajustarse correctamente con este último de lo contrario se alterará la imagen, ahora las preguntas que me surgen es ¿como es que al cuadrar la ventana se ajusta correctamente el triángulo?, el que pasaría si no se tuviera un espacio así sino que se mostrara directamente en pantalla, o es indispensable este espacio aparte donde se dibuja inicialmente? ¿Que pasa si el tamaño del viewport es mayor al del buffer, que es entonces lo que se observa? Esto útlimo lo intenté hacer más arriba (si es que entendí bien como funcionaba la línea de código) pero solo no aparecia nada, ¿es esto porque al ser más grande que el buffer no aparece nada?
### Segundo experimento
Al jugar cambiando parámetros en ``glDrawArrays`` sale algo como esto al cambiar por lines y 4 al final

<img width="425" height="473" alt="image" src="https://github.com/user-attachments/assets/460d54a8-1518-4979-b60a-c639ec564edd" />

si se cambia a Points no se ve nada, quizas se esten dibujando los puntos pero son casi invisibles para mi, si se cambia a 2 al final pero teniendo triangles desaparece el triángulo y si lo cambio a 4 sigue apareciendo sin ningún cambio lo cual me parece raro.
### Preguntas
<a name="4"></a>
#### ¿Qué es el contexto OpenGL?
Es el contexto que crea OpenGL donde almacena cual es el estado gráfico que tiene, es muy necesario ya que sin él practicamente no se podría hacer nada.
#### ¿Cuál es el rol de la biblioteca GLFW y qué ventaja tiene usarla?
Es la que permite a OpenGL dibujar, le da el espacio donde hacerlo y le da la disposición de las "herramientas" y espacio donde hacerlo, su ventaja es que es multiplataforma por lo que se adapta sola a la plataforma utilizada.
#### ¿Por qué crees que OpenGL necesita un contexto (recuerda la analogía del taller de arte)?
Necesita el donde poder realizar lo suyo, de lo contrario no podría hacer nada, no le basta con lo que posee si no tiene donde y como aplicarlo.
#### ¿En últimas qué será el framebuffer y a qué te recuerda de las dos primeras unidades del curso?
El framebuffer es un espacio de memoria donde OpenGL dibuja antes de pasarlo a pantalla, es un "lienzo" invisible donde se hace todo inicialmente en cada cuadro, en las primeras unidades aprendimos a disponer de un espacio para dibujar con el lenguaje de ensamblador, supongo que es asi como se relacionan ya que el espacio en el que dibujabamos pixel por pixel era un buffer, pintabamos un espacio de memoria poco a poco y esto se veía en la pantalla.
#### ¿Qué relación entre en el viewport y el framebuffer? 
El viewport es un espacio del framebuffer donde se dibuja, este toma una parte o la totalidad de este, es como si tuvieramos una ventana movil por la cual podemos ver algo, esta ventana puede ajustarse a la pared donde esta puesta, tienen que tener una relación adecuada, de lo contrario habrán errores en lo que se muestre en pantalla.
#### ¿En todo la analizado hasta ahora qué rol juega los drivers de la GPU y la GPU misma?
Es esta quien realmente dibuja todo, es OpenGL quien le indica como hacerlo y con que.
#### ¿Por qué crees que sea necesario activar el VSync? ¿Si no lo activas y la imagen es estática qué crees que pase, y si es dinámica?
Es necesario porque si la taza de refresco no es igual entre la ventana y el monitor pueden haber momentos donde se vean las cosas mal o no sincronizadas, esto no afectaría tanto algo estático pero si algo dinámico, causando que quizas algunos momentos no se puedan ver.
#### En esta unidad estamos usando OpenGL moderno, pero ¿Qué es OpenGL Legacy? ¿Qué diferencias hay entre ambos?
Este era el OpenGL "viejo" no usaba shaders, era más lento, menos eficiente y no utilizaba el VAO y VBO para dibujar como si lo hace el moderno, en general en este OpenGL decidía como renderizar y dibujar lo establecido.
#### ¿Qué es el shader program? ¿Por qué es importante en OpenGL moderno?
Los shader son los que permiten a OpenGL y a la GPU procesar una escena, si ellos no se vería nada, el shader program combian varios y los junta para poder utilizarlor con OpenGl
#### Trata de revisar el código setupTriangle(), intuitivamente ¿Qué crees que hace? ¿Qué crees que es el VAO y el VBO?
Segun veo hace una matriz con la ubicación de los vertices, creo que el VAO hace un array con estos valores para definir el objeto y el VBO debe ser algun buffer que lo dibuje, pero no estoy seguro aún.
#### En el ciclo principal (game loop) de OpenGL, notaste que en cada frame (cuadro) le decimos a openGL que use el shader program y el VAO. Si le indicas esto antes del game loop ¿Será necesario seguirlo haciendo en cada loop? Si no es necesario ¿En qué casos crees que esto puede ser útil?
Yo creo que no es necesaio pero puede ser necesario en proyectos que sean muy grandes o donde puedan haber errores al no asignar esto constantemente.
#### Finalmente, recuerda lo que hace glfwSwapBuffers(mainWindow); ¿Por qué crees que es importante? ¿Qué pasaría si no lo llamas? ¿Cómo explicas lo que pasa si no lo llamas? (experimenta)
Esto hace que el buffer donde se estaba dibujando todo sea el que se muestre en pantalla, de no ser asi pues no se mostraría lo dibujado sino que se queda quieto dibujando sin ser visto, es importante que sea asi para que se vea bien la pantalla y como se dibuja.

## Actividad 04
### Diferencia CPU y GPU
La CPU hace pocas cosas a la vez es más de hacerlo uno a uno pero más complejas, mientras que la GPU hace muchas cosas simples a la vez, esto le permite hacer cosas como la del video donde pintaba inmediatamente a la monalisa, por eso es mejor usar la GPU para cosas gráficas, porque de lo contrario seria como en la unidad 1 y 2 donde para dibujar habia que ir frame por frame activando cada pixel de una manera individual y lenta.
### Preguntas Video
<a name="5"></a>
#### 1
- Vertex Shading: En esta se toman los vertices de la figura formada y se pasan de un espacio 3D a el 2D de la pantalla, esto a atraves de calcular los espacios de estos vertices y realizar complejas y numerosas operaciones matriciales, esto ocurre poco a poco con cada triangulo de el objeto.
- Rasterization: En este proceso se toman los triangulos calculados anteriormente y se calcula cuantos pixeles y en que posición son necesarios para dibujar esta imagen, son texturizados y divididos en fragmentos
- Fragment Shading: En esta el objetivo es permitir diferenciar las superficies a partir de calcular diferentes iluminaciones para los fragmentos.
#### 2
En el pipeline fijo todos los pasos estaban predefinidos por la API y nosotros solo cambiabamos los estados sin cuadrar la lógica interna, mientras que en el moderno estos pasos pueden ser programados con los shaders, principalmente podemos programar el vertex shader y el fragment shader. Las ventajas de esto son que nos da mejor flexibilidad y control sobre la apariencia, además que nos permite usar métodos y efectos más modernos aprovechando mejor la GPU al nosotros saber que queremos usar, calcular y como.
#### 3
En este proceso se toman los triangulos calculados anteriormente y se calcula cuantos pixeles y en que posición son necesarios para dibujar esta imagen, son texturizados y divididos en fragmentos
#### 4
Los fragmentos son grupos de pixeles que comparten la misma textura o color, no es lo mismo que un pixel porque de hecho los fragmentos estan consolidados por varios pixeles, son grupos de estos que poseen las mismas carácteristicas y que estan dentro de un mismo triángulo.
#### 5
El Z-Buffer es un espacio donde se guardan los valores en z de los objetos, esto se utiliza para evitar el problema causado al momento de querer mostrar vario objetos que estan en un mismo espacio en valores de X y Y pero no en Z, o sea uno atrás del otro, el programa solo representa aquellos que esten más cerca a la cámara al encontrarse con estos casos, para saber cuales cumplen con esto y poder compararlos se utilizan los valores guardados en el Z-Buffer
#### 6
Este problema surge porque si se hace la resterization de manera simple se generan bordes pixelados, el anti-aliasing permite vbariar la opacidad de los pixeles en los bordes para generar el efecto de bordes suaves y disminuir la percepción de que estan pixelados.
#### 7
El fragment shader esta relacionado con la iluminación debido a que utiliza esta para calcular, junto con la posición de el fragmento, su color, esto tomando en cuenta tambien cosas como la textura, etc. y depende de la iluminación ya que este es el punto de esta técnica, no dejar un objeto con un color plano sino variarlo dependiendo de lo anterior, esto permite que haya realismo y sentido en un objeto y pueda adaptarse y simularse en diferentes ambientes de manera coherente. 
#### 8
Implica mucho más trabajo y puede ser muy pesado, un juego que utilice de manera desproporcionada muchas fuentes lumínicas se condena a ser más pesado y dificil de correr, ya que suma a la GPU más cálculos que debe hacer por superficie al querer hacer el fragment shading.

### Segundo Resumen
Para poder dibujar un triángulo en OpenGL, lo primero es decirle a la GPU cuáles son los vertices que lo forman, se definen en coordenadas normalizadas que van de -1 a 1. Luego, necesitamos guardar esa información de forma eficiente, y para eso se crean dos objetos importantes: el VBO, que almacena directamente los datos de los vértices, y el VAO, que guarda la configuración sobre cómo se deben interpretar esos datos, sus atributos, etc. Una vez creados, enviamos la información a la GPU, le decimos cómo leerla (por ejemplo, cada vértice tiene 3 coordenadas) y activamos estos objetos. Con todo listo, solo se necesita llamar a la función que dibuja (glDrawArrays) para que el triángulo aparezca en pantalla.

Por otro lado, para usar un shader necesitamos escribir un pequeño programa que se ejecuta directamente en la GPU. Este programa tiene dos partes básicas: el vertex shader, que transforma las posiciones de los vértices, y el fragment shader, que decide de qué color será cada fragmento del triángulo. Después de escribirlos, hay que compilarlos, enlazarlos en un shader program y activarlo. A partir de ese momento, cada vez que OpenGL dibuja algo, usa nuestro código para procesar los vértices y colores. Esto es lo que nos da el control creativo y técnico sobre cómo se ve y se comporta todo lo que aparece en pantalla.

<a name="6"></a>
### Implementación:
Este es el resultado al implementar las partes nuevas del código: 

<img width="411" height="449" alt="image" src="https://github.com/user-attachments/assets/460d929b-0b09-4a35-ba22-aa349aac5c6f" />

## Actividad 05
Capturas del código funcionando en la máquina

<img width="403" height="448" alt="image" src="https://github.com/user-attachments/assets/b92660d8-248b-4e0b-91f1-c2bee712ca83" />

<img width="413" height="460" alt="image" src="https://github.com/user-attachments/assets/3adfdfd6-411d-41b2-a912-ffe6637922f0" />

<img width="405" height="435" alt="image" src="https://github.com/user-attachments/assets/e7986bd9-b0fb-4297-acfe-299cc495870e" />

Normalmente las coordenadas del mouse se calculan tomando como origen la esquina superior izquierda y tomando el ancho y alto de la ventana, pero en OpenGL no se trabajan con estas sino con Coordenadas de Dispositivo (NDC).
El proceso realizado para poder normalizarlo  a NDC es el siguiente:
Primero se dividen las coordenadas del mouse entre el tamaño de la ventana, esto convierte el rango de ``[0, ancho]`` → ``[0, 1]`` en X y ``[0, alto]`` → ``[0, 1]`` en Y. Despues es necesario convertir de ``[0,1]`` a ``[-1,1]`` esto se hace multiplicando por 2 y luego restando por 1, tambien invirtiendo el eje en y ya que en las coordenadas del mouse el negativo esta arriba debido a como ubica el origen, pero para OpenGL esta abajo.

La posición del mouse la normalizamos debido a que es necesario hacer esto para poder usarlo como offset directamente, moviendo el triángulo en el mismo sistema de coordenadas que la ventana, esto es muy útil y necesario ya que de lo contrario sería como mínimo muy engorroso cambiar de sistemas de coordenadas constantemente.

# Autoevaluación
## Nota Propuesta: ``3.8/5``

### Nota Actividad 01: ``1/1``
Logré tener el primer [acercamiento](#1) al programa ejemplo y realizar preguntas importantes que serían respondidas eventualmente a lo largo de la bitácora.

### Nota Actividad 02: ``1/1``
Siento que el [resumen](#2) que realicé de lo explicado en la actividad fue adecuado, además que mientras lo realizaba logré conectar mejor los conceptos leidos y entenderlos más que solo de memoria como recitados, sino generando una conexión genuina con ellos.

### Nota Actividad 03: ``1/1``
Me siento contento y suficiente con el resultado de esta actividad ya que fui capáz de realizar un [resumen](#3) en el cual comprendia y volvia a traer a mi lo descríto anteriormente a este, y al final pude condensar todo lo aprendido en las [preguntas](#4).

### Nota Actividad 04: ``0.8/1``
Me siento bien con las respuestas a las [preguntas](#5) del video ya que siento que lo comprendí y al resumen también, pero no estoy seguro de si la [implementación](#6) fue correcta, teno haber malentendido donde poner las partes del código y que este no fuera realmente el resultado esperado, estas dudas pueden llegar de por si a representar que hay algo que no me quedó claro.

### ### Nota Actividad 05: ``1/1``
Siento que esta vez si implementé bien y logré entender el roceso de normalización.


