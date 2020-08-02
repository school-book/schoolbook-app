# SchoolBook
## Introducción
* Caso de estudio referente a una empresa que administra bibliotecas y venta de libros.
* El propósito de este proyecto es 100% académico, dirigido especialmente a estudiantes de los últimos semestres de carreras asociadas con el desarrollo de software. 
* A nivel general se implementan los conceptos básicos para realizar desarrollos multicapa así como la incorporación de conceptos básicos de la arquitectura de *micro servicios* y tecnologías asociadas. 
* Cualquier interesado en contribuir es bienvenido!
##  Arquitectura básica.
* De forma muy sencilla la arquitectura propuesta para esta aplicación se describe en la siguiente imagen. 
<span style="display:block;text-align:center">
![arquitectura](arquitectura.png)
</span>
## Preparar ambiente de desarrollo.
### Instalación de herramientas
* Instalación JDK de Java ([Open JDK](https://openjdk.java.net/)) 
* Instalación de la IDE de desarrollo [Spring Tool Suite](https://spring.io/tools)
* Uso del algún editor de texto, de preferencia [Visual Studio Code](https://code.visualstudio.com/).
* Instalación de Git.  Revisar  los siguientes documentos:
	* [Tutorial básico de Git](https://github.com/jorgerdc/tutoriales/tree/master/git)
	* [Lineamientos de desarrollo](https://github.com/jorgerdc/tutoriales/tree/master/lineamientos-desarrollo) tanto para la IDE como para el uso de github.
## Documentación y diseño
* La documentación de análisis y diseño del proyecto se estará publicando y actualizando en la carpeta `docs` de cada uno de los repositorios.
* Revisar el documento `docs/caso-estudio.md`  en el que se describe la definición de este caso de estudio y sus principales requerimientos.
* A nivel general SchoolBook se divide en los siguientes servicios:
	* Servicio encargado de la administración de contratos con escuelas y bibliotecas
	* Servicio encargado de la administración de usuarios.
	* Servicio de administración de los catálogos de libros
	* Servicio encargado de la administración de préstamos y ejemplares.
	* Servicio encargado de administrar las  ordenes de compra de libros.
## Código fuente
* El código fuente del proyecto se distribuye en diversos repositorios los cuales se pueden consultar [en este enlace.]([https://github.com/school-book/](https://github.com/school-book/)) 
