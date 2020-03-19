---
title: 'Cuentas individuales: nuget.org'
description: Se requieren cuentas individuales en NuGet.org para publicar paquetes.
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 7951b3db0cdcaee0a1eb955a5bf6fedce24c79c9
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428634"
---
# <a name="individual-accounts-on-nugetorg"></a>Cuentas individuales en nuget.org

Debe crear una cuenta individual para publicar y administrar paquetes en NuGet.org.

## <a name="individual-accounts-vs-organization-accounts"></a>Cuentas individuales frente a cuentas de organización

Su cuenta individual (de usuario) es su identidad en NuGet.org y puede ser un miembro de cualquier número de organizaciones. Un paquete puede pertenecer a una cuenta de organización y a una cuenta individual. Los consumidores de paquetes no perciben ninguna diferencia entre una cuenta individual y una cuenta de organización, ya que ambas aparecen como `owners` (propietarias) del paquete.

Una cuenta de organización tiene una o varias cuentas individuales como miembros. Estos miembros pueden administrar un conjunto de paquetes al tiempo que mantienen una identidad única para la propiedad.

## <a name="add-a-new-individual-account"></a>Adición de una nueva cuenta individual

Para crear una cuenta de NuGet.org, necesita una cuenta personal de Microsoft (MSA) o Azure Active Directory (AAD). Si no tiene una, puede [crearla](https://signup.live.com). Siga los pasos que se indican a continuación si tiene una cuenta de MSA o AAD.

1. Vaya a la [página de inicio de sesión de NuGet.org](https://www.nuget.org/users/account/LogOn).

1. Haga clic en el botón**Sign in with Microsoft** (Inicio de sesión con Microsoft).

1. Especifique los detalles de su cuenta Microsoft o de Azure Active Directory.

1. Haga clic en **Sí** para aceptar los permisos que se van a asignar a la aplicación de *NuGet.org*.

   ![Concesión de permisos a NuGet.org](media/nuget-org-permissions.png)

1. Se le redirigirá a *nuget.org* y se le pedirá que registre un nombre de usuario.

1. Especifique el nombre de usuario en el cuadro de entrada. Tenga en cuenta que el nombre de usuario **distingue** mayúsculas de minúsculas y no se puede cambiar más adelante.

   ![Indicación de un nombre de usuario en NuGet.org](media/nuget-org-register.png) 

1. Haga clic en el botón **Registrar**.

Ya tiene una cuenta de NuGet.org. Puede realizar la administración de la cuenta en la página de [configuración de la cuenta](https://www.nuget.org/account).

## <a name="enable-two-factor-authentication-2fa"></a>Habilitación de la autenticación en dos fases (2FA)

La autenticación en dos fases, o 2FA, es una capa de seguridad adicional que se usa al iniciar sesión en sitios web o aplicaciones. Con 2FA, tiene que iniciar sesión con su cuenta de Microsoft (MSA) y ofrecer otra forma de autenticación que solo usted conoce o a la que tiene acceso. Para proteger mejor la cuenta, habilite la autenticación en dos fases (recomendado).

1. Cuando haya iniciado sesión en la cuenta, abra su perfil y elija **Habilitar** en **Cuenta de inicio de sesión**.

   ![Habilitación de la autenticación en dos fases](media/nuget-org-register-2fa.png)

   Verá un mensaje que le indica que la próxima vez que inicie sesión en *nuget.org*, se le pedirán credenciales adicionales.

2. Para completar la autenticación en este momento, cierre la sesión y vuelva a iniciarla.

3. Cuando inicie sesión, elija si la segunda forma de autenticación será por texto o correo electrónico.

   Compruebe el número de teléfono o el correo electrónico que ya tiene asociado con su cuenta de Microsoft. Es posible que tenga que escribir un nuevo número de teléfono o correo electrónico para la cuenta. Si es así, escriba la información necesaria tal como se indica y haga clic en **Siguiente**.

   ![Habilitación de la autenticación en dos fases](media/nuget-org-sign-in-2fa.png)

4. Revise el dispositivo o la cuenta de correo electrónico y escriba el código que acaba de recibir.

   ![Habilitación de la autenticación en dos fases](media/nuget-org-enter-code-2fa.png)

5. Siga cualquier instrucción adicional para completar la autenticación en dos fases.

> [!Tip]
> La habilitación de 2FA para la cuenta de nuget.org no afecta a la configuración de autenticación para otras cuentas o servicios que puedan estar vinculados a la cuenta de Microsoft que se usa para iniciar sesión en NuGet.org.

## <a name="delete-a-nugetorg-account"></a>Eliminación de una cuenta de nuget.org

Para obtener ayuda con las tareas adicionales relacionadas con las cuentas, como la eliminación de una cuenta de nuget.org, vea [Administración de cuentas de nuget.org](nuget-org-faq.md#nugetorg-account-management).
