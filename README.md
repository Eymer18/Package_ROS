# Package_ROS

_Toda la documentación esta basada en clases de ROS(2021-I) sobre notas de clase y la interpretación de packages de 3ros_

## Robot RBX1 

### Primer paso: Crear un workspace

* En un primer terminal se ejecuta la siguiente sentencia para crear el workspace "catkin_ws" en home y dentro la carpeta scr
```
mkdir -p ~/catkin_ws/scr
```

* En el mismo terminal se ejecuta la siguiente sentencia para ir al workspace creado 
```
cd catkin_ws
```

* Y nuevamente en el mismo terminal se ejecuta la siguiente sentencia para compilar el workspace y empezar a crear packages dentro de el 
```
catkin_make
```

### Segundo paso: Instalar el repositorio RBX1

Para instalar directamente desde el repositorio de ROS se ejecuta la siguiente sentencia en un terminal
```
sudo apt-get install ros-kinetic-rbx1
```
_Nota: Para este repositorio se usa la distribución de kinectic, en tal caso de tener una distribución diferente, verifique y cambie la sentencia para su versión de ROS_   

O si se desea instalar desde un repositorio de github se debe hacer lo siguiente

* En un terminal para ir a la carpeta de origen del workspace se ejecuta la siguiente sentencia
```
cd ~/catkin_ws/src
```

* Y en el mismo terminal se ejecuta la siguiente sentencia para copiar el repositorio RBX1 del github del autor 
```
git clone https://github.com/pirobot/rbx1.git
```
### Tercer paso: Ejecutar el archivo _.launch_
Los archivos .launch sirven para ejecutar varios archivos o nodos al mismo tiempo, sin tener que estar ejecutando nodo por nodo en terminales diferentes. Primero debemos inicializar el entorno de ROS para poder trabajar con los nodos y demás, para ello se ejecuta la siguiente sentencia en un terminal
```
roscore
```
El paquete de RBX1 contiene varios .launch, el archivo especifico el cual se va a trabajar es _fake_turtlebot.launch_ el cual puede ser encontrado en el directorio _catkin_ws/src/rbx1/rbx1_bringup/launch_ y se ejecuta con la siguiente sentencia
```
roslaunch rbx1_bringup fake_turtlebot.launch
```
Una forma de visualizar los nodos que ejecuta un archivo .launch es mediante el _rqt_grahp_ el cual provee un elemento gráfico para visualizar topics y nodos conectados actualmente, para ejecutarlo se puede hacer mediante las siguientes sentencias
```
rosrun rqt_graph rqt_graph
```
O bien
```
rqt_graph
```
Y para visualizar graficamente el robot que ha ejecutado el archivo .launch se usa _rviz_ el cual abre una interfaz gráfica desde la cual se pueden observar distintos procesos o simulaciones en 3D para librerías que asi lo requieran en este caso cargará el modelo dentro de un entorno 3D, para ejecutarlo se hace mediante la siguiente sentencia
```
rosrun rviz rviz -d`rospack find rbx1_nav`/sim.rviz

```
