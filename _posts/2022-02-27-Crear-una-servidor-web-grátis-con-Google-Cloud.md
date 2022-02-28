---
title: Crear una servidor web grátis con Google Cloud
author: Fredy Rosero
tags: 'google-cloud, comput-engine, apache, servidor-web'
date: '2022-02-27'
layout: post
category: Google Cloud
---
![banner-google-cloud.png](/assets/banner-google-cloud.png)
Muchas veces queremos desplegar un servidor web con fines pedagógicos o experimentales, y por ende, nos estaríamos dispuestos a pagar un hosting por un sitio web que al cumplir su finalidad se arrume en el olvido. Aquí es donde entra la capa gratuita de Google Cloud para su service Compute Engine que nos permite montar una máquina virtual para configurarla a nuestro antojo.

## Capa gratuita de **Compute Engine** 
Todos los clientes de Google Cloud pueden usar Compute Engine, Cloud Storage, y BigQuery gratis solo si lo usan dentro de los limites especificados:

* Una instania en una de la zonas: 
    * Oregon: us-west1
    * Iowa: us-central1
    * South Carolina: us-east1
* Disco persistente estandar de 30 GB por mes.
* Almacenamitno de 5 GB por mes en Snapshots en:
    * Oregon: us-west1
    * Iowa: us-central1
    * South Carolina: us-east1
    * Taiwan: asia-east1
    * Belgium: europe-west1
* 1 GB de tráfico de salida de Norta América a la demás regiones (excluyendo China y Australia) por mes.

El limite de la capa gratuita para instancias E2-micro se contabiliza sumando de manera global todos los servicios en todas las instancias usadas. La IP externa es gratuita. 
[Mas info.](https://cloud.google.com/free/docs/gcp-free-tier/#compute)

# Google Cloud CLI
GC tiene un cliente CLI que podemos usar desde nuestra consola de Windows o Linux para administrar nuestros pryectos de GC o conectarnos a nuestras MV. Si bien noe s obligatorio ayudará y simplificará muchas tareas que impliquen proyectos en Google Cloud. 

Instala el GC CLI para windows desde PoweShell [[?]](https://cloud.google.com/sdk/docs/install-sdk#windows)
```powershell
(New-Object Net.WebClient).DownloadFile("https://dl.google.com/dl/cloudsdk/channels/rapid/GoogleCloudSDKInstaller.exe", "$env:Temp\GoogleCloudSDKInstaller.exe")
& $env:Temp\GoogleCloudSDKInstaller.exe
```
o para Linux
```bash
curl -O https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-374.0.0-linux-x86_64.tar.gz
tar -xf google-cloud-sdk-374.0.0-linux-x86.tar.gz
./google-cloud-sdk/install.sh
./google-cloud-sdk/bin/gcloud init
```

## Proyecto Google Cloud para la MV
Debemos primero que todo crear un proyecto Google Cloud y luego una instancia de MV:
1. Configura un proyecto Google Cloud (GCP)
    1. Selecciona un proyecto o crea uno.
    2. Habilita la api **Compute Engine API**.

2. Crea la instancia de la MV con *Debian*
    1. En la página **Compute Engine**, haz clic en **VM instances**.
    2. Luego haz clic en **Create instance**.
    2. En el campo nombre yo ingresaré `'your_name_server'`.
    4. Y definiré la zona en `'your_VM_zone'`
    4. En el tipo de máquina seleccionamos **e2-micro**.

## Conectarse a la maquina

**Opción 1**: Cloud Shell desde web o GC CLI
1. Click the Activate Cloud Shell button.
2. Connect to the server VM by using SSH:        
    ```bash
    VM_NAME='your_name_server'
    ZONE='your_VM_zone'
    PROJECT=$(gcloud config list --format 'value(core.project)' 2>/dev/null)
    gcloud compute --project $PROJECT ssh --zone $ZONE $VM_NAME
    ```

**Opción 2**: Conectate a la máquina usando cliente SSH
1. Habilita `OS Login` [[?]](https://cloud.google.com/compute/docs/instances/managing-instance-access)
    ```bash        
    gcloud compute instances add-metadata $VM_NAME --metadata enable-oslogin=TRUE --zone=$ZONE
    ```

2. Configura los roles `OS Login` para la cuenta de servicio [[?]](https://cloud.google.com/sdk/gcloud/reference/compute/instances/add-iam-policy-binding)
    ```bash
    PRINCIPAL='serviceAccount:'['your_service_account']
    ROLE='roles/compute.osLogin'
    gcloud compute instances add-iam-policy-binding $VM_NAME --zone=$ZONE --member=$PRINCIPAL --role=$ROLE
    ```

3. Crea un par de llaves SSH [[?]](https://cloud.google.com/compute/docs/connect/create-ssh-keys#create_an_ssh_key_pair) y copia la llave
    ```bash
    KEY_FILE_PATH=~/.ssh/uqbar_key
    USER='faroseroc_unal_edu_co'
    ssh-keygen -t rsa -f $KEY_FILE_PATH -C $USER -b 2048
    cat $KEY_FILE_PATH
    ```
    
4. En tu máquina local (cliente SSH) crea la llave privada y dale permisos `600 (-rw-------)`
    ```bash
    KEY_FILE_LOCAL_PATH=~/uqbar/google_cloud/uqbar_key
    nano $KEY_FILE_LOCAL_PATH
    #pega la llave del paso de arriba
    ls -al $KEY_FILE_LOCAL_PATH
    chmod 600 $KEY_FILE_LOCAL_PATH
    ls -al $KEY_FILE_LOCAL_PATH
    ```

4. De vuelte en el GC Shell, agregar las llaves SSH a la MV [[?]](https://cloud.google.com/sdk/gcloud/reference/compute/os-login/ssh-keys/add)        
    ```bash
    gcloud compute os-login ssh-keys add --key-file=$KEY_FILE_PATH.pub
    ```

5. Finalmente en tu máquina cliente SSH, concetate por SSH [[?]](https://cloud.google.com/compute/docs/instances/connecting-advanced#linux,-macos,-and-windows-10-or-later)

    **Opción 1:** Cliente OpenSSH en Linux, WSL o CyGWin
    ```bash
    KEY_FILE_LOCAL_PATH=~/uqbar/google_cloud/uqbar_key
    USERNAME=faroseroc_unal_edu_co
    EXTERNAL_IP=35.224.246.3
    ssh -i $KEY_FILE_LOCAL_PATH $USERNAME@$EXTERNAL_IP
    ```
    **Opción 2:** PuTTY
    1. Primero convertimos la llave privada en formato .PPK: En `PuTTYgen` cargamos la llave privada, seleccionamos RSA y 2048 bits y luego guardamos la llave pública como archivo `.ppk`.
    3. En `PuTTY`, en el panel de la izquierda vamos a `Conexión > SSH > Auth`  y cargamos el archivo `.ppk`.
    4. En el panel de la izquierda ahora volvemos a `Session` y en hostname ingresamos `$USERNAME@$EXTERNAL_IP`.
    5. Finalmente, hacemos clic en `Open` para abrir la conexión SSH y aceptamos la nueva firma en nuestro equipo.

## Servidor web
1. Instala el servidor web Apache
    ```bash
    sudo apt update
    sudo apt install apache2
    systemctl status apache2
    sudo systemctl start apache2
    systemctl status apache2 
    netstat -tulpn | grep :80
    ```
    Notaremos un servicio TCP corriendo en el puerto 80: `netstat -tulpn | grep :80`

2. Habilitamos el modulo Rewrite:
    ```bash
    sudo a2enmod rewrite
    sudo systemctl restart apache2
    systemctl status apache2 
    ```
3. Raíz del sitio web: Notaremos que en `grep IncludeOptional /etc/apache2/apache2.conf` se incluyen `sites-enabled/*.conf`. El comando `ls /etc/apache2/sites-enabled/*.conf` nos arroja `/etc/apache2/sites-enabled/000-default.conf` el cual contiene la configuración del sitio web por defecto. El atributo `DocumentRoot` obtenido con `grep DocumentRoot /etc/apache2/sites-enabled/000-default.conf` es `/var/www/html` el cual contiene el archivo `index.html` que se entrega al hacer `curl localhost:80`. Podemos comprobar que son los mismos archivos con:  
    ```bash
    curl -s localhost:80 | md5sum
    cat /var/www/html/index.html | md5sum
    ```

## Ruta de archivos personalizada
1. Vamos a cambiar la raíz del directorio web por uno nuestro al cual le agregaremos una página de inicio
    ```bash
    mkdir /home/user/www
    echo "hola mundo!" > /home/user/www/index.html
    sudo vim /etc/apache2/sites-enabled/000-default.conf
    # DocumentRoot /home/user/www/
    sudo apachectl configtest
    # Sintax OK
    sudo systemctl restart apache2
    ```

2. Al solicitar el sitio con `curl localhost` y revisar el log con `sudo tail -100 /var/log/apache2/error.log` notaremos el mensaje  `client denied by server configuration`:
    ```html
    <!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
    <html><head>
    <title>403 Forbidden</title>
    </head><body>
    <h1>Forbidden</h1>
    <p>You don't have permission to access this resource.</p>
    <hr>
    <address>Apache/2.4.38 (Debian) Server at localhost Port 80</address>
    </body></html>
    ```
    Tenemos que dar permisos en `/etc/apache2/sites-enabled/000-default.conf` dentro del nodo `<VirtualHost *:80>` con 
    ```xml
        ...
        <Directory /home/faroseroc_unal_edu_co/www>
            Options Indexes FollowSymLinks
            AllowOverride None
            Require all granted
        </Directory>
        ...
    ```
3. Para tener finalmente nuestro sitio web operante y visible al solicitarlo con `curl localhost` o visitar la ip pública en nuestro navegador
    ```bash
    Hola mundo!
    ```

## Material
* Google Cloud Skill https://www.cloudskillsboost.google/focuses/3563
* Recursos: https://www.youtube.com/watch?v=ew-r46FmzSM
/etc/apache2/sites-enabled/000-default.conf