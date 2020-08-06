# SchoolBook
## 1. Caso de estudio
* SchoolBook es una empresa que se dedica a 3 principales actividades:
	* Administrar la operación de las bibliotecas de escuelas con las que la empresa tiene contratos.
	* Realizar el control de compra, venta y distribución de libros que requieren las bibliotecas.
	* Administrar la operación de sus tiendas de libros tanto físicas como virtuales. 
### 1.1 Administración de contratos.
* Escuelas en general contratan los servicios de *SchoolBook* para llevar el control de  sus bibliotecas. 
* Una vez que la escuela y SchoolBook acuerdan los términos y condiciones, el administrador de SchoolBook realiza el registro de un contrato que contiene los siguientes datos: número de contrato, fecha inicio y fin del contrato, nombre de la escuela o institución, clave escolar,  responsable del contrato (generalmente el director de la escuela).
* En el detalle del contrato también se especifica la lista de bibliotecas que serán administradas por  SchoolBook.  Para cada biblioteca se registra la siguiente información:  Nombre, dirección,  ubicación geográfica (latitud, longitud), dirección de su página web,  teléfonos de contacto, número aproximado de ejemplares que maneja,  número aproximado de usuarios que maneja.
* Con base en estos datos, en el contrato se especifica la cuota mensual que la escuela deberá pagar para cada una de las bibliotecas.   Una  vez que el contrato es firmado, se obtiene una copia en formato PDF el cual se almacena en base de datos.
* La escuela puede renovar su contrato las veces que así lo desee. En realidad renovar un contrato significa generar uno nuevo con las mismas condiciones y asociarlo con el contrato anterior. La cuota mensual puede cambiar al renovar.
* Para realizar los pagos mensuales, la escuela puede proporcionar varios números de tarjeta de crédito. Se registra el número de tarjeta, su tipo, mes y año de expiración y número de seguridad.
* Para realizar los pagos, a cada biblioteca se le asigna una de las tarjetas de crédito registradas por parte de la escuela.
* Cada vez que se realiza un cargo a una tarjeta se guarda el importe, la fecha del cobro y el número de operación que genera el banco.
* Para llevar el control de las bibliotecas se cuenta con los siguientes estados:

Status   | Descripción
--       | --
ACTIVA   | La biblioteca está al día con sus pagos y con contrato vigente.
CON PAGO PENDIENTE | El cargo a la tarjeta de la biblioteca no pudo ser realizado. Si el pago no se realiza posterior a los 15 días posteriores, los servicios se suspenden en esta biblioteca.
CON CONTRATO VENCIDO | El contrato de la escuela asociado a vencido. En caso de no existir renovación, el servicio se suspende para la biblioteca en cuestión. 

### 1.2 Operación de las bibliotecas.
* SchoolBook realiza el control de la operación de cada biblioteca a través de un sistema web.   Las principales funcionalidades del sistema se describen a continuación.
#### Registro de usuarios.
* Se cuenta con un registro único de usuarios. Este registro le permite al usuario estudiante poder acceder al acervo de cualquiera de las bibliotecas de su escuela.  Se registra nombre, apellidos, escuela a la que pertenece, email,  username, password, al menos un teléfono, número de cuenta o matrícula y foto tamaño infantil la cual es tomada al momento de realizar el registro. 
#### Registro de Libros.
* SchoolBook cuenta con un catálogo global de registro de libros.  Se almacenan los siguientes datos:  Título,  ISBN, editorial, lista de autores, edición, año de publicación, número de páginas. Se cuenta con un catálogo de editoriales que incluye nombre, dirección de sus oficinas centrales, teléfono, dirección de su página web. 
* Existen 2 formatos para cada libro: físico y digital.  
* Para los libros físicos se almacena el número total de ejemplares existentes, el número total de ejemplares que se encuentran ubicados en bibliotecas, el número total de ejemplares que se encuentran el almacén, el número total de libros vendidos en librerías, y el número total de libros que se consideran como perdidos, ya sea por robo, maltrato, o pérdida por alguna razón.
* Para los libros digitales se almacena su URL donde puede ser consultado y el número de archivos que contiene el contenido del  libro. 
* Cada libro digital se almacena en varios archivos. Se almacena el archivo,  su número iniciando en 1 por cada libro, el rango de páginas que contiene cada archivo, nombre del archivo, formato y tamaño en bytes.
* Algunos libros digitales incluyen material multimedia, archivos de audio y/o archivos de vídeo.  Para cada archivo se registra un número de archivo,  su tipo (vídeo, audio, etc.), su formato (mp3, mp4, etc.),  y una descripción.
* Independiente al tipo de libro se almacenan los siguientes datos que permiten facilitar su búsqueda:
	* Imagen que representa a la portada
	* Imagen que representa a la contra portada
	* Archivo PDF que contiene la tabla de contenido del libro.
	* Lista de palabras clave que se usan en búsqueda de hasta 20 palabras.
	* Resumen de hasta 500 caracteres.
* Para propósitos de venta, SchoolBook almacena el precio de venta de sus libros. Almacena tanto el precio de un ejemplar como el precio de un libro en formato digital. 
* Se requiere llevar el control del cambio de precios a lo largo del tiempo para cada libro. 
#### Control  de ejemplares en bibliotecas
* Cuando un ejemplar es asignado a una biblioteca, se debe registrar en base de datos esta asociación,  su número de clasificación, así como la fecha de asignación. 
* A cada ejemplar se le asocia un folio iniciando en 001.
* Este folio de ejemplar se incluye en una etiqueta junto al número de clasificación que se pega en el lomo del ejemplar así como su número de clasificación que permite ubicar a libro dentro de la biblioteca.
* Para determinar la ubicación del ejemplar dentro de la biblioteca se emplea una cadena con el siguiente formato.  Suponer que un libro se encuentra en el piso 3, sala norte, sección M,  anaquel 5,  renglón 3.  Su cadena será:  `PS3-SAN-SEM-AN5-R3` . Cada biblioteca puede definir el formato de esta cadena.
* Para llevar el control de los ejemplares con los que cuenta una biblioteca se ha diseñado una serie de status.

|Status            |Descripción
| ---              | ---------- 
|DISPONIBLE        | El ejemplar se encuentra en la biblioteca y está disponible para ser incluido en préstamos solicitados por los usuarios.
|DISPONIBLE EN BIBLIO | El ejemplar se encuentra en biblioteca, puede ser consultado, pero no puede ser incluido en solicitudes de préstamo.
| BAJA POR ROBO O EXTRAVIO | El ejemplar se considera como perdido debido a un robo o extravío.
| BAJA POR DAÑO   | El ejemplar se considera como perdido debido a un daño físico irreparable por lo que ya no puede continuar en uso.
| EN PRESTAMO     | El ejemplar ha sido prestado a un usuario, se encuentra dentro del periodo de vigencia del préstamo.
| EN PRESTAMO CON RETARDO  | El ejemplar ha sido prestado a un usuario, pero el periodo para ser regresado a la biblioteca ha expirado
| EN REPARACIÓN | El ejemplar presenta daños que pueden ser reparados. Mientras el ejemplar no sea reparado permanecerá en este estado.
* Se requiere contar con histórico de status.
### 1.3 Control de préstamos
* Los préstamos aplican a ambos tipos de libros (ejemplares y digitales).
* El usuario solicita un préstamo, se genera un folio de 13 caracteres.  Se registra la fecha de inicio del préstamo. La fecha de entrega se asigna a cada ejemplar.
* Para el caso de los libros digitales, se habilita una clave de acceso de 5 caracteres que será empleada para acceder al contenido del libro desde Internet.  Una vez que la fecha de entrega del libro ha expirado, el sistema ya no permitirá acceder a su contenido.
* De forma similar a los libros, se lleva un control de status de préstamos

Status  |Descripción  
 ---        | --- 
VIGENTE     | El préstamo se ha otorgado y las fechas de entrega de cada uno de sus ejemplares aún no expiran.
EXPIRADO    | Por lo menos una de las fechas de entrega de los ejemplares del préstamo ha expirado sin haber sido entregado a la biblioteca.  Cuando esto ocurre, el usuario se le otorgarán 2 días adicionales antes de establecer una multa.
CON MULTA   | El usuario aún no ha realizado la entrega del préstamo, tiene al menos un ejemplar con fecha de entrega expirada y han pasado los 2 días que el sistema otorga para regresar los ejemplares. El importe de la multa a pagar se establecerá una vez que el usuario regrese todos los ejemplares del préstamo a la biblioteca.
ENTREGADO  | El usuario ha devuelto todos los ejemplares a la biblioteca en buen estado y sin contar con fechas de entrega expiradas.
ENTREGADO CON MULTA | El usuario ha devuelto los ejemplares, pero se detecta que el usuario debe pagar multa por alguno de los siguientes escenarios: 1. El usuario no realizó la entrega de sus ejemplares en las fechas establecidas.  2. El usuario regresó los ejemplares con daños o no los regresa por pérdida.  En el momento de la entrega, se asigna la multa al usuario. Dependiendo el daño, el operador del sistema podrá dar de baja al ejemplar o marcarlo como EN REPARACIÓN.
* Se requiere llevar el control de un histórico de estos status.
#### Surtido de libros para bibliotecas.
* Las bibliotecas pueden solicitar a SchoolBook el surtido ya sea de ejemplares existentes o de nuevos libros que no se encuentran en el catálogo de SchoolBook.  
* Para realizar el surtido de ejemplares se requiere registrar una solicitud.   Se almacena un folio de solicitud, fecha de solicitud,  usuario que realiza el pedido (generalmente el administrador de la biblioteca).
* Como parte del detalle de la solicitud se guarda la lista de los libros solicitados: Título, editorial , edición, autores (no se requiere desglosar, se registra una sola cadena), tipo de libro (físico, digital o ambos), y número de ejemplares (para libros físicos).  
* Una vez que la solicitud se registra, se inicia el proceso de compra a través del registro de una orden de compra en el sitio web de SchoolBook la cual se describe a continuación.  
* Cabe mencionar que SchoolBook generalmente aplica descuentos  a las ordenes de compra que las bibliotecas solicitan debido al contrato laboral que tienen con la empresa.
### 1.4 Venta de libros.
* SchoolBook también ofrece  el servicio de venta de libros a través de su sitio web. Para realizar una compra, los usuarios generan una orden de compra. Se registra la fecha de la orden y la lista de libros. 
* Los usuarios que desean comprar libros deben registrar los datos de al menos una tarjeta de crédito (número, tipo, año y mes de expiración, número de seguridad).   Se requiere registrar de forma obligatoria  su fecha de registro,  y su dirección de entrega (calle, número, código postal , municipio/delegación/alcaldía/ciudad,  estado y país).  La dirección se almacena en un solo campo. También se almacena la latitud y longitud de dicha dirección para facilitar la ubicación del domicilio de entrega.
* Cabe mencionar que los usuarios registrados que pertenecen a las escuelas mencionadas anteriormente, pueden hacer uso de sus datos para realizar compras en el sitio web.  Solo deberán registrar los datos de sus tarjetas y de su dirección de envío.
* Para usuarios que no pertenecen a las escuelas, estos no podrán acceder a los préstamos  que son ofrecidos por las escuelas.
* El sistema web ofrece la funcionalidad clásica del *carrito de compras*.
* Nuevamente, el control de una orden de compra se realiza a través de la aplicación de una serie de estados.

Status | Descripción
---    | ---
REGISTRADA | La orden de compra está registrada pero aún no ha sido pagada.
PAGADA |  La orden ha sido pagada sin contratiempos empleando la tarjeta del usuario.
RECHAZADA | La orden no pudo ser pagada empleando la tarjeta del usuario.
ENVIADA | Se ha generado un paquete y este ha sido enviado para su entrega. Durante este estado, el usuario puede monitorear el lugar y la fecha de llegada en las diferentes escalas que realice el paquete empleando un Id de seguimiento que proporciona la empresa de paquetería.
ENTREGADA | La orden de compra fue entregada satisfactoriamente al usuario en su domicilio.
DEVUELTA | La orden de compra no pudo ser entregada. Se almacena el motivo de su devolución
* Para el caso de los libros digitales, el  sistema no realiza envío.  En este caso se le proporcionará un PDF al usuario que podrá ser descargado. Por seguridad, cada página del PDF tendrá como pie de página la leyenda 
``` 
Libro bajo licencia para el usuario  {usuario} ({email})
```
* Como parte de las funcionalidades del sitio web, los usuarios podrán hacer búsquedas de sus libros.  El sistema muestra algunas imágenes representativas del libro (similar a la página de Amazon).  
* También se ofrece la funcionalidad de calificar a cada libro hasta con 5 estrellas así como del registro de comentarios, preguntas y respuestas acerca del contenido de cada libro.
### 1.5 Usuarios de las aplicaciones.
* SchoolBook ha definido varios roles de usuarios.

Rol | Descripción
--- | ---
Estudiante |  Usuario inscrito en una escuela que puede realizar préstamos así como realizar compras en línea.
Admin SchoolBook | Usuario encargado de realizar operaciones administrativas como son: registro de contratos entre la Escuela y SchoolBook, registro de nuevas bibliotecas.
Admin biblioteca | Usuario encargado de realizar operaciones de administración en el sistema de control de bibliotecas: Controlar préstamos, capturar solicitudes de surtido de libros.
Cliente | Usuario que no es alumno de una escuela cuya función es realizar compras en el sistema web.
Admin Web | Usuario que realiza tareas administrativas en el sitio web de venta de libros. Por ejemplo, autorizar comentarios, procesar solicitudes de surtidos capturados por las escuelas, administrar el catálogo de libros, solicitar surtido de libros a las editoriales en caso de requerirse, etc.





