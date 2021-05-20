# ROS_Package_RBX1

_Toda la documentación esta basada en clases de ROS(2021-I) sobre notas de clase y la interpretación de packages de 3ros_

## Robot RBX1 

### Primer paso: Crear un workspace

* En un primer terminal se ejecuta la siguiente sentencia para crear el workspace "catkin_ws" en home y dentro la carpeta scr:
```
mkdir -p ~/catkin_ws/scr
```

* En el mismo terminal se ejecuta la siguiente sentencia para ir al workspace creado: 
```
cd catkin_ws
```

* Y nuevamente en el mismo terminal se ejecuta la siguiente sentencia para compilar el workspace y empezar a crear packages dentro de el: 
```
catkin_make
```

### Segundo paso: Instalar el repositorio RBX1

Para instalar directamente desde el repositorio de ROS se ejecuta la siguiente sentencia en un terminal:
```
sudo apt-get install ros-kinetic-rbx1
```
_Nota: Para este repositorio se usa la distribución de kinectic, en tal caso de tener una distribución diferente, verifique y cambie la sentencia para su versión de ROS_   

O si se desea instalar desde un repositorio de github se debe hacer lo siguiente:

* En un terminal para ir a la carpeta de origen del workspace se ejecuta la siguiente sentencia:
```
cd ~/catkin_ws/src
```

* Y en el mismo terminal se ejecuta la siguiente sentencia para copiar el repositorio RBX1 del github del autor: 
```
git clone https://github.com/pirobot/rbx1.git
```
### Tercer paso: Ejecutar el archivo _.launch_
Los archivos .launch sirven para ejecutar varios archivos o nodos al mismo tiempo, sin tener que estar ejecutando nodo por nodo en terminales diferentes. Primero debemos inicializar el entorno de ROS para poder trabajar con los nodos y demás, para ello se ejecuta la siguiente sentencia en un terminal:
```
roscore
```
El paquete de RBX1 contiene varios .launch, el archivo especifico el cual se va a trabajar es _fake_turtlebot.launch_ el cual puede ser encontrado en el directorio _catkin_ws/src/rbx1/rbx1_bringup/launch_ y se ejecuta con la siguiente sentencia:
```
roslaunch rbx1_bringup fake_turtlebot.launch
```
Una forma de visualizar los nodos que ejecuta un archivo .launch es mediante el _rqt_grahp_ el cual provee un elemento gráfico para visualizar topics y nodos conectados actualmente, para ejecutarlo se puede hacer mediante las siguientes sentencias:
```
rosrun rqt_graph rqt_graph
```
O bien:
```
rqt_graph
```
Y para visualizar graficamente el robot que ha ejecutado el archivo .launch se usa _rviz_ el cual abre una interfaz gráfica desde la cual se pueden observar distintos procesos o simulaciones en 3D para librerías que asi lo requieran en este caso cargará el modelo dentro de un entorno 3D, para ejecutarlo se hace mediante la siguiente sentencia:
```
rosrun rviz rviz -d`rospack find rbx1_nav`/sim.rviz
```
### Cuarto paso: Modificar el archivo _.launch_ 
Para este ejemplo modificaremos el archivo con el cual estamos trabajando _fake_turtlebot.launch_. En este caso en especifico, se modificará un topic dentro del archivo para que el robot RBX1 sea compatible con la característica teleop_key del ejemplo de turtlebot incluido en ROS.
_Nota: Para realizar este paso, se debe haber realizado el tercer paso correctamente_

* En un terminal nuevo para utilizar el teleoperador, es necesario ejecutar la siguiente sentencia:
```
rosrun turtlesim turtle_teleop_key
```
* Y en otro terminal para saber el topic a modificar, se ejecuta la siguiente sentencia:
```
rostopic list
```
En los topics actuales, se aprecia que hay dos topics similares: _/cmd_vel_ y _/turtle1/cmd_vel_. El topic a modificar es precisamente _/turtle1/cmd_vel, al matar el proceso _teleop_key_ se puede ver que el topic llamado _/turtle1/cmd_vel_ desaparecerá. Para realizar los cambios se debe hacer lo siguiente:

* Primero hay que dirigirse al directorio en especifico que contiene el _.launch_ el cual mecione antes _catkin_ws/src/rbx1/rbx1_bringup/launch_. Se puede buscar en los archivos directamente yendo a la carpeta o acceder a el mediante la siguiente sentencia:
```
cd ~/catkin_ws/src/rbx1/rbx1_bringup/launch
```
* Si se accedió mediante la carpeta se puede abrir el archivo con cualquier editor de texto, y si fue mediante el terminal la mejor forma de editarlo graficamente es con la siguiente sentencia:
```
gedit fake_turtlebot.launch
```
* Dentro del archivo se debe buscar la parte del código que ejecuta el nodo llamado _arbotix_ marcado con los símbolos </>, en una nueva línea dentro de este segmento de código se debe escribir lo siguiente:
```
<remap from="/cmd_vel" to="/turtle1/cmd_vel"/>
```
* Finalmente se debe guardar, se matan los procesos en ejecución y se repite el paso 3 junto con la sentencia del teleoperador. Ahora se puede controlar el robot _arbotix RBX1_ dentro del entorno _rviz_ con la característica _teleop_key_ del ejemplo del bot de turtle ROS. 

_NOTA: En este repositorio dejo adjunto el archivo .launch modificado para comprobar los cambios o si lo desea reemplezar con el de su proyecto_ 


## Autor

* Eymer S. Tapias
