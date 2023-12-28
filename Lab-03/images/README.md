# **LABORATORIO N° 3: WiFi - AWS (aplicación web para visualización de datos atmosféricos**)

## **Descripción General**
<div style="text-align:center" ><img src="images/schema.png"/></div>



## **Paso 01: Creación en Cloud9 de Entorno de Programación para React**
- Vamos a la consola de **AWS**.
>https://console.aws.amazon.com/

<hr></hr>

### **Cloud9: IDE en la nube para escribir, ejecutar y depurar código**
<div style="text-align:center" ><img src="images/cloud9.jpg"/></div>

- Beneficios:
    - Funciona en el navegador.
    - Incluye una terminal de línea de comandos.
    - Permite colaboración con otros programadores en tiempo real (pair programming) con un chat incluido.
    - Incluye SDKs, librerías, plug-ins para desarrollo serverless y permite testear localmente funciones Lambda.
    - Acceso directo a AWS desde la terminal (tiene AWS CLI pre-autenticada).
    - Soporta Node.js, JS, Python, PHP, Ruby, Go, and C++.
    - Puedes utilizar diferentes IDEs para diferentes proyectos.




<hr></hr>

- Vamos al servicio **Cloud9** e inicializamos un **IDE** con una máquina tipo **t3.medium** y con S.O. **Amazon Linux 2**.
- Verificamos la versión de Node.js instalada:
>`node -v`

- Verificamos la versión de NPM instalada:
>`npm -v`

- Inicializamos nuestra aplicación de React (el nombre del proyecto debe ser en minúsculas, restricciones de NPM):
>`npx create-react-app <nombre_proyecto>`

<hr></hr>

### **React: una librería de JS para desarrollar UIs**
- Single Page Application (Client Side Rendering) vs Multi Page Application (Server Side Rendering).
<div style="text-align:center" ><img src="images/spa.png"/></div>

- DOM object
<div style="text-align:center" ><img src="images/dom.png"/></div>

- Virtual DOM
<div style="text-align:center" ><img src="images/spa2.png"/></div>

- Pensando en Componentes de React
<div style="text-align:center" ><img src="images/component.png"/></div>

- Árbol de Interfaz Gráfica
<div style="text-align:center" ><img src="images/tree.png"/></div>


<hr></hr>

- Vamos a la carpeta del proyecto y ejecutamos React.
>`cd <nombre_proyecto>`

>`npm start`

- Esperamos a que se ejecute y vamos a **Preview** > **Preview Running Application**.
- Veremos la aplicación ejecutándose al costado.
<div style="text-align:center" ><img src="images/03-01.png"/></div>

- Eliminamos los archivos innecesarios, abrimos una nueva terminal, nos ubicamos en la carpeta del proyecto **src** y ejecutamos:
>`cd <nombre_proyecto>/src`

>`rm App.css App.test.js logo.svg reportWebVitals.js setupTests.js`

- En el archivo **index.js** pegamos lo siguiente:
>`import React from 'react';`

>`import ReactDOM from 'react-dom/client';`

>`import './index.css';`

>`import App from './App';`

>`const root = ReactDOM.createRoot(document.getElementById('root'));`

>`root.render(   <React.StrictMode>     <App />   </React.StrictMode> );`

- En el archivo **App.js** pegamos lo siguiente:
>`function App() {   return (     <h1>Hola mundo!</h1>   ); } export default App;`

- Actualizamos el **Preview** y veremos lo siguiente:
<div style="text-align:center" ><img src="images/03-02.png"/></div>

<hr></hr>

## **Paso 02: Seteamos AWS Amplify en React**

<hr></hr>

### **Amplify**
- Framework de AWS que permite crear aplicaciones web y mobile que interactúen con los servicios de AWS.
- Es similar a un "**Backend as a Service**" como "**Firebase**", "**Supabase**"
- Ofrece una interfaz visual "**Amplify Studio**" para desplegar los recursos como "**Storage**", "**ML**", "**APIs**", etc.
- También ofrece una interfaz de línea de comandos (CLI) para interactuar con "**Amplify**" y desplegar recursos con unos comandos.
- Tiene librerías Open-Source para crear aplicaciones con "**React.js**", "**Vue.js**", "**Next.js**", "**Android**", "**iOS**", "**Flutter**".
- Tiene el "**Amplify UI Components**" para construir componentes de "**React**" usando "**Figma**".
- Permite hostear tu aplicación utilizando "**CI/CD**".

- Crea backend.
<div style="text-align:center" ><img src="images/amplify1.png"/></div>

- Crea una interfaz de usuario (frontend).
<div style="text-align:center" ><img src="images/amplify2.png"/></div>


- Hostea tu web app.
<div style="text-align:center" ><img src="images/amplify3.png"/></div>

- Servicios de Amplify.
<div style="text-align:center" ><img src="images/amplify4.png"/></div>

<hr></hr>

- En la terminal ejecutamos los siguientes comandos, nos ubicamos en la raíz de nuestro proyecto:
>`cd ..`

>`npm install -g @aws-amplify/cli`

>`npm install aws-amplify`

>`amplify configure`

- En la terminal va a aparecer un mensaje que pide que iniciemos sesión en nuestra cuenta de AWS. Le hacemos click al link y luego regresamos a la terminal y presionamos Enter.
- Especificamos la región **us-east-1**.
- Nos pide que completemos la creación del usuario en la consola de AWS, hacemos click al link que aparece.
- Ingresamos un nombre de usuario y click en "**Next**".
- Hacemos click en "**Attach policies directly**".
- En el buscador buscamos "**AdministratorAccess**" y "**AdministratorAccess-Amplify**" y los seleccionamos, luego click en "**Next**".
- Hacemos click en "**Create user**".
- Nos redirigirá a la ventana de "**IAM**" y a "**Users**", en el buscador colocamos el nombre del usuario que creamos.
- Escribimos un nombre de usuario, le hacemos click. Luego hacemos click en "**Security credentials**" y hacemos click en "**Create access key**, seleccionamos "**Local code**", check y click en "**Next**" y luego en "**Create access key**".
- A continuación en la consola de AWS nos aparecerá el "**Access key**" y el "**Secret access key**", los cuáles tenemos que guardarlos en un lugar seguro, luego de guardarlos click en "**Done**".
- Regresamos a **Cloud9**, damos enter e ingresamos nuestras credenciales, dejamos el **profile name** por default.
- Nos aparecerá el mensaje "**Successfully set up the new user**".
- Con esto hemos configurado el nuevo usuario.
<hr></hr>

- Inicializamos la configuración de **Amplify**.
>`amplify init`

- Nos pide: nombre de proyecto, y otras configuraciones que dejamos por defecto.
- En el método de autenticación seleccionamos el **AWS profile**.
- Seleccionamos el perfil que acabamos de crear **default**.
- Va a empezar a desplegar los recursos en **Amplify**.
- Si regresamos a la consola de AWS, veremos que nuestro proyecto está desplegado.
<div style="text-align:center" ><img src="images/03-03.png"/></div>

- Vamos al archivo **index.js** y agregamos lo siguiente justo después de la importación de los módulos y antes de la declaración de la variable root:
>`import {Amplify} from "aws-amplify";`

>`import awsExports from "./aws-exports";`

>`Amplify.configure (awsExports);`

- Ejecutamos el siguiente comando para ver el estado de **Amplify**:
>`amplify status`
<div style="text-align:center" ><img src="images/03-04.png"/></div>

<hr></hr>

## **Paso 03: Añadimos recursos de Autenticación con Amplify**

<hr></hr>

### **Cognito**
- Ayuda a implementar la administración de acceso e identidad del cliente (CIAM) en su sitio web y sus aplicaciones móviles.
- Maneja autenticación y control de acceso de usuarios.

<div style="text-align:center" ><img src="images/cognito0.png"/></div>
<div style="text-align:center" ><img src="images/cognito1.png"/></div>
<div style="text-align:center" ><img src="images/cognito2.png"/></div>
<div style="text-align:center" ><img src="images/cognito3.png"/></div>

<hr></hr>


- Añadimos servicios de autenticación.
>`amplify add auth`

- Seleccionamos lo siguiente:
    - Default configuration
    - Email
    - No, I am done

- Vemos nuevamente el status:
>`amplify status`

- Si regresamos a la consola de **Amplify**, veremos que se añadió el recurso.
<div style="text-align:center" ><img src="images/03-05.png"/></div>

- Desplegamos el recurso en la nube.
>`amplify push`

- Si regresamos a la consola de "**Amplify**", veremos que se añadió el recurso.
<div style="text-align:center" ><img src="images/03-06.png"/></div>

- Instalamos el siguiente módulo:
>`npm install @aws-amplify/ui-react`

- Pegamos el siguiente código en "**App.js**":
>`import {withAuthenticator} from "@aws-amplify/ui-react";`

>`import '@aws-amplify/ui-react/styles.css';`

>`function App({signOut}) {`

>`return (`

>`<>`

>`<h1>Hola UNAMAD!</h1>`

>`<button onClick={signOut}>Sign out</button>`

>`</>`

>`);`

>`}`

>`export default withAuthenticator(App);`

- Luego para ingresar a nuestra página principal, tenemos que loguearnos.
<div style="text-align:center" ><img src="images/03-07.png"/></div>

- Creamos una nueva cuenta e ingresamos.

<hr></hr>

## **Paso 04: Creación del "Chart" para la visualización de datos**
- Instalamos "**react-chartjs-2**".
>`npm install react-chartjs-2`

- Dentro de "**src**" creamos un nuevo archivo llamado "**LineData.js**".
- Abrimos este archivo y pegamos lo siguiente:
>`import {Chart as ChartJS, CategoryScale, LinearScale, PointElement, LineElement, Title, Tooltip, Legend} from 'chart.js';`

>`import { Line } from 'react-chartjs-2';`

>`ChartJS.register(CategoryScale, LinearScale, PointElement, LineElement, Title, Tooltip, Legend);`

>`-------`

>`export const options = {`

>`responsive: true,`

>`plugins: {legend: {position: 'top',},},`

>`layout: { padding: {top: 20, right: 20, bottom: 20, left: 20,},},`

>`};`

>`-------`


>`const labels = ['0', '1', '2', '3', '4', '5', '6'];`

>`const data_temperatura = [23.5, 24.2, 24.9, 25.2, 26, 25.5];`

>`const data_humedad = [94, 92, 91, 84, 84, 87];`

>`-------`

>`export const data_temperatura_chart = {`

>`  labels,`

>`datasets: [`

>`{`

>`label: 'Temperatura Ambiental',`

>`data: data_temperatura,`

>`borderColor: 'rgb(224, 40, 27)',`

>`backgroundColor: 'rgb(224, 40, 27)',`

>`}`

>` ]`

>`};`

>`-------`

>`export const data_humedad_chart = {`


>`labels,`

>`datasets: [`

>`{`

>`label: 'Humedad Ambiental',`

>`data: data_humedad,`

>`borderColor: 'rgb(27, 106, 224)',`

>`backgroundColor: 'rgb(27, 106, 224)',`

>`}`

>`]`

>`};`

>`-------`

>`export function LineData() {`

>`return (`

>`<>`

>`<Line options={options} data={data_temperatura_chart} />`

>`<Line options={options} data={data_humedad_chart} />`

>`</>`

>`)`

>`}`

- Luego en "**App.js**" pegamos el siguiente código:

>`import {withAuthenticator} from "@aws-amplify/ui-react";`

>`import '@aws-amplify/ui-react/styles.css';`

>`import {LineData} from './LineData';`

>`function App({signOut}) {`

>`return (`

>`<>`

>`<h1>Hola UNAMAD!</h1>`

>`<LineData />`

>`<button onClick={signOut}>Sign out</button>`

>`</>`

>`);`

>`}`

>`export default withAuthenticator(App);`

- Luego veremos que nuestra aplicación se actualizó y ahora contiene dos gráficos.
<div style="text-align:center" ><img src="images/03-08.png"/></div>

<hr></hr>

## **Paso 05: Envío de Temperatura y Humedad con el ESP32 y el sensor DHT11 a AWS IoT Core**

<div style="text-align:center" ><img src="images/cli-cf.png"/></div>

<hr></hr>

### **Paso 05.1: Creación de recursos en AWS con CloudFormation**

<hr></hr>

### **AWS IoT Core**
- Permite conectar dispositivos IoT (sensores, actuadores, microcontroladores integrados o aparatos inteligentes) a la nube de AWS de manera segura.
- Completamente gestionado, no se gestionan servidores.
- Billions (dispositivos).
- Trillions (mensajes).
- Integración directa con muchos servicios (Lambda, S3, Kinesis, DynamoDB, etc.)
- Soporta: MQTT, HTTPS, MQTT sobre WSS, LoRaWAN.
<div style="text-align:center" ><img src="images/iotcore1.png"/></div>
<div style="text-align:center" ><img src="images/iotcore2.png"/></div>
<div style="text-align:center" ><img src="images/iotcore3.png"/></div>
<div style="text-align:center" ><img src="images/iotcore4.png"/></div>
<div style="text-align:center" ><img src="images/iotcore5.png"/></div>
<div style="text-align:center" ><img src="images/iotcore6.png"/></div>
<div style="text-align:center" ><img src="images/iotcore7.png"/></div>
<div style="text-align:center" ><img src="images/iotcore8.png"/></div>

<hr></hr>

### **SNS: Simple Notification Service**
- Servicio de mensajería tipo pub/sub totalmente gestionado, alta disponibilidad, seguro y con durabilidad que permite desacoplar microservicios, sistemas distribuidos y aplicaciones sin servidor.
<div style="text-align:center" ><img src="images/sns.png"/></div>

<hr></hr>

### **CloudFormation: herramienta para desplegar Infraestructura como Código**
- Servicio que nos permite crear infraestructura (bases de datos, clústers de Big Data, Máquinas Virtuales, etc.) como código (IaC).
- Documento en texto plano: JSON y YAML.
- Ventajas:
    - Automatiza el despliegue de recursos.
    - Toma menos tiempo que hacerlo de forma manual.
    - Puedes basarte en otros templates, donde se utilizan buenas prácticas.
    - Puedes compartirlo, y el usuario puede personalizar algunos campos.
    - Puedes integrarte con servicios de terceros (p.e. interconexión con el servidor de red de LoRaWAN).
    - Es gratuito, AWS solo cobra por el uso de recursos
desplegados.
    - Eliminación de todos los recursos en conjunto como un stack.

<div style="text-align:center" ><img src="images/cf1.png"/></div>
<div style="text-align:center" ><img src="images/cf2.png"/></div>
<div style="text-align:center" ><img src="images/cf3.png"/></div>
<div style="text-align:center" ><img src="images/cf4.png"/></div>

- Estructura de "**CloudFormation**":
    - "***AWSTemplateFormatVersion**"
        - Versión del formato de la plantilla por defecto.
    - "***Description**"
        - Descripción básica del propósito de la plantilla.
        - Nombre del proyecto, de qué trata, etc.
    - "***Parameters**"
        - Similar a los argumentos pasados a una función.
        - Permite al usuario ingresar información al momento de crear el stack.
        - Ejemplo: nombre de un bucket S3.
    - "***Mappings**"
        - Permite hacer un mapeo de llave:valor (key:value)
    - "***Conditions**"
        - Crean o no recursos si una condición es V o F.
        - Puede usarse el input del usuario.
    - "**Resources**"
        - Los "recursos" es lo que se crea dentro de los servicios de AWS.
        - Define los recursos de AWS que se desplegarán:
        - Ejemplo: EC2, Lambda, DynamoDB, etc.
        - El nombre de un recurso es el “Logical ID”, es el nombre lógico para CloudFormation.
        - El “Physical ID” será el nombre del recurso en AWS.
    - "***Outputs**"
        - Importante para retornar valores que serán usados por otros stacks.
        - Stacks anidados.

<hr></hr>

### **ESP32**
- MCU (Microcontroller Unit) con dos núcleos y con conexión a WiFi y Bluetooth baratos.
<div style="text-align:center" ><img src="images/esp32-1.png"/></div>
<div style="text-align:center" ><img src="images/esp32-2.png"/></div>
<div style="text-align:center" ><img src="images/esp32-3.png"/></div>
<div style="text-align:center" ><img src="images/esp32-4.png"/></div>
<div style="text-align:center" ><img src="images/esp32-5.png"/></div>

<hr></hr>

- Creamos una nueva carpeta, afuera de la carpeta que se creó con "**React**".
>`cd ~/environment/`

>`mkdir esp32-dht11-aws`

>`cd esp32-dht11-aws`

- Descargamos en esta carpeta los siguientes archivos.
>`curl -O https://iot-lab-bucket.s3.amazonaws.com/esp32_dht11_aws/config-file`

>`curl -O https://iot-lab-bucket.s3.amazonaws.com/esp32_dht11_aws/DHT11_ESP32_AWS.cpp`

>`curl -O https://iot-lab-bucket.s3.amazonaws.com/esp32_dht11_aws/DHT11_ESP32_AWS.yaml`

>`curl -O https://iot-lab-bucket.s3.amazonaws.com/esp32_dht11_aws/DHT11_ESP32.cpp`

>`curl -O https://iot-lab-bucket.s3.amazonaws.com/esp32_dht11_aws/GenerateFile.py`

>`curl -O https://iot-lab-bucket.s3.amazonaws.com/esp32_dht11_aws/M3_script.sh`

>`curl -O https://iot-lab-bucket.s3.amazonaws.com/esp32_dht11_aws/policy-iot.json`

- Abrimos el archivo "**config-file**" y modificamos de manera obligatoria los siguientes parámetros "**CORREO_ELECTRONICO**", "**NOMBRE_SSID**", "**NOMBRE_PASSWORD**", los demás parámetros se pueden dejar tal como están, aunque también pueden modificarse para personalizarlos.
- Ejectamos el archivo "**M3_script.sh**" con el siguiente comando.
>`sh M3_script.sh`

- Se generarán bastantes archivos en nuestra carpeta (entre ellos los certificados de autenticación).
- Revisamos nuestro correo electrónico y aceptamos la suscripción para recibir las alertas.

<hr></hr>

## **Paso 05.2: Creación del Proyecto en PlatformIO**
- Abrimos "**VSCode**".
- Vamos a "**Extensions**", buscamos "**PlatformIo**" y lo instalamos, cuando se instale aparecerá el logo de una hormiga en la barra izquierda y le hacemos click.
- Creamos un nuevo proyecto en "**PlatformIO**", hacemos click en "**+ New Project**".
- Colocamos un nombre al proyecto en "**Name**".
- Seleccionamos la placa "**Espressif ESP32 Dev Module**" en "**Board**".
- En "**Framework**" seleccionamos "**Arduino**".
- Click en "**Finish**".
- En la carpeta "**src**" copiamos los archivos "**DHT11_ESP32_AWS.cpp**" y "**certs.h**", los descargamos directamente de "**Cloud9**".
- En el "**PIO Home**" vamos a "**Libraries**".
- Buscamos las siguientes librerías y las instalamos haciendo click en "**Add to Project**" y seleccionamos el nombre de nuestro proyecto:
    - "**adafruit/DHT sensor library@^1.4.4**"
    - "**adafruit/Adafruit Unified Sensor@^1.1.9**"
    - "**bblanchon/ArduinoJson@^6.21.2**"
    - "**256dpi/MQTT@^2.5.1**"
- Conectamos nuestro "**ESP32**" a la PC con el cable micro USB.
- Hacemos click en el logo de "**PlatformIO**".
- Hacemos click en "**Build**".
- Hacemos click en "**Upload**".
- Cuando el modelo carga, hacemos click en "**Monitor**".

<div style="text-align:center" ><img src="images/03-09.png"/></div>

- Si vamos a "**AWS IoT Core** > "**Test**" > "**MQTT test client**" > "**Subscribe to a topic**".
- Escribimos "**#**" para suscribirnos a todos los mensajes que lleguen a AWS IoT Core.
<div style="text-align:center" ><img src="images/03-10.png"/></div>

- Si se supera el umbral de temperatura, automáticamente nos llegará una notificación a nuestro correo.
<div style="text-align:center" ><img src="images/03-11.png"/></div>

<hr></hr>

## **Paso 06: Integración AWS IoT Core con React**

- Vamos a la consola de **AWS**.
- Vamos al servicio de **AWS IoT Core**.
- Vamos a "**Settings**".
- Copiamos el "**Endpoint**".
- Vamos a nuestra aplicación en "**Cloud9**".
- Vamos al archivo "**index.js**".
- Copiamos el siguiente código:
>`import React from 'react';`

>`import ReactDOM from 'react-dom/client';`

>`import './index.css';`

>`import App from './App'; `

>`import {Amplify} from 'aws-amplify';`

>`import awsExports from './aws-exports';`

>`import {AWSIoTProvider} from '@aws-amplify/pubsub';`

>`Amplify.configure (awsExports);`

>`//Apply plugin with configuration`

>`Amplify.addPluggable(   new AWSIoTProvider({     aws_pubsub_region:'<YOUR-IOT-REGION>',     aws_pubsub_endpoint: wss://'<YOUR-IOT-ENDPOINT>'   }) );`

>`const root = ReactDOM.createRoot(document.getElementById('root'));`

>`root.render(   <React.StrictMode>     <App />   </React.StrictMode> );`

- Colocamos la región de AWS en la que estamos trabajando en "**YOUR-IOT-REGION**".
- Colocamos el Endpoint que copiamos anteriormente en: "**YOUR-IOT-ENDPOINT**".

<hr></hr>

### **Paso 06.1: Creamos políticas IAM para AWS IoT**
- Vamos a "**IoT Core**".
- Vamos a "**Security**".
- Vamos a "**Policies**".
- Vamos a "**Create a policy**".
- Colocar el nombre de la política.
- Policy effect: "**Allow**"
- Policy action: **'*'**
- Policy resource: "**arn:aws:iot:YOUR-IOT-REGION:YOUR-AWS-ACCOUNT-ID:***"
<div style="text-align:center" ><img src="images/03-12.png"/></div>

<hr></hr>

### **Paso 06.2: Adjuntar política a la Identidad de Amazon Cognito**
- Vamos a "**App.js**".
- Importamos la librería "**Auth**".
>`import {Auth} from 'aws-amplify';`

- Añadimos el siguiente código después la línea de "**function App({signOut}) {**".
>`Auth.currentCredentials().then((info) => {const cognitoIdentityId = info.identityId; console.log(cognitoIdentityId);});`

- Abrimos la aplicación de "**React**" en una pestaña aparte, abrimos la consola del navegador y recuperamos el "**cognitoIdentityId**".
<div style="text-align:center" ><img src="images/03-13.png"/></div>

- En la terminal de "**Cloud9**" ejecutamos lo siguiente para adjuntar la política a nuestro usuario:
>`aws iot attach-policy --policy-name '<YOUR_POLICY_NAME>' --target '<YOUR_COGNITO_IDENTITY_ID>'`

<div style="text-align:center" ><img src="images/03-14.png"/></div>

- Vamos a "**AWS IoT**" > "**Security**" > "**Policies**" > "**<YOUR_POLICY_NAME>**" > "**Targets**" y vamos a ver como la "**policy**" fue adjuntada al "**Cognito identity**".
<div style="text-align:center" ><img src="images/03-15.png"/></div>

<hr></hr>

### **Paso 06.3: Leemos la data del tópico IoT desde nuestra app de React**
- Vamos a la carpeta "**src**".
>`cd ~/environment/<nombre_proyecto>/src`

- Eliminamos los archivos "**index.js**", "**App.js**", y "**LineData.js**".
>`rm index.js App.js LineData.js`

- Descargamos los siguientes archivos.
>`curl -O https://iot-lab-bucket.s3.amazonaws.com/amplify/index.js`

>`curl -O https://iot-lab-bucket.s3.amazonaws.com/amplify/App.js`

>`curl -O https://iot-lab-bucket.s3.amazonaws.com/amplify/LineData.js`

- En "**index.js** colocar tu "**aws_pubsub_region**" y "**aws_pubsub_endpoint**".
- En "**App.js**" colocamos el nombre de nuestro "**Tópico IoT**".

<hr></hr>

### **Paso 06.4: Permitir al Rol Autenticado de Amazon Cognito acceder a los servicios de IoT**
- Vamos a **CloudFormation**.
- Localizamos el stack creado por "**Amplify**".
- Seleccionamos "**Resources**", hacemos click en el "**Physical ID**" del "**Auth Role**".
<div style="text-align:center" ><img src="images/03-16.png"/></div>

- Esto nos va a llevar a la consola de "**IAM**".
- Vamos a "**Add permissions**" > "**Attach policies**".
- Añadimos los siguientes permisos: "**AWSIoTConfigAccess**" y "**AWSIoTDataAccess**".
<div style="text-align:center" ><img src="images/03-17.png"/></div>

- Ahora si vamos a la consola, vamos a poder observar la data que está llegando a nuestro frontend en tiempo real.
<div style="text-align:center" ><img src="images/03-18.png"/></div>

- Si observamos nuestra aplicación de React se verá el Chart cambiando en tiempo real.
<div style="text-align:center" ><img src="images/03-19.png"/></div>

<hr></hr>

## **Paso 07: Hosting de la Aplicación**
- Vamos a nuestro "**IDE**" en "**Cloud9**".
- Nos ubicamos en la raíz del proyecto en nuestra terminal y ejecutamos:
>`git log`

- Nos deberá mostrar los commits guardados en el repositorio de "**Git**".
- Para ver el estado de los archivos ejecutamos:
>`git status`

- Esto nos dirá que hay muchos archivos modificados y borrados que no se han incluido en el "**Staging Area**" de "**Git**".
- Agregamos todo a el "**Staging Area**":
>`git add .`

- Luego hacemos el commit de esta versión de nuestro proyecto:
>`git commit -m "1ra versión" -m "Proyecto IoT."`

- Ahora veremos el nuevo commit de "**Git**" así:
>`git log`

- Ahora vamos a "**GitHub**" y creamos un nuevo repositorio en modo privado.
- Seguimos las instrucciones para hacer un "**push**" de un repositorio existente en nuestra línea de comandos.
- Añadimos el "**remote**".
>`git remote add origin <URL_REPO>`

- Cambiamos el nombre de la rama de "**master**" a "**main**".
>`git branch -M main`

- Hacemos el "**push**" a este origin.
>`git push -u origin main`

- Nos va a pedir nuestro correo y nuestra key.
<div style="text-align:center" ><img src="images/git1.png"/></div>
<div style="text-align:center" ><img src="images/git2.png"/></div>
<div style="text-align:center" ><img src="images/git3.png"/></div>
<div style="text-align:center" ><img src="images/git4.png"/></div>
<div style="text-align:center" ><img src="images/git5.png"/></div>

- Vamos a la consola de "**Amplify**".
- Vamos a nuestra aplicación.
- Vamos a "**Hosting environments**".
- Seleccionamos "**GitHub**".
- Click en "**Connect branch**".
- Seleccionamos nuestro repositorio.
- Seleccionamos el "**Branch**".
- En "**environment**" seleccionamos "**dev**", que es el entorno de nuestro backend.
- Checkeamos la opción referida a "**Full-stack CI/CD**".
- Creamos un nuevo "**role**" y aceptar las opciones por defecto.
- En los "**Build and test settings**" añadimos lo siguiente (después de "**npm run build**"):
>`- GENERATE_SOURCEMAP=false npm run build`

- "**Next**" y "**Save and deploy**".
- Luego se verá como se termina de desplegar la aplicación.
<div style="text-align:center" ><img src="images/web0.png"/></div>

- Vamos al link que se genera una vez desplegada la aplicación, y veremos nuestra aplicación en línea y funcionando.
<div style="text-align:center" ><img src="images/web1.png"/></div>
<div style="text-align:center" ><img src="images/web2.png"/></div>