# Laboratorio Robótica Industrial No. 1
# Miembros:
Edgar Giovanny Obregon Espitia

Juan Nicolas Carvajal Useche
# Descripción de la solución planteada
1. Simulación en RobotStudio
La solución propuesta para simular la decoración de un pastel de 20 personas utilizando un robot
manipulador incluye el desarrollo de un programa en Rapid de Robot Studio, que puede ser
ejecutado en un entorno de simulación y en un robot real. El objetivo principal es que el robot real
sea capaz de decorar el pastel siguiendo un diseño específico en nuestro caso la forma de un fénix
y escribir las primeras cinco letras de los nombres de los participantes en el pastel. Para lograrlo, se
diseñará e implementará una herramienta final personalizada que sujetará un marcador para
realizar las escrituras.
Se creará un programa detallado en Robot Studio que incluirá los movimientos y las acciones
necesarias para decorar el pastel. Esto implicará la programación de los movimientos del robot,
movJ y movL según el caso, la importación de la herramienta diseñada, y la orientación de esta. Por
lo que se inicia importando los CAD de la herramienta y el workobject, para después ajustarlos a las
medidas estipuladas en el plano de planta, la herramienta también se puso en la brida del robot del
simulador. Los workobject fueron creados en inventor y allí mismo se realizó el grabado de las
formas que se deseaban (tanto las letras de los nombres como la figura), por lo que en el entorno
de robotstudio ya se tenían los caminos. Se preparó la estación y luego se activó el controlador
virtual, aquí fue donde comenzó la programación de las trayectorias, definiendo primero los
sistemas de coordenadas en la punta de la herramienta, luego se crearon los puntos para definir la
trayectoria del robot, como el camino ya estaba grabado, fue crear primero el camino hacia la
posición inicial desde el home del robot, luego, a la posición inicial de la trayectoria que es la parte
superior del fénix, aquí se pusieron los puntos convenientemente para los movimientos suaves de
las articulaciones del robot a lo largo de todo el camino. Luego, se hizo la rutina para el regreso a
home.
Del mismo modo se realizó para el plano inclinado, cargando el workobject con a inclinación
deseada, se realizó el mismo procedimiento para crear los caminos y los puntos.
Antes de ejecutar el programa en el robot real, se realizarán simulaciones en el entorno de Robot
Studio. También se garantizará que la herramienta se ajuste de manera adecuada al brazo del robot.
Por último, el robot real ejecutará el programa completo. Esto incluirá la aplicación del diseño del
fénix y la escritura de las primeras cinco letras de los nombres de los participantes en el pastel
utilizando el marcador sostenido por el actuador final.
2. Montaje experimental físico
Habiendo verificado las trayectorias en simulación usando la herramienta, y verificando que el
código no tuviera ningún error, se exporta el código en RAPID a una USB que es insertada al puerto
del FlexPendant, aquí se carga el archivo al controlador físico.
El programa cuenta con una rutina de GoHome, que es la primera en ejecutarse. Por sugerencia del
profesor, primero se ensayó la rutina sin herramienta, siendo sumamente cuidadosos y pendientes
de que no existieran colisiones o posibles daños al robot de ningún tipo, esta rutina se realizó
exitosamente, por lo que ahora se dispuso a ponerle la herramienta diseñada a la brida del robot.
De nuevo, se ensayó la rutina SIN usar el “workobject”, es decir, sin ponerle superficies al robot
donde escribir, sino que se siguió ensayando al aire, esto para poder prevenir accidentes y
determinar si la trayectoria era correcta o si poseía algún tipo de incertidumbre mayor, al realizar la
rutina con la herramienta pero sin su superficie para escribir, no ocurrió ningún tipo de accidente ni
tampoco colisiones, por lo que se pasó a la prueba final que era ponerle la superficie para que
escriba el robot.
En este punto, para “simular” el pastel, se usó un tablero para marcador borrable y se ajustó la
altura de este con diversas tablas del laboratorio, se observaron varios problemas, el primero es que
el workobject fue creado con una altura que no se podía montar con las tablas del laboratorio, por
lo que después de esto se recalibró el workobject y se regeneró la trayectoria. Al realizar el primer
intento se observa que la superficie está desalineada debido a la disposición en sí del laboratorio,
por lo que se tuvo que reajustar iterativamente el workobject y la superficie del laboratorio para
poder lograr el objetivo de escribir en superficie plana.
Ahora, para la rutina de plano inclinado se realizó un procedimiento de calibración del plano
fijando 3 puntos para las 3 esquinas del tablero que simula el pastel con el fin de determinar la
inclinación real de este para recalibrar el workobject del código. Después de esto, y corrigiendo los
desniveles del montaje se realiza la rutina sin ningún tipo de problemas, dando por finalizada la
práctica de laboratorio.
# Diagrama Flujo
![image](https://github.com/Ggio0/Robot_lab1/assets/82681128/f85e1831-3d79-45ad-b60b-7b7bc117f9a9)
https://github.com/Ggio0/Robot_lab1/blob/main/Entregables/DiagramaDeFlujo/DiagramaFlujo.pdf
# Plano de planta 
![image](https://github.com/Ggio0/Robot_lab1/assets/82681128/27aff2d6-9c66-4992-b47a-afe5e9fd9f19)
https://github.com/Ggio0/Robot_lab1/blob/main/Entregables/PlanoPlanta/PlanoPlanta.pdf
# Descripción de las funciones utilizadas.
Las funciones utilizadas en el código de RAPID fueron principalmente dos, movJ y movL.
MovJ es una función que se utiliza para realizar movimientos de trayectoria en el espacio utilizando
interpolación joint (articulación). Esta función fue utilizada para trayectorias como el movimiento a
la posición "home" (posición de inicio), estableciendo ceros para la herramienta (posición de
referencia), y la aproximación al pastel. Se especifica que se realizó con una velocidad de 1000, lo
que indica la rapidez con la que el robot se desplaza, y un valor de z igual a 5.
MovL se utiliza para realizar movimientos de trayectoria en el espacio utilizando interpolación lineal.
En este caso, el robot se mueve siguiendo una línea recta en el espacio de trabajo. En el código, se
menciona que se usó cuando se realizan rutinas sobre el pastel, lo que implica los movimientos de
escritura o decoración en el pastel. Se especifica que se realizó con una velocidad de 100 para trazos
y una velocidad de 500 cuando el actuador final necesita acercarse o alejarse ligeramente del pastel,
para realizar un movimiento más rápido para cambios de posición.
Fue con base en estas dos funciones que se crearon las rutinas de movimiento del robot, en el código
se puede distinguir rutinas para cada letra y para el fénix, así como el retorno a home. Esto se puede
observar mejor en el código de RAPID.
# Diseño de la herramienta
La herramienta fue diseñada para impresión 3D, por lo que ahora se explicará el proceso de
modelado. El explosionado se muestra en la siguiente figura.
![image](https://github.com/Ggio0/Robot_lab1/assets/82681128/ce435dab-19a1-49db-b8aa-1daa6e79681d)
El modelado de esta y la herramienta ya fabricada se puede apreciar en las siguientes figuras.
![image](https://github.com/Ggio0/Robot_lab1/assets/82681128/419d1eb2-a976-49b8-8e8b-2d9fc8ff79ff)
Para mas informacion remitirse al apartado del git Diseño de herramienta.
https://github.com/Ggio0/Robot_lab1/blob/main/Entregables/DiseñoHerramienta/Diseño_herramienta.pdf
# Codigo en Rapid
Programa en robot studio usado para el desarrollo de la practica.
https://github.com/Ggio0/Robot_lab1/tree/main/Entregables/CodigoRAPID/Robot_lab1-main
# Video 
Video del robot en el plano horizontal.

https://github.com/Ggio0/Robot_lab1/assets/82681128/fef23a7d-0e4a-4764-8e38-4d0a4809387a

Video del robot en plano inclinado.

https://github.com/Ggio0/Robot_lab1/assets/82681128/6565816e-26cd-4f1f-ad39-eb8d0186d6ca

Video de la simulacion.

https://github.com/Ggio0/Robot_lab1/assets/82681128/a3b8d581-4c41-437f-96cf-162f7a9a47f7

ver en mejor calidad.
https://github.com/Ggio0/Robot_lab1/tree/main/Entregables/Videos







