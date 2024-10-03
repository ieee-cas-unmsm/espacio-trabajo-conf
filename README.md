# Configuración de entorno - Septiembre 2024

### **Objetivos**  
> Entender la dinámica de trabajo grupal con GitHub  
> Aprender diseño de circuito impreso en KiCAD 
> Compilar y subir codigo C a microcontroladores AVR  

## Tabla de Contenidos

1. [Instalación WSL](#instalacion-WSL)
2. [Manejando la Terminal](#manejando-la-terminal)

## Instalación WSL (Windows Subsystem for Linux)
¿Nos cambiamos de sistema operativo? No. Estaremos utilizando una distribución de Linux, que es Ubuntu, dentro de Windows. La razones para hacerlos son muchas, pero, poniendolo en pocas puntos:
- Permite usar las herramientas de Linux en Windows
- Facilitará la instalación de programas a una sola linea de comando.
- Los paquetes y entorno de instalación son homogeneos.

### WSL / Ubuntu
- Ingresamos a *Powershell*, ejecutamos como administrador y ejecutamos el siguiente comando para instalar WSL 2:
```
wsl --install
```
- Terminada la isntalación de WSL 2, instalaremos Ubuntu con el siguiente comando:
```
wsl --install -d Ubuntu
```

## Comandos en la Terminal
A diferencia de Windows nuestra forma de interactuar con Ubuntu será unicamente mediante la terminal, es decir lineas de comando. Para ello es necesario saber los comandos básicos para la manipulación de carpetas y ficheros.
> Todas las acciones que se realizan se llevan acabo en la dirección actual.

### Manipulación de carpetas y ficheros
- Para ver las carpetas y ficheros visibles del directorio actual, ejecutaremos el comando:
```
ls
```
- Para ver las carpetas y ficheros **NO** visibles del directorio actual, ejecutaremos el comando:
```
la
```
> Si agregamos -l despues del comando podremos visualizar los archivos de forma vertical.

### Manipulación de carpetas y ficheros
Comandos empleados para la visualización, creación, modificación y eliminación de los archivos

- Comandos para la creación de una carpeta y archivo
  ```
  mkdir carpeta_creada          
  ```
  ```
  touch archivo_creado.txt
  ```
  > Se crearán en el directorio actual

- Comandos para mover carpetas o ficheros hacia otra dirección
    > Preparación de las carpetas y archivos para probar los comandos
  ```
  cd
  mkdir carpeta_destino
  mkdir carpeta_fuente
  cd carpeta_fuente
  touch archivo_mover.txt
  cd
  ```
    > Comando para mover
  ```
  mv carpeta_fuente/archivo_mover.txt carpeta_destino
  ```
    > Revisamos la carpeta con el archivo movido
  ```
  ls carpeta_destino
  ```
- Comandos para copiar una carpeta o fichero a otra dirección.
    > Preparación de las carpetas y archivos para probar los comandos
  ```
  cd
  mkdir carpeta_destino_A
  cd carpeta_destino_A
  mkdir carpeta_destino_B
  cd carpeta_destino_B
  mkdir carpeta_destino_C
  cd mkdir carpeta_destino_C
  touch archivo_copiar_1.txt
  touch archivo_copiar_2.c
  touch archivo_copiar_3.cpp
  cd
  ```
    > Copiando la carpeta carpeta_destino_C al directorio principal
  ```
  cd carpeta_destino_A/carpeta_destino_B
  cp -r carpeta_destino_C $HOME
  ```
    > Copiando el archivo_copiar_1.txt a carpeta_destino_B
  ```
  cp archivo_copiar_1.txt ../
  ```

Comandos para la eliminación de carpetas y archivos:
> Eliminamos la carpeta y los archivos dentro de la misma
```
rm -r carpeta_creada
```


## Git / GitHub
Ahora iniciaremos con el control de versiones GIT y los repositorios existentes en GITHUB. 
Aclararemos que utilizaremos git tanto en Windows como en Ubuntu, se espcificará antes en cual de los entornos estamos trabajando.

### Git - WSL / Ubuntu
Iniciaremos en el entorno que trabajamaos previamente, para comprobar la isntalación de Git dentro de ubuntu ejecutamos el comando:
> De forma nativa Linux incluye Git, GCC, entre otras herramientas que utilizaremos
```
git --version
```

Ahora deberemos de configurar nuestro nombre y correo que emplearemos
```
git config --global user.name "nombre_cuenta"
git config --global user.email "correo_cuenta"
```
### Comandos en el Control de Versiones
Para facilitar algunas actividades instalaremos 2 paquetes: *gedit* y *VScode*
> Primero revisaremos las actualizaciones de los paquetes instalados
```
sudo apt update
```
> Actualizaremos aquellos paquetes que tienen cambios
```
sudo apt upgrade
```

> Instalamos el paquete geddit en el entorno
```
sudo apt install geddit
```
> Instalaremos de forma no convencional VS code
```
code .
```
> Modificaremos el nombre por defecto de la rama principal
```
git config --global init.defaultBranch main
```

### Usando Git de forma Local
Github no es lo mismo a Git, es cierto que comparten comandos y funcionalidad pero, es debido a que GitHub es una plataforma desarrollada en base al Git y que opera utiliza sus comandos. Ahora nos centraremos en revisar el flujo de trabajo en archivos locales. 
- Crearemos e ingresamos a la carpeta donde haremos las modificaciones
  ```
  cd
  mkdir git_local
  cd git_local
  ```
- Inicializaremos git dentro de la carpeta de trabajo
  > Podemos usar el comando la -l para visualizar la carpeta no visible creada .git
  ```
  git init
  la -l
  ```
- Crearemos un archivo y una carpeta
  ```
  mkdir primera_carpeta
  touch primer_archivo.c
  ```
- Revisaremos el estado actual de nuestra carpeta inicializada
  > Observaremos que existen archivos no "trackeados", es decir sin seguimiento para el control de versiones
  ```
  git status
  ```
- Aggregaremos ambos archivos al flujo de git
  > Al emplear add . implica que todos los archivos de la dirección pasan a ser trackeados
  > Para deshacer se emplea git reset para eliminar a los archivos del track
  ```
  git add .
  ```

- Commit a los archivos agregados al git
  Lo primero por definir es que la etapa del commit no se realiza en cada momento o de forma repetitiva, si no se busca crear commit en puntos claves del desarrollo de nuestro proyecto.
  > Al ser nuestro primer commit será el punto máximo de retorno
  > -m es la indicación que será un mensaje breve
  ```
  git commit -m "Añadi el archivo primer_archivo y el directorio primera_carpeta"
  ```
- Verificamos nuestra rama principal
  > Las ramas en GIT hacen referencia espacios de trabajo independientes, siendo main la principal / official del proyecto
  ```
  git status
  ```

- Modificación de archivos 
