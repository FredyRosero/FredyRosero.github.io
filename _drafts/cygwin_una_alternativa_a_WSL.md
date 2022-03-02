## ¿Qué...
### ...es?
Cygwin es:
* una larga colección de herramientas GNU y Open Source que proveen una funcionalidad similar a Linux pero emulada en Windwos.
* un DLL (cygwin1.dll) que provee una funcionalidad substancial de la API POSIX

### ...no es?
Cygwin no es:
* una manera de correr una aplicación nativa de Linux (incluyendo entornos WSL). Se debe recompilar la aplicación con el código fuente para correrla en Windows.
* una manera mágica de hacer que aplicaciones nativas de windows usen funcionalidad de UNIX® como signals, ptys, etc.



## Gestor de paqquetes
Por defecto Cyqwin no utiliza un gstor de paquetes como `apt` o `yum`:
> La razón básica para no usar un administrador de paquetes más completo es que dicho programa necesitaría acceso completo a todas las funciones POSIX de Cygwin. Sin embargo, eso es difícil de proporcionar en un entorno libre de Cygwin, como el que existe en la primera instalación. Además, Windows no permite sobrescribir fácilmente los ejecutables en uso, por lo que instalar una nueva versión de la DLL de Cygwin mientras un administrador de paquetes está usando la DLL es problemático.
[cygwin: Why not use apt, yum, my favourite package manager, etc.?](https://www.cygwin.com/install.html#why-not)
Sin embargo, podemos utilizar [apt-cyg](https://github.com/transcode-open/apt-cyg) de [@transcode-open](https://github.com/transcode-open) el cual es un gestor de paquetes para Cygwin

## Instalación + apt-cyg

1. Instalamos CygWin con las siguientes binarios para `apt-cyg`

    setup-x86_64 -q -P  wget,tar,bzip2,subversion,vim,lynx 

2. Luego descargamos `apt-cyg`

    Opción 1:
    ```bash
    lynx -source rawgit.com/transcode-open/apt-cyg/master/apt-cyg > apt-cyg
    ```
    Opción 2:    
    ```bash
    wget rawgit.com/transcode-open/apt-cyg/master/apt-cyg
    ```
3.  Instalamos `apt-cyg`

    install apt-cyg /bin

3. Ahora si podemos instalar paquetes

    apt-cyg install openssh


# Fuentes:
https://stackoverflow.com/a/19243415/11077105
https://www.fir3net.com/Cygwin/cygwin-package-installation.html