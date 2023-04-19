## Realizando ETL con Python y Pentaho
- ETL (Extraccion, Transformacion y Cargado de datos)
- Se utiliza la estructura estrella
- Extraccion(sql,json,.csv,NoSQL -> Carga (datawarehouse) -> Transformacion -> Analizar ( graficos power bi)
- ===Consideraciones de ETL===
  - 1.-Debo asegurar la calidad de los datos
  - 2.-Tener claro las fuentes y los objetivos
  - 3.-Definir si mi ETL sera en Batch (cada 20 min) o Streaming (en menos de 1 seg)
  - 4.-Definir si mi ETL sera incremental o total
  - 5.-La documentación

### Batch o Streaming
20 minutes or 1 seconds

### Herramientas:
- Extraer: Realizamos la subida de archivos ya sea en .sql .csv .doc en un postgresql y utilizamos el dataspell
SQL, Json y CSV
Conectaremos a DB OLTP:
DataSpell
- Configuraremos docker:
https://www.docker.com/products/docker-desktop/

- Transformaremos: se trabajo con "pandas"
google colab - anaconda - .pynb - munpy - pandas
Es decir cambiamos los datos nulos a que esten completos , cambiamos filas en columnas
o si tiene 6 rows y el otro 3 rows lo pasmos a 6 rows
Pentaho
- Cargado: Es basicamente unir las base de datos en uno solo y ahora teniendo todo eso ya podemos
utilizar power bi
Python

- visualizacion de datos:
Herramienta: Power bi


## Segmentacion de herramienta para ETL:
ENTERPRISE, CLOUD, OPEN SOURCE Y CUSTOM
Objetivo del ETL:
Dejar datos confiables en un repositorio para que sean usados en proyectos de analítica,
 data science y de machine learning.
 1.5 Instalación local de PostgreSQL (opcional)
De no usar Docker podrías ver la clase del curso de PostgreSQL en donde aprendes a instalarlo localmente, pero te sugiero intentarlo con Docker ya que puede agilizar tu flujo de trabajo. 😉

## 2. Validar container creado
Una vez que hayas creado el container de Docker usa el comando docker ps en tu terminal. Podrás ver todos los contenedores que se encuentran en ejecución actualmente y una descripción.

Deberás ver la IMAGE postgres.
- ![imagen0](/img/1.webp)
## 3. Configurar DataSpell
Para conectarte a la base de datos usarás un software de administración de bases de datos. Existen varios que puedes utilizar. Para el seguimiento del curso te sugiero utilizar DataSpell o, en su defecto, DBeaver.

DataSpell es un IDE completo para ciencia de de datos donde, además de conectarte y hacer consultas a bases de datos, podrás ejecutar Jupyter Notebooks. ¡Todo en el mismo lugar! 💪🏽

- ![imagen0](/img/2.webp)
💡 Una de sus desventajas es que es de pago, pero tiene un período de prueba de 30 días para que lo pruebes con este curso. Además existen ciertas opciones para obtener licencias para estudiantes de bachillerato y universidad.

⚠️🦫 En caso de que decidas usar DBeaver en lugar de DataSpell, utiliza tu entorno local de Jupyter Notebooks con Anaconda para la ejecución del código Python de las siguientes clases. 🐍

Instalación de DataSpell
Para instalar DataSpell ve a su sitio web aquí y descarga la versión para tu sistema operativo.📥

Instálalo siguiendo las instrucciones que te aparezcan en el instalador.

⚠️ Cuando te solicite actualizar PATH Variable acepta marcando la opción que te indique. Esto es para evitar errores de ambientes en el futuro. En Windows se ve así:

- ![imagen0](/img/3.webp)
Al finalizar te pedirá reiniciar el computador:

- ![imagen0](/img/4.webp)
Abre DataSpell ya que se haya instalado. Al hacer esto por primera vez te pedirá iniciar sesión. Elige la versión free trial registrando tu cuenta para ello.

Una vez que tengas tu cuenta configurada te pedirá elegir un intérprete de Python 🐍.

Previamente deberás tener instalado Anaconda en tu sistema operativo. Te recomiendo que crees un ambiente de Anaconda (Conda environment) único para el proyecto del curso. Llama al ambiente fundamentos-etl.

Elige el ambiente de Anaconda que usarás para el proyecto y presiona el botón Launch DataSpell.

- ![imagen0](/img/5.webp)
Elegir un intérprete de Anaconda servirá para ejecutar Jupyter Notebooks en DataSpell.

Crea un nuevo Workspace en DataSpell. Presiona el botón File en la barra superior y luego elige la opción New Workspace Directory.
new_workspace_directory.png
Llama fundamentos-etl al workspace y presiona el botón azul Create.

- ![imagen0](/img/6.webp)
Elegir ambiente de WSL2 (opcional si usas WSL)
Si quieres usar DataSpell con tu entorno en Windows con WSL 2, deberás conectar DataSpell al ambiente de Anaconda que tenga tu WSL.🐍

Crea un ambiente de Anaconda en tu WSL dedicado al proyecto de tu curso si todavía no lo has hecho. Llámalo fundamentos-etl
- ![imagen0](/img/7.webp)
Después ve a DataSpell en su parte inferior donde aparece el intérprete. Presiona la dirección que aparece y elige la opción Interpreter Settings.
elegir_interprete_dataspell.png
Escoge el workspace fundamentos-etl creado anteriormente en DataSpell.
⚠️OJO: el workspace y el Anaconda Environment no son lo mismo. El Anaconda Environment lo vamos a cargar dentro del Workspace de DataSpell.

Después presiona el botón Add Interpreter e inmediatamente selecciona la opción On WSL.

- ![imagen0](/img/8.webp)
Elige la distribución de Linux a usar y da clic en el botón Next cuando aparezca el mensaje "Instrospection completed succesfully!
- ![imagen0](/img/9.webp)
Elige el intérprete a usar. Este puede ser un Virtualvenv Environment, el System Interpreter o un Conda Environment. Elige la opción de Conda Environment.
- ![imagen0](/img/10.webp)
Mara la casilla Use existing environment. Elige el Conda Environment de WSL que usarás para tu proyecto. Anteriormente debiste crearlo desde tu terminal en WSL y llamarlo fundamentos-etl.

Finalmente, presiona el botón azul Create.

conda-fundamentos-etl-environment.png
Para terminar el proceso presiona el botón azul OK en la parte inferior.
- ![imagen0](/img/11.webp)
Listo, ya deberá aparecer tu entorno de Anaconda en WSL cargado en la parte inferior de DataSpell.
ambiente-cargado.png
⚠️Si te aparece un error que indique que el ambiente no puede ser usado como el intérprete del workspace es porque estás intentando cargar el ambiente en el workspace general y no en un workspace de DataSpell que creaste.

Aquí encuentras la guía oficial de cómo conectar tu DataSpell al intérprete de Python o Anaconda en WSL, por si necesitas aprender a configurarlo a detalle.

Recuerda que otra alternativa en Windows es instalar Anaconda para Windows y conectar DataSpell directamente a esta versión.

## 4. Conexión a la base de datos PostgreSQL
Sigue estos pasos para conectarte a la base de datos postgres desde DataSpell.

Abre DataSpell en tu computador.
- ![imagen0](/img/12.webp)
Ve a la pestaña de Database y en ella da clic en el botón de signo de +.
- ![imagen0](/img/13.webp)
Selecciona la opción de Data Source y dentro del menú desplegable elige la opción de PostgreSQL.
- ![imagen0](/img/14.webp)
Introduce los datos siguientes en la conexión:
Name: local_postgres
Host: localhost
Port: 5432
User: postgres
Database: postgres
Url (opcional): jdbc:postgresql://localhost:5432/postgres
Password: mysecretpass
Da clic en el botón de Test Connection para probar la conexión. Puede que te solicite actualizar unos drivers, acéptalos. Una vez que indique que la conexión es exitosa, da clic en el botón OK.
- ![imagen0](/img/15.webp)
Listo, ya tienes tu base de datos conectada en DataSpell.
- ![imagen0](/img/16.webp)
4. Cargar datos en la base de datos Postgres
Dentro de DataSpell, ya con la conexión a la base de datos previamente creada, ejecutarás el script postgres_public_trades.sql.

Descárgalo aquí de Google Drive. 📥

⚠️Este archivo pesa cerca de 500 MB, por lo que puede demorar su descarga. Contiene la creación de una tabla llamada trades y los insert de registros de la tabla.

⚠️Es posible que al intentar correr este script en DBeaver no sea posible por falta de memoria. Te sugerimos cortarlo en varias partes y cargar cada script independientemente.

- ![imagen0](/img/17.webp)
Una vez descargado el archivo postgres_public_trades.sql sigue estos pasos para cargar los datos con DataSpell:

Da clic derecho sobre la base de datos de PostgreSQL.
- ![imagen0](/img/18.webp)
Posteriormente da clic en SQL Script y luego en Run SQL Scripts.
- ![imagen0](/img/19.webp)
Ubica el script descargado dentro de tu computador y da clic en OK.
- ![imagen0](/img/20.webp)
⚠️La creación de la tabla y la carga de datos puede demorar cerca de 15-20 minutos en DataSpell.

- ![imagen0](/img/21.webp)
## 5. Prueba la tabla trades
Una vez terminada la ejecución del script, consulta la tabla Trades ya cargada. Abre el editor de queries desde tu base de datos en DataSpell e ingresa la siguiente consulta:

    ```
    SELECT * FROM trades;

    ```
- ![imagen0](/img/22.webp)
¡Listo! Ya tienes lo esencial para comenzar a extraer datos de una base de datos OLTP y correr tus notebooks de Python.