1. Cambie a la carpeta que contiene el archivo `.nupkg`.

1. Ejecute el comando siguiente, especificando el nombre del paquete y reemplazando el valor de clave por la clave de API:

    ```cli
    dotnet nuget push AppLogger.1.0.0.nupkg -k qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -s https://api.nuget.org/v3/index.json
    ```

1. dotnet muestra los resultados del proceso de publicación:

    ```output
    info : Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
    info :   PUT https://www.nuget.org/api/v2/package/
    info :   Created https://www.nuget.org/api/v2/package/ 12620ms
    info : Your package was pushed.
    ```

Vea [dotnet nuget push](/dotnet/core/tools/dotnet-nuget-push).