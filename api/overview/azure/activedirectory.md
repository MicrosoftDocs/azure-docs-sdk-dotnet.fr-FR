---
title: Bibliothèques Azure Active Directory pour .NET
description: Référence pour les bibliothèques Azure Active Directory pour .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: active-directory
ms.openlocfilehash: 0226f06546f7dc14b9ab3392008744754d47a19a
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190222"
---
# <a name="azure-active-directory-libraries-for-net"></a>Bibliothèques Azure Active Directory pour .NET

## <a name="overview"></a>Vue d’ensemble

Authentifiez des utilisateurs et gérez l’accès aux applications et aux API avec Azure Active Directory.

Pour découvrir Azure Active Directory, consultez [Connexion et déconnexion à une application web ASP.NET avec Azure AD](/azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet).

## <a name="client-library"></a>Bibliothèque cliente

Connectez et authentifiez des utilisateurs ou des applications sur OAuth2, OpenID Connect, l’API d’authentification Active Directory Graph ou [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference).

Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.AppService.Fluent) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

#### <a name="net-core-cli"></a>CLI .NET Core

```bash
dotnet add package Microsoft.IdentityModel.Clients.ActiveDirectory
```

### <a name="code-example"></a>Exemple de code

Récupérez un jeton d’accès pour une application de bureau.

```csharp
/* Include this "using" directive...
using Microsoft.IdentityModel.Clients.ActiveDirectory;
*/

AuthenticationResult result = null;
AuthenticationContext authContext = new AuthenticationContext("https://someauthority.com");
try
{
    result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Auto));
}
catch (AdalException ex)
{
    // An unexpected error occurred, or user canceled the sign in.
    if (ex.ErrorCode != "access_denied")
        MessageBox.Show(ex.Message);

    return;
}
```

> [!div class="nextstepaction"]
> [Explorer les API clientes](/dotnet/api/overview/azure/activedirectory/client)

### <a name="samples"></a>Exemples

* [Utiliser OpenID Connect pour authentifier les utilisateurs à partir d’un locataire Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect)
* [Utiliser Oauth2 pour appeler une API web avec les autorisations d’application](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-appidentity)
* [Utiliser un contrôle d’accès basé sur les rôles (RBAC) dans une application](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims)

Explorez la collection complète d’[exemples de code Azure Active Directory](/azure/active-directory/develop/active-directory-code-samples).

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
