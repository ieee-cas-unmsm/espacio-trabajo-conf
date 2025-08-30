# Configuración de entorno - Septiembre 2024
Realizando modificaciones de prueba
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


## Git
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

### Usando Git
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
  > Modificaremos el contenido del archivo primer_archivo.c
  ```
  gedit primer_archivo.c
  ```
  > Se abrirá una nueva ventano donde codificaremos lo siguiente, mas adelante compilaremos y ejecutaremos.
  ```
  #include <stdio.h>
  int main(){
	  for (int i=0; i<10;i++){
		  printf("%d\n",i);
	  }
  }
  ```
  Ingresaremos a primera_carpeta y añadiremos un documento de texto
  > Ingresa al documento utilizando *vim* o *nano* y modifica su contenido
  ```
  cd primera_carpeta
  touch documento.txt
  ```
  Observaremos los cambios en el control de versiones
  > Describirá los cambios ocurridos
  ```
  git status
  ```
  Añadiremos y Commitearemos el desarrollo
  ```
  git add .
  git commit -m "Modificación primer_archivo y nuevo archivo en carpeta"
  ```
- Creación de una nueva branch (rama)
  Las ramas son empleadas para hacer cambios seguros al documento oficial. Debido a que se crea una copia identica de los documentos trackeados.
  > Creamos una branch llamada nueva_rama y nos movemos usando checkout
  ```
  git branch rama_nueva
  git checkout rama_nueva
  ```
  > Podemos simplificar cuando recien la crearemos
  ```
  git branch -b rama_nueva
  ```
  Modificaremos el documento primer_documento.c de la siguietne forma:
  > Recordar que debemos de ingresar utilizando algun visor de texto
  ```
  #include <stdio.h>
  int main(){
	  for (int i=0; i<10;i++){
		  printf("%d\n",i*i);
	  }
  }
  ```
  Agregaremos un nuevo archivo dentro de la carpeta y tambien modificaremos el existente
  > Nuevo archivo
  ```
  touch documento2.txt
  ```
  > Modificar archivo
  ```
  Hola esta es una modificacion en la branch: nueva_rama
  ```
  Repetiremos el proceso de añadir y commit
- Moviendonos entre commits
  Una gran funcionalidad de git es el hecho de que todo lo que has realizado puede recuperarse. Restaurar versiones anteriores, explorar ramas y juntarlas o merge, que veremos mas adelante.
  > Visualizamos
  ```
  git log
  ```
  > Visualización mas ordenada
  ```
  git log --oneline
  ```
  Para saltar entre los commits podemos emplear las primeras letras identificadores de cada branch
  > En este caso puede que cada uno tenga un número diferente, estar atento.
  ```
  git checkout "segundo commit numero"
  ```
  Revisar la lista de los commit realizados, bueno ahora unicamente tenemos el anterior. Los cambios superiro no estan disponibles para observarlos, sin embargo, podemos dirigirnos ahí.
  > Revisamos los commits disponibles
  ```
  git log --oneline
  ```
  > Regresamos a nuestro commit inicial
  ```
  git 
  ```
- Merge y culminación de una rama
  Finalmente, la ultima parte antes de llegar al KiCAD y parte de la programación es entender a fusionar estos cambios
  > Nos situaremos en la rama main (principal) y en el último commit
  ```
  git checkout main
  git checkout "ultimo_commit"
  ```
  Realizamos el proceso de merge con la branch: "rama_nueva"
  > Consideraciones
  ```
  git merge rama_actual rama_nueva
  ```
  > Deberemos de solucionar los problemas
  Finalmente exploramos los archivos y observamos los cambios jiji


## KiCAD
Para ello cada uno de nosotros trabajaremos en un archivo del 
  
