# Bitácora de aprendizaje de la unidad 7

## Actividad 01
### 1.
Esto es lo que sale al momento de ejecutar el programa, un tirangulo naranja, no se si tendrá algo relacionado con el programa o algo que se vaya a explicar pero me percaté de que el tamaño del triángulo depende de el tamaño de la ventana, si esta se acorta este también, y no recuerdo si en programas pasados pasaba lo mismo o solo se reducia el rango de visión del programa sin afectar su tamaño.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/5019023a-b0b9-4c54-87fb-72aa1c81908a" />

<img width="872" height="964" alt="image" src="https://github.com/user-attachments/assets/abab76d8-6c38-490e-ab7f-0f36862b97f5" />

### 3.
-¿Porqué se utiliza repetidamente el "gl"?
-¿De donde saca los compíladores de shaders y en general todas estas referencias a objetos relacionados con renders?
-¿Que es VAO/VBO?

## Actividad 02
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
Hasta ahora hemos aprendido como se establece el contexto inicial de OpenGL y que necesita para funcionar correctamente, ahora empezamos a entender como es que define un contexto en el cual "dibujar" para esto se ayuda de ``GLFW`` que fue algo definido anteriormente, esta le permite poder generar un contexto en el cual "dibujar" y es multiplataforma lo que evita tener que cuadrarlo para la plataforma específica donde se hace. OpenGL no es quien dibuja realente sino que lo hace la GPU pero es OpenGL quien le brinda el contexto y le "explica" como utilizarlo y como dibujar lo que le pedimos. El espacio donde dibuja esto es el framebuffer que es un espacio en la memoria designado para dibujar inicialmente lo que se desea hacer, esto se muestra finalmente en la pantalla, el viewport define que espacio del buffer es visible, debe de ajustarse correctamente con este último de lo contrario se alterará la imagen, ahora las preguntas que me surgen es ¿como es que al cuadrar la ventana se ajusta correctamente el triángulo?, el que pasaría si no se tuviera un espacio así sino que se mostrara directamente en pantalla, o es indispensable este espacio aparte donde se dibuja inicialmente? ¿Que pasa si el tamaño del viewport es mayor al del buffer, que es entonces lo que se observa? Esto útlimo lo intenté hacer más arriba (si es que entendí bien como funcionaba la línea de código) pero solo no aparecia nada, ¿es esto porque al ser más grande que el buffer no aparece nada?
### Segundo experimento
Al jugar cambiando parámetros en ``glDrawArrays`` sale algo como esto al cambiar por lines y 4 al final

<img width="425" height="473" alt="image" src="https://github.com/user-attachments/assets/460d54a8-1518-4979-b60a-c639ec564edd" />

si se cambia a Points no se ve nada, quizas se esten dibujando los puntos pero son casi invisibles para mi, si se cambia a 2 al final pero teniendo triangles desaparece el triángulo y si lo cambio a 4 sigue apareciendo sin ningún cambio lo cual me parece raro.
### Preguntas
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
#### 1
Vertex Shading: 
Rasterization:
Fragment Shading: En esta se toman los vertices de la figura formada


