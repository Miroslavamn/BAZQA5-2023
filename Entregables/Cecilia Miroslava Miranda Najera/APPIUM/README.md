# Proyecto - Appium 📲

Proceso de instalación y configuración necesaria para ejecutar los casos de prueba automatizados en la aplicación móvil "Sauce Labs Swag Labs".

## Herramientas 🛠
* Python3 - [descarga](https://www.python.org/downloads/)
* Appium Server - [descarga](https://github.com/appium/appium-desktop/releases/)
* Appium Inspector - [descarga](https://github.com/appium/appium-inspector/releases)
* Android Studio - [descarga](https://developer.android.com/studio)
* IDE Pycharm community - [descarga](https://www.jetbrains.com/es-es/pycharm/download/?section=mac#section=windows)
     * Appium-Python-client
     * Pytest
     * Allure
     * Flake8
  
## Configuración ⚙️
### Appium Server
Una vez instalado dejar los parametros por default (host, port) 

![appium_server.png](img%2Fappium_server.png)
y oprimir el botón **startServer** como se muestra en la siguiente pantalla:

![appium_server_run.png](img%2Fappium_server_run.png)

### Appium Inspector
Una vez instalado: 

1.- Configurar...
```bash
Host: 0.0.0.0, 
Port: 4723 
Remote path: /wd/hub  
Capabilities:
{
 "platformName": 'Android',
 "deviceName": 'emulator-5554',
 "app": '../APP/sauce_app.apk',
 "appPackage": "com.swaglabsmobileapp",
 "appActivity": ".MainActivity"
}
```
**Nota**: `deviceName` depende del modelo de dipositivo a utilizar  

2.- Guardar el capabilitie e iniciar la sesión.

**Importante**: Es necesario que Appium server ya se encuentre iniciado.

![appium_inspector.png](img%2Fappium_inspector.png)

### Android Studio
Una vez instalado crear un dispositivo para emular las pruebas.

![Android_studio.png](img%2FAndroid_studio.png)

### IDE Pycharm Community

Se requiere tener nodeJS para ejecutar los comandos con el prefijo npm. 

#### 1.- Importar proyecto dentro del IDE
* Oprimir el menu File
* De la lista desplegada oprimir el botón Open
* Buscar el proyecto y oprimir la opción abrir

#### 2.- Instalar librerias - [requirements.txt](requirements.txt)

Para instalar las dependencias utilizar el siguiente comando:
  
 ```bash
pip install -r requirements.txt
```

## Ejecución 🤖

Para correr el set de pruebas se debe tener la siguiente configuración: 

![Configuracion_Python.png](img%2FConfiguracion_Python.png)

Dentro del campo **parameters** colocar:
```bash
--tags=smoke,regression
-f
allure_behave.formatter::AllureFormatter
-o
reports/android
-f
pretty
features/
```  

### 1.- Pruebas de regresión 
* Modificar el parametro `--tags=regression`

### 2.- Pruebas de humo
* Modificar el parametro `--tags=smoke`
 
**Nota**: Cada tag del tipo de prueba se debe colocar en los **features** en la parte superior del escenario (Scenario).  

![Etiqueta_feature.png](img%2FEtiqueta_feature.png)

## Reportes Allure  📋

Para generar un reporte desde cero con Allure, es necesario seguir los siguientes pasos:

1.- Instalar **allure** en la terminal de Pycharm 
```bash
    brew install allure #macOS
  ```  
2.- Agregamos la llamada a allure en enviroment.py para generar el reporte al terminar la ejecución de los casos de prueba. 

```bash
def after_scenario(context, scenario):
    subprocess.run("allure serve reports/android", shell=True)
    context.driver.quit()
```
**Ejemplo:**

## Análisis de código estático 🧐
Escaneo de código en busca de errores, lo ejecutamos en steps y screens.

**1.- Instalación**
```
pip install flake8
```
**2- Ejecución**
```
flake8 ./steps
flake8 ./screens
 ```
**3.- Resultado**
![flake8.png](img%2Fflake8.png)

## Autor 👩‍💻
* Cecilia Miroslava Miranda Nájera