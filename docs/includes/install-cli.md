#### <a name="windows"></a>Windows

1. Visite [nuget.org/downloads](https://nuget.org/downloads) y seleccione NuGet 3.3 o posterior (2.8.6 no es compatible con Mono). Siempre se recomienda la última versión, y 4.1.0+ es la versión necesaria para publicar paquetes en nuget.org.
1. Cada descarga es el archivo `nuget.exe` directamente. Indique al explorador que guarde el archivo en una carpeta de su elección. El archivo *no* es un instalador; no verá nada si lo ejecuta directamente desde el explorador.
1. Agregue la carpeta donde colocó `nuget.exe` a la variable de entorno de RUTA DE ACCESO para usar la herramienta CLI desde cualquier lugar.

#### <a name="macoslinux"></a>macOS y Linux

Los comportamientos pueden variar ligeramente según la distribución del sistema operativo.

1. Instale [Mono 4.4.2 o versiones posteriores](http://www.mono-project.com/docs/getting-started/install/).

1. Ejecute los comandos siguientes en un símbolo del sistema del shell:

    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    ```

1. Cree un alias mediante la adición del script siguiente al archivo apropiado del sistema operativo (normalmente `~/.bash_aliases` o `~/.bash_profile`):

    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```

1. Recargue el shell.  Para probar la instalación, escriba `nuget` sin parámetros. Debe aparecer la Ayuda de la CLI de NuGet.
