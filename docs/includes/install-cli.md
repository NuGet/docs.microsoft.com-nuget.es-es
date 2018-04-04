#### <a name="windows"></a>Windows
1. Visite [nuget.org/downloads](https://nuget.org/downloads) y seleccione NuGet 3.3 o superior (2.8.6 no es compatible con Mono). Siempre se recomienda la versión más reciente y 4.1.0+ es necesario para publicar paquetes en nuget.org.
2. Cada descarga el `nuget.exe` archivo directamente. Indicar el explorador para guardar el archivo en una carpeta de su elección. El archivo es *no* un instalador; no verá nada si se ejecuta directamente desde el explorador.
3. Agregar la carpeta donde colocó `nuget.exe` a la variable de entorno de ruta de acceso para usar la herramienta CLI desde cualquier lugar.

#### <a name="macoslinux"></a>macOS/Linux
Comportamientos pueden variar ligeramente según distribución del sistema operativo.

1. Instalar [Mono 4.4.2 o una versión posterior](http://www.mono-project.com/docs/getting-started/install/).
2. Ejecute los comandos siguientes en un símbolo del sistema del shell:
    
    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    # Give the file permissions to execute
    sudo chmod 755 /usr/local/bin/nuget.exe
    ```
3. Crear un alias mediante la adición de la secuencia de comandos siguiente en el archivo apropiado para su sistema operativo (normalmente `~/.bash_aliases` o `~/.bash_profile`):
    
    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```
4. Vuelva a cargar el shell.  Para probar la instalación, escriba `nuget` sin parámetros. Debe mostrar la Ayuda de NuGet CLI.