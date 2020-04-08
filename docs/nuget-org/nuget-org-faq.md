---
title: Preguntas más frecuentes de NuGet.org
description: Preguntas y respuestas habituales para trabajar con la galería de NuGet.
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 915f6e4cfc0b21d2b10006c62e8230720d07ce74
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428538"
---
# <a name="nugetorg-frequently-asked-questions"></a>Preguntas más frecuentes de NuGet.org

## <a name="license-terms"></a>Términos de licencia

**¿Cuáles son los términos de licencia predeterminados si un paquete no proporciona información específica de licencia?**

Cada paquete se rige por los términos que se incluyen con el paquete. Debe revisar los términos aplicables antes de obtener acceso a los paquetes, descargarlos o adquirirlos. En nuget.org, use el vínculo **Información de licencia** de la página del paquete.

Si un paquete no especifica los términos de licencia, póngase en contacto con su propietario directamente mediante el vínculo de **contacto con el propietario** que encontrará en la página del paquete en nuget.org. Microsoft no le ofrece licencia para propiedad intelectual de proveedores de paquetes de terceros ni es responsable de la información proporcionada por terceros.

## <a name="managing-packages-on-nugetorg"></a>Administración de paquetes en NuGet.org

**¿Puedo editar metadatos de paquete después de cargarlos?**

NuGet recomienda que todos los paquetes estén firmados. Un principio de diseño de la firma de paquetes es que el contenido del paquete firmado debe ser inmutable, lo que incluye el archivo nuspec. Al modificar los metadatos del paquete se producen cambios en el archivo nuspec, lo que invalida las firmas existentes. Se recomienda modificar los flujos de trabajo existentes para que no se requiera la modificación de los metadatos del paquete una vez creado el paquete.

Tenga en cuenta que las dependencias indicadas para el paquete se generan automáticamente a partir del propio paquete y no se pueden modificar.

Además, cargar paquetes en [int.nugettest.org](https://int.nugettest.org) es una excelente manera de probar y validar el paquete sin hacer que esté disponible en la galería pública. Punto de conexión de API: https://apiint.nugettest.org/v3/index.json

**¿Puedo eliminar un paquete publicado en NuGet.org?**

En general, no se admite la eliminación de un paquete publicado en NuGet.org. Obtenga más información sobre nuestra [directiva de eliminación de paquetes](policies/deleting-packages.md).

**¿Es posible reservar nombres para los paquetes que se van a publicar en el futuro?**

Sí. Puede reservar identificadores para paquetes en [nuget.org](https://www.nuget.org/); para ello, solicite un prefijo de id. de paquete para su cuenta. Para pedir un prefijo de identificador de paquete, siga las instrucciones de la [documentación](id-prefix-reservation.md).

**¿Cómo puedo reclamar la propiedad de los paquetes?**

Consulte [Administración de los propietarios de paquetes en nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).

**¿Qué puedo hacer con el propietario de un paquete que infringe mi licencia de software?**

Se recomienda que la comunidad de NuGet trabaje de forma conjunta para resolver los conflictos que puedan surgir entre los propietarios de paquetes y los propietarios de otro software. Se ha diseñado un [proceso de resolución de conflictos](policies/dispute-resolution.md) que se debe seguir antes de solicitar la actuación de los administradores de nuget.org.

**¿Se recomienda cargar los paquetes de prueba en nuget.org?**

Para fines de prueba, se puede usar [int.nugettest.org](https://int.nugettest.org), o bien servidores públicos alternativos de NuGet como [myget.org](https://myget.org) o [Azure DevOps](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).

Tenga en cuenta que es posible que los paquetes que se cargan en int.nugettest.org no se conserven.

**¿Cuál es el tamaño máximo de los paquetes que puedo cargar en nuget.org?**

nuget.org permite paquetes de hasta 250 MB, pero se recomienda mantener los paquetes por debajo de 1 MB si es posible y usar dependencias para vincularlos. Como regla general, los paquetes solo contienen un ensamblado para evitar conflictos.

NuGet usa HTTP para descargar los paquetes, por lo que la probabilidad de que se produzca un error en la instalación es mayor en los paquetes más grandes que en los de menor tamaño.

Es posible compartir dependencias entre varios paquetes, lo que reduce el tamaño total de la descarga para los consumidores de los paquetes NuGet.

Las dependencias son principalmente estáticas y nunca cambian. Cuando se corrige un error en el código, es posible que no sea necesario actualizar las dependencias. Si agrupa las dependencias, terminará creando paquetes cada vez más grandes. Al dividir los paquetes NuGet en dependencias relacionadas, las actualizaciones son mucho más específicas para los consumidores del paquete.

## <a name="nugetorg-not-accessible"></a>nuget.org no está disponible

**¿Por qué no puedo descargar paquetes de nuget.org ni tampoco cargarlos?**

En primer lugar, asegúrese de que está usando la versión más reciente de NuGet. Si siguen produciéndose errores en esa versión, [póngase en contacto con el soporte técnico](https://www.nuget.org/policies/Contact) y proporcione información adicional para la solución de problemas de conexión:

- La versión de NuGet que está usando
- Los orígenes de paquete que está usando
- Un registro de restauración con nivel de detalle detallado
- MTR o seguimientos de Fiddler (ver a continuación)
- El área geográfica
- Si el equipo está detrás de un proxy o firewall
- Si el equipo está ubicado en el centro de datos de un proveedor de servicios en la nube (Azure y AWS, entre otros) En caso afirmativo, proporcione el nombre del proveedor y la región.

*Para capturar MTR:*

- Descargue [WinMTR](https://sourceforge.net/projects/winmtr/files/WinMTR-v092.zip/download).
- Escriba `api.nuget.org` como nombre de host y haga clic en **Start** (Iniciar).
- Espere hasta que el valor de la columna **Sent** (Enviados) sea >= 100.

    ![Captura de MTR](media/mtr.png)

- Copie el texto en el Portapapeles.

*Para capturar Fiddler:*

- Instale la versión más reciente de [Fiddler](https://www.telerik.com/download/fiddler).
- Inicie Fiddler y deshabilite la captura de tráfico mediante el menú **File > Capture Traffic** (Archivo > Capturar tráfico).
- Quite todas las sesiones (seleccione todos los elementos en la lista y presione la tecla **Suprimir**).
- Configure Fiddler para capturar el tráfico HTTPS activando **Decrypt HTTPS traffic** (Descifrar tráfico HTTPS) en la pestaña **HTTPS** del menú **Tools > Fiddler Options...** (Herramientas > Opciones de Fiddler).
- Cierre Visual Studio.
- Habilite el menú **File > Capture Traffic** (Archivo > Capturar tráfico).
- Inicie Visual Studio o nuget.exe, y ejecute las acciones que no están funcionando. El tráfico generado por estas acciones debería aparecer en Fiddler.
- Una vez que se ejecuten las acciones, use **File > Save > All Sessions** (Archivo > Guardar > Todas las sesiones) para almacenar las sesiones capturadas.

Nota: Es posible que sea necesario establecer la variable de entorno `HTTP_PROXY` en `http://127.0.0.1:8888` para enrutar el tráfico de NuGet a través de Fiddler.

Si eso no funciona, pruebe las [sugerencias mencionadas en esta publicación de StackOverflow](https://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).

## <a name="nugetorg-account-management"></a>Administración de cuentas de nuget.org

### <a name="how-to-recover-nugetorg-password-login"></a>¿Cómo se recupera la contraseña de inicio de sesión de nuget.org?

Tenga en cuenta que el [inicio de sesión con contraseña en nuget.org se ha interrumpido](https://blog.nuget.org/20180515/NuGet.org-will-only-support-MSA-AAD-starting-June.html) y la única manera de hacerlo es mediante una cuenta Microsoft persona (MSA) o una cuenta de Azure Active Directory (AAD). Sin embargo, en el caso de que no pueda acceder a las cuentas de AAD/MSA asociadas, es posible que tenga que usar el inicio de sesión con contraseña para recuperar la cuenta de nuget.org. En ese caso, siga estos pasos.
- **Requisito:** Necesita tener acceso al correo electrónico que esté asociado con la cuenta para la que necesita recuperar la contraseña.
- Vaya a la [página Forgot password](https://www.nuget.org/account/ForgotPassword) (He olvidado mi contraseña).
- Escriba la dirección de **correo electrónico** asociada a la cuenta de nuget.org que quiera recuperar.
- Haga clic en el botón **Send** (Enviar).
- Recibirá un mensaje de correo en la cuenta de la dirección de correo electrónico especificada con un vínculo para restablecer la contraseña. Haga clic en ese vínculo y establezca la contraseña nueva. Si no encuentra el correo electrónico, busque en la carpeta "Correo no deseado".
- Después, ya puede iniciar sesión con el nombre de usuario y la contraseña en NuGet.
- Para iniciar sesión con el nombre de usuario y la contraseña, haga clic en el vínculo para **iniciar sesión con la cuenta de nuget.org** que encontrará en la [página de inicio de sesión de nuget.org](https://www.nuget.org/users/account/LogOn).

### <a name="which-microsoft-account-is-linked-to-my-nugetorg-account"></a>¿Qué cuenta Microsoft está vinculada con la cuenta de nuget.org?

Si ha olvidado qué cuenta Microsoft está asociada a la cuenta de nuget.org, siga los pasos siguientes para obtener asistencia.
1. Vaya a la [página de inicio de sesión de nuget.org](https://www.nuget.org/users/account/LogOn) y haga clic en el vínculo pertinente para **obtener ayuda para iniciar sesión**.
1. Se mostrará el cuadro de diálogo emergente para obtener ayuda. Siga los pasos descritos en este cuadro de diálogo para consultar las cuentas Microsoft asociadas a la cuenta de nuget.org.

### <a name="how-to-change-the-microsoft-account-i-use-for-nugetorg-login"></a>¿Cómo puedo cambiar la cuenta Microsoft que uso para iniciar sesión en nuget.org?
Si quiere cambiar la cuenta Microsoft para el usuario de nuget.org, siga estos pasos. Supongamos que la cuenta Microsoft con el correo electrónico `account1@outlook.com` está asociada a la cuenta de nuget.org con el nombre de usuario `MyNuGetAccount`. Quiere cambiar el inicio de sesión a otra cuenta de Microsoft con el correo electrónico `account2@outlook.com`.
1. Inicie sesión con la **cuenta de Microsoft asociada actualmente**, es decir, `account1@outlook.com` en la [página de inicio de sesión](https://www.nuget.org/users/account/LogOn) después de hacer clic en **Sign in with Microsoft** (Inicio de sesión con Microsoft).
1. Una vez iniciada la sesión, vaya a la página de [configuración de la cuenta](https://www.nuget.org/account).
1. Expanda la sección **Login Account** (Cuenta de inicio de sesión). Haga clic en el botón **Change Account** (Cambiar cuenta).
1. Se le redirigirá a la página de inicio de sesión de Microsoft. Inicie sesión con la cuenta a la quiera cambiar la asociación, es decir, `account2@outlook.com`. **Nota**: Es posible que tenga que hacer clic en **Sign out (Cerrar sesión) e iniciar sesión con otra cuenta** durante el flujo de inicio de sesión para poder iniciar sesión con otra cuenta de Microsoft.
1. Si se le muestra un error similar al siguiente, vea [La cuenta de Microsoft está vinculada con otra cuenta de nuget.org](#microsoft-account-is-linked-with-another-nugetorg-account) para obtener más detalles.
    >_Failed to update the Microsoft account with "account2<account2@outlook.com>" (No se pudo actualizar la cuenta de Microsoft con "cuenta2"). This could happen if it is already linked to another NuGet account. (Esto podría suceder si ya está vinculada a otra cuenta de NuGet) Contact support for more information._ (Póngase en contacto con el servicio de soporte técnico para más información)

1. Una vez que haya iniciado sesión correctamente con la segunda cuenta, se le redirigirá a la página de configuración de la cuenta de nuget.org; debería ver la nueva cuenta Microsoft asociada como la cuenta de inicio de sesión. A partir de ahora, tendrá que usar esta cuenta para iniciar sesión en nuget.org.

### <a name="microsoft-account-is-linked-with-another-nugetorg-account"></a>La cuenta Microsoft está vinculada a otra cuenta de nuget.org.

Si ha intentado cambiar el inicio de sesión de Microsoft y vio el error siguiente:
> _Failed to update the Microsoft account with "account2<account2@outlook.com>" (No se pudo actualizar la cuenta de Microsoft con "cuenta2"). This could happen if it is already linked to another NuGet account. (Esto podría suceder si ya está vinculada a otra cuenta de NuGet) Contact support for more information._ (Póngase en contacto con el servicio de soporte técnico para más información)

Supongamos que ha intentado cambiar la cuenta Microsoft para iniciar sesión `account1@outlook.com` del usuario de nuget.org con el nombre de usuario `MyNuGetAccount1` por otra cuenta Microsoft con el correo electrónico `account2@outlook.com`. Y recibe el error anterior.

**¿Qué significa el error anterior?**

Esto significa que hay otra cuenta de nuget.org asociada a la cuenta Microsoft por la que está intentando cambiarla. Es decir, en el ejemplo anterior, la cuenta Microsoft con el correo electrónico `<account2@outlook.com>` está asociada a otra cuenta de nuget.org, por ejemplo, con el nombre de usuario `MyNuGetAccount2`.

No se puede cambiar el inicio de sesión asociado a una cuenta Microsoft que esté vinculada a otra cuenta de nuget.org.

**He olvidado que tenía otra cuenta de nuget.org, ¿cómo averiguo de qué cuenta de nuget.org se trata?**

Inicie sesión con la segunda cuenta de Microsoft en la [página de inicio de sesión](https://www.nuget.org/users/account/LogOn?returnUrl=%2F# "página de inicio de sesión"). Esto iniciará la sesión en la cuenta de nuget.org que esté asociada actualmente a la segunda cuenta Microsoft. Después, podrá ver los paquetes cargados y realizar la administración en esta cuenta.

**No me interesa esta segunda cuenta de nuget.org; quiero cambiar el inicio de sesión de la primera cuenta de nuget.org por la segunda cuenta Microsoft. ¿Qué hago?**

Si no quiere preocuparse de la segunda cuenta de nuget.org y le sigue interesando volver a usar la cuenta Microsoft asociada al correo electrónico `account2@outlook.com`, 

puede liberar la asociación entre la cuenta Microsoft y la de nuget.org; para ello elimine la de nuget.org.
1. Siga los pasos para [eliminar el usuario](#how-to-delete-my-nugetorg-account) de la segunda cuenta de nuget.org `MyNuGetAccount2`. 
1. Una vez que haya eliminado esta cuenta, puede volver a intentar los pasos para [cambiar el inicio de sesión con la cuenta de Microsoft](#how-to-change-the-microsoft-account-i-use-for-nugetorg-login).

**Un momento, también me interesa esta segunda cuenta. No me interesa perderla, pero quiero cambiar los inicios de sesión con la cuenta asociada a la primera cuenta.**

Tendrá que crear o usar una tercera cuenta de Microsoft, por ejemplo, con el correo electrónico `account3@outlook.com`. 
1. En primer lugar, debe iniciar sesión con la segunda cuenta Microsoft, `account2@outlook.com`, en nuget.org. Siga los pasos anteriores para cambiar los inicios de sesión relacionados y asociar la tercera cuenta Microsoft a esta de nuget.org.
1. Después, la segunda cuenta Microsoft con el correo electrónico `account2@outlook.com` ya se podrá asociar a la primera cuenta de nuget.org, `MyNuGetAccount1`. Siga los mismos pasos anteriores para cambiar los inicios de sesión de Microsoft a la segunda cuenta de Microsoft.

### <a name="signing-in-with-microsoft-account-shows-me-my-email-is-linked-to-another-microsoft-account"></a>En el inicio de sesión con la cuenta de Microsoft se muestra que el correo electrónico está vinculado a otra cuenta de Microsoft

Si ha intentado iniciar sesión con la cuenta de Microsoft, por ejemplo, con el correo electrónico `account1@outlook.com`, y ve un error similar al siguiente:
> _The account with email 'account1@outlook.com' is linked with another microsoft account._ (La cuenta de Microsoft con el correo electrónico "account1@outlook.com" está vinculada a otra cuenta de nuget.org).
>
> _If you would like to update the linked Microsoft account you can do so from the account settings page._ (Si quiere actualizar la cuenta de Microsoft vinculada, puede hacerlo desde la página de configuración de la cuenta)

**¿Qué significa el error anterior?**

Cuando se crea una cuenta en nuget.org, hay una dirección de correo electrónico de comunicación asociada a esa cuenta. Esta suele ser la misma dirección de correo electrónico que se ha usado para la cuenta de Microsoft asociada. Pero podría elegir especificar otra dirección de correo electrónico para la comunicación. Por tanto, técnicamente, podría tener otra cuenta Microsoft, por ejemplo, con `account2@outlook.com`, vinculada a la cuenta de nuget.org con la dirección de correo electrónico de comunicación como `account1@outlook.com`.

Por tanto, el error anterior significa que ya existe la cuenta de NuGet.org con la dirección de correo electrónico de comunicación `account1@outlook.com`, pero está asociada a otra cuenta Microsoft con un correo electrónico **que no es** `account1@outlook.com`.

**¿Cómo averiguo qué cuenta de Microsoft está vinculada con esta cuenta de nuget.org?**

Debe usar el flujo de [asistencia para el inicio de sesión](#which-microsoft-account-is-linked-to-my-nugetorg-account) para averiguar qué cuenta Microsoft está vinculada a la cuenta de nuget.org con la dirección de correo electrónico `account1@outlook.com`.

**Quiero reemplazar esa cuenta con mi cuenta de Microsoft**

Siga los pasos de la sección [No puedo usar el inicio de sesión de Microsoft, ¿cómo recupero mi cuenta de nuget.org?](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account) para asociar la cuenta Microsoft a la cuenta de nuget.org existente.

### <a name="unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account"></a>No puedo usar el inicio de sesión de Microsoft, ¿cómo recupero mi cuenta de nuget.org?

Si ha intentado usar la [asistencia para el inicio sesión](#which-microsoft-account-is-linked-to-my-nugetorg-account) y no tiene acceso a la cuenta Microsoft asociada a la cuenta de nuget.org, siga los pasos siguientes para vincular una cuenta Microsoft a la de nuget.org.
1. **Requisito**: Necesitará acceso a una cuenta Microsoft que no esté asociada a las cuentas de nuget.org existentes. Si no tiene una, puede [crearla](https://signup.live.com).
2. Si ha olvidado el nombre de usuario y la contraseña de su cuenta de nuget.org, siga los [pasos para recuperar las credenciales para iniciar sesión](#how-to-recover-nugetorg-password-login).
3. [Inicie sesión en nuget.org](https://www.nuget.org/users/account/LogOnNuGetAccount) con el inicio de sesión de usuario y contraseña.
4. Una vez iniciada la sesión, verá aparecer un cuadro de diálogo emergente similar al siguiente. Es el cuadro de diálogo de suspensión de la contraseña.
5. **NOTA**: Omita las instrucciones para iniciar sesión con la cuenta de Microsoft especificada. Ahora puede vincular la cuenta de nuget.org con cualquier otro inicio de sesión de Microsoft.
6. Haga clic en el botón **Sign in with Microsoft** (Inicio de sesión con Microsoft) e inicie sesión con la cuenta de Microsoft a la que tenga acceso, como se mencionó en el paso 1.
7. Ahora la cuenta se vinculará a la nueva cuenta Microsoft, que a partir de ahora podrá usar para iniciar sesión en nuget.org.

    ![Cuadro de diálogo Vincular MSA](media/link-msa-dialog.png)

### <a name="how-to-transform-my-nugetorg-account-to-an-organization"></a>¿Cómo se transforma la cuenta de nuget.org en una organización?

Si quiere transformar la cuenta en una organización, y esta cuenta ya está asociada con un inicio de sesión de cuenta de Microsoft, siga los pasos indicados en la documentación para [organizaciones en nuget.org](organizations-on-nuget-org.md).

Sin embargo, si la cuenta de nuget.org no está asociada ni vinculada a una cuenta Microsoft, puede seguir los pasos siguientes para transformar esta cuenta en una organización.
1. **Requisito**: Primero debe crear una cuenta individual en nuget.org para usarla como administrador en la cuenta de organización. Si no tiene una, [cree una cuenta de nuget.org](individual-accounts.md).
2. Siga los [pasos para recuperar la contraseña de inicio de sesión](#how-to-recover-nugetorg-password-login) para la cuenta de nuget.org si no tiene inicio de sesión de contraseña para ella; si lo tiene, omita este paso.
3. [Inicie sesión en nuget.org](https://www.nuget.org/users/account/LogOnNuGetAccount) con el inicio de sesión de usuario y contraseña.
4. Una vez iniciada la sesión, verá aparecer un cuadro de diálogo emergente similar al siguiente. Es el cuadro de diálogo de suspensión de la contraseña. 
    > [!Important]
    > Omita este cuadro de diálogo, **no** haga clic en el botón **Sign in with microsoft** (Inicio de sesión con Microsoft).

5. Vaya a [https://www.nuget.org/account/transform](https://www.nuget.org/account/transform). Esto le permitirá convertir la cuenta de nuget.org en una de organización sin vincularla a una cuenta Microsoft.
6. Especifique el nombre de usuario de administrador para la cuenta personal de nuget.org o la que haya creado en el paso 1.
7. Siga las instrucciones para completar la transformación de esta cuenta en una organización.

    ![Cuadro de diálogo Vincular MSA](media/link-msa-dialog.png)

### <a name="nugetorg-login-issues-for-aad-accounts-with-unmanaged-tenant"></a>¿Tiene problemas de inicio de sesión en nuget.org para cuentas de AAD con un inquilino no administrado?

Si ve un error como el siguiente durante el flujo de inicio de sesión con el dominio de la cuenta de correo electrónico (@yourdomain.com), vea los pasos siguientes para recuperar la cuenta de nuget.org.

<p align="center">
    <img src="media/unmanaged-aad-tenant.png" />
</p>

**¿Qué significa lo de estado no administrado durante el inicio de sesión? ¿Y por qué sucede ahora?** 

Parece que la cuenta se ha registrado previamente como una cuenta personal de Microsoft y que funcionaba correctamente, pero ahora parece que se ha registrado como un inquilino "no administrado" en Azure Active Directory (el servicio de identidad que se usa para autenticar las cuentas de Microsoft). 

Esto podría haber ocurrido si usted o alguien de la organización (con la dirección de correo electrónico @yourdomain.com) se ha registrado con uno de los servicios integrados de AAD o ha realizado un [registro de autoservicio para Azure Active Directory](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-self-service-signup), lo que crea ese inquilino "no administrado" para el dominio de la cuenta de Microsoft que se usa (en este caso, @yourdomain.com). 

**¿Qué puedo hacer para recuperar mi cuenta?**

En este momento, en nuget.org no contamos con ninguna forma de autenticar cuentas con estas cuentas de inquilino "no administrado" en Azure Active Directory. Buscamos una mejor manera de autenticar este tipo de cuentas.

Si quiere iniciar sesión en nuget.org con la cuenta Microsoft (@yourdomain.com), usted (o un administrador de la empresa), tendrá que reclamar la propiedad de AAD mediante una validación de DNS para autenticar a los usuarios con la dirección de correo electrónico "@yourdomain.com". Siga los pasos para la [adquisición de dominios como administrador](https://docs.microsoft.com/azure/active-directory/users-groups-roles/domains-admin-takeover) que se documentan en Azure Active Directory. Una vez hecho esto, el inicio de sesión normal debería empezar a funcionar.

**No me interesa hacer todo eso, ¿cuál es la otra forma de recuperar la cuenta?**

Puede [crear](https://www.microsoft.com/account) una cuenta de Microsoft (con un correo electrónico que **no** esté asociado a @yourdomain.com). Siga los pasos indicados en la sección sobre cómo [recuperar la cuenta de nuget.org](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account).

### <a name="how-do-i-change-my-nugetorg-account-username"></a>¿Cómo puedo cambiar el nombre de usuario de la cuenta de nuget.org?

No se puede. De acuerdo con la directiva, no se permite el cambio de los nombres de usuario. Además, realizar esta acción conlleva un cambio importante para los usuarios que puedan haber definido [directivas de confianza de paquetes basadas en el propietario del paquete](../consume-packages/installing-signed-packages.md#trust-package-owners). La única forma de cambiar el nombre de usuario consiste en crear una cuenta con el nombre de usuario deseado. Se recomienda eliminar la cuenta existente antes de crear una nueva; en caso contrario, no podrá volver a usar la cuenta de Microsoft registrada.
> [!Important]
> Al eliminar el usuario se seguirá **reservando** el `username`. No podrá volver a usar el mismo nombre de usuario, **incluido el cambio de mayúsculas y minúsculas**. Por ejemplo, si ha creado un usuario con el nombre de usuario `mycoolname` y quiere cambiarlo a `MyCoolName`(cambio de mayúsculas y minúsculas), no será posible después de eliminar el usuario.

Siga los pasos indicados en la sección [Eliminación de la cuenta de nuget.org](#how-to-delete-my-nugetorg-account) y [registre una cuenta nueva](individual-accounts.md) con el nombre de usuario correcto.

### <a name="how-to-delete-my-nugetorg-account"></a>¿Cómo elimino mi cuenta de nuget.org?

Para eliminar la cuenta, tenga en cuenta que se recomienda transferir la propiedad de todos los paquetes de los que sea el único propietario. En [Administración de los propietarios de paquetes](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg) puede obtener más información sobre cómo hacerlo. Esto también nos ayudará a acelerar su solicitud.

Si lo que busca es transformar su cuenta en una organización, consulte [¿Cómo se transforma la cuenta de nuget.org en una organización?](#how-to-transform-my-nugetorg-account-to-an-organization) siga los pasos indicados.

> [!Important]
> La eliminación del usuario tendrá como resultado lo siguiente:
>  1. Su nombre de usuario se reservará y nadie podrá volver a usarlo para crear una cuenta individual o una cuenta de organización.
>  1. La revocación de las claves de API asociadas. 
>  1. La eliminación de la cuenta como propietario de todos los paquetes secundarios.
>  1. La desasociación de esta cuenta de todas las reservas de prefijo de identificador existentes anteriormente.
>  1. La eliminación de la cuenta como un miembro de todas las organizaciones.

Siga los pasos siguientes para continuar con la eliminación de la cuenta.
1. [Inicie sesión en nuget.org](https://www.nuget.org/users/account/LogOn) con la cuenta que quiera eliminar.
2. Haga clic en esta dirección URL: [https://www.nuget.org/account/delete](https://www.nuget.org/account/delete) y siga los pasos para enviar la solicitud de eliminación de la cuenta.

Nuestro servicio de soporte técnico al cliente procesará esta solicitud y realizará la eliminación de la cuenta.
