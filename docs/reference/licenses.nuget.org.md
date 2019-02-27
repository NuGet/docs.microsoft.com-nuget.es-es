# <a name="licensesnugetorg"></a>licenses.nuget.org

## <a name="rationale"></a>Razonamiento

Con la introducción de la [licencia expresiones](nuspec.md#license) surgido un requisito para que un servicio confiable que proporcionaría un texto de referencia para los identificadores de licencia individual, los identificadores de excepción o expresiones de licencia.
Un requisito adicional para este servicio es tener un esquema de dirección URL estable, que no es susceptible de vincular la tabla rot, por lo que podemos usar sin riesgos, para proporcionar compatibilidad con versiones anteriores de clientes antiguos.

Licenses.NuGet.org cumple ese rol. NuGet.org lo usa para proporcionar la referencia de texto de la licencia para los paquetes que especifican su licencia usando una expresión de la licencia. `nuget pack` o empaquetado con otros [las herramientas de cliente](https://docs.microsoft.com/en-us/nuget/install-nuget-client-tools) establecer el [ `licenseUrl` ](nuspec.md#licenseurl) elemento para que apunte a licenses.nuget.org para ofrecer compatibilidad con clientes antiguos que no son compatibles con el `license` elemento.

## <a name="protocol"></a>Protocolo

Licenses.NuGet.org está pensado para su visualización por personas en sus exploradores, no las respuestas que se proporcionan.
Se debe usar el protocolo HTTPS y las solicitudes se esperan que se construye de una manera determinada. Solo admite `GET` solicitudes.
Acepta expresiones de licencia o identificadores de excepción de licencia como una entrada de una manera especificada a continuación. Tenga en cuenta que todos los elementos de expresiones de licencia distinguen mayúsculas de minúsculas y, por lo tanto, todas las entradas a licenses.nuget.org también distingue mayúsculas de minúsculas.

### <a name="license-expressions"></a>Expresiones de licencia

#### <a name="request"></a>Request

Las expresiones de licencia (incluso los casos trivial expresión consta de una sola licencia) tienen que ser [con codificación URL](https://tools.ietf.org/html/rfc3986#section-2.1) y puede usar como una ruta de acceso en la solicitud para licenses.nuget.org.

| Expresión de licencia | Dirección URL para usar |
|:---|:---|
MIT                                                | https://licenses.nuget.org/MIT
(MIT)                                              | https://licenses.nuget.org/(MIT)
(LGPL-2.0-solo con Apache FLTK excepción OR-2.0 +) | https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)

El servicio solo admite identificadores de licencia y los identificadores de excepción de licencia que se aceptan en nuget.org. Todas las expresiones que contienen los identificadores de licencia no admitido o identificadores de excepción de licencia o que no se ajusta a la sintaxis de expresión de licencia de licencia se consideran no válidas.

#### <a name="response"></a>Respuesta

Licenses.NuGet.org responde a las solicitudes que contienen expresiones de licencia válida con un código de estado HTTP 200 y una página web que contiene una descripción de la expresión de licencia:
* Si se proporciona la expresión de licencia contiene un identificador de licencia solo que se devuelve una página web que contiene ese texto de referencia de la licencia;
* Si proporciona licencia trata de una expresión compuesta de licencia, se devuelve una página web que contiene la expresión de licencia con vínculos a referencias de excepción de licencias o licencias individuales.

Las solicitudes que contengan un resultado de la expresión de licencia no válida en una respuesta HTTP 404.

### <a name="license-exceptions"></a>Excepciones de licencia

#### <a name="request"></a>Request

Los identificadores de excepción de licencia deben ser con codificación URL y se utiliza como una ruta de acceso en la solicitud para licenses.nuget.org. Solo un identificador de excepción única licencia se puede proporcionar en una única solicitud. Ningún carácter adicional además de identificador de licencia de excepción puede existir en la parte de la ruta de acceso de la dirección URL.

| Identificador de la excepción de licencia | Dirección URL para usar |
|:---|:---|
Excepción de FLTK            | https://licenses.nuget.org/FLTK-exception
openvpn-openssl-exception | https://licenses.nuget.org/openvpn-openssl-exception

#### <a name="response"></a>Respuesta

Licenses.NuGet.org responde a una solicitud con un identificador de excepción conocidos licencia con una respuesta HTTP 200 y una página web que contiene el texto de referencia para la excepción de licencia especificado.

Cualquier solicitud que contiene un identificador de excepción de la licencia no admitido da como resultado una respuesta HTTP 404.