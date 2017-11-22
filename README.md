# AM_Proyect

Implemente un paquete en Integration Services el cual se encargue de realizar las siguientes acciones:
•	Se conecte a un sitio ftp en particular, a una ruta específica y traiga al sistema operativo local todos los archivos que ahí se encuentren. Tanto la dirección del sitio, como la ruta de conexión y las credenciales son valores leídos de una tabla de parámetros en sql server.
•	Mediante algún utilitario de descompresión ejecutable desde línea de comandos, puede ser 7-zip o WinRar, se hace una invocación al sistema operativo y todos los archivos se descomprimen en la ruta que el programa lo espera utilizando el passsword que se requiere.  Tanto el password de encripción de los archivos como el comando y los demás elementos que usted requiera, deben leerse de la misma tabla de parámetros mencionada en el punto anterior.
•	Mediante un componente for each file enumerator, todos los archivos se intentan cargar a una tabla particular.  Por cada archivo que se procese exitosamente, el sistema registra en la tabla de bitácora la siguiente información:
o	Nombre del archivo cargado.
o	Fecha y hora en que inició la carga.
o	Cantidad de registros cargados exitosamente.
o	Fecha y hora en que finalizó la carga.
•	Si en la tabla de bitácora ya se encuentra previamente cargado un archivo con nombre igual al que se está procesando y con una cantidad de registros procesados mayor estricta a cero (0), el archivo NO se carga nuevamente, sino que se rechaza; sin embargo, en la tabla de bitácora se registran todos los datos y la cantidad de registros cargados es cero (0).
•	Una vez que los archivos de texto han sido procesados, éstos deben ser eliminados físicamente de la ruta del sistema operativo en que fueron copiados, de modo que no se corra el riesgo de reprocesarlos.
•	Una vez que los archivos descargados por ftp han sido procesados, éstos deben ser eliminados físicamente de la ruta del sistema operativo en que fueron copiados, de modo que no se corra el riesgo de reprocesarlos.

Calendarización de la ejecución del paquete.
•	Se debe realizar la configuración para que el paquete sea publicado dentro del motor y, con la ayuda del agente de sql server, se calendariza su ejecución, por decir algo, cada 15 minutos.

Entregables:
•	Se debe mantener el código correspondiente al paquete y a la creación de las tablas de la base de datos, así como los datos de cada una de ellas, en un proyecto en github el cual será utilizado por todo el equipo.  Por este motivo, el código no es parte de los entregables; sin embargo, el proyecto sí debe contar con los diferentes y significativos aportes de todos los  miembros del equipo.
•	Se debe subir al aula virtual un documento en Word el cual contiene el url del repositorio de github, los nombres de los integrantes del curso, y un análisis de resultados en el cual se describa cuáles requerimientos se cumplieron completamente, cuáles a medias y cuáles no se iniciaron.  Para los que se realizaron al 100%, debe aportar pantallas de evidencia suficiente y competente que demuestren, a simple vista, sin necesidad de restaurar su proyecto ni de parametrizar ningún motor, que, efectivamente, todos los escenarios posibles de ese requerimiento fueron satisfechos.  En este punto, debe prestar especial atención a las posibles condiciones de error, ya que se estará interactuando, al menos, con dos elementos externos, como lo son un servidor ftp y un programa invocado en el sistema operativo.  Adicionalmente, preste especial atención a la documentación del enfoque que siguió para implementar las características de encripción solicitadas.

Consideraciones adicionales:
•	El usuario y la contraseña que se utilizan para cada conexión ftp, así como la contraseña para descompresión de los archivos, se encuentran encriptados en la tabla por medio de una librería de encripción.  Se recomienda analizar la viabilidad de utilizar AES-256, CoverUp o Block Encrypter. También se puede aprovechar la facilidad que provee sql server de mantener columnas encriptadas directamente en la base de datos.
•	Todos los parámetros requeridos para lograr la descompresión deben leerse de la tabla de parámetros.
•	La fecha de entrega es el lunes 30 de octubre de 2017 a las 18:00 horas

Contenido de los archivos:
•	Los archivos que se tendrán disponibles en el servidor ftp corresponden a los de la base de datos AdventureWorks 2014, para las tablas Sales.SalesOrderHeader y Sales.SalesOrderDetail, los cuales estarán separados por un delimitador definido por el equipo.  Los que se recomiendan son el caracter de tabulación y el de pipe (|).  El delimitador de líneas es el de Unix, y no el de Windows.  Para generar los archivos, se le recomienda que utilice los datos que ya existen en la base de datos Adventureworks 2014 y que exporte varios registros, de manera controlada, a archivos de texto; posteriormente, en un editor adecuado, le da el formato que necesita, lo comprime en formato .tar.gz, el cual es el estándar de Linux, le asigna una contraseña y ya están listos para transferirse y cargarse.

Evaluación
•	Github:			15%
•	Ftp:			20%
•	Zip:			20%
•	Encripción en BD	20%
•	Tablas de parámetros y bitácora:		  5%
•	Agente SQL:		10%
•	Carga y proceso:	  5%
•	Análisis de resultados:	  5%
