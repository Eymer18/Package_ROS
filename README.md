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
