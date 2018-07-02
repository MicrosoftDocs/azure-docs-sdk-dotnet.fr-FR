---
title: Bibliothèques Azure Active Directory pour .NET
description: Référence pour les bibliothèques Azure Active Directory pour .NET
keywords: Azure, .NET, SDK, API, AAD, Active Directory
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: active-directory
ms.custom: devcenter, svc-overview
ms.openlocfilehash: a5a228fcde29dbef6a6e8d0482121ee710b002a4
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065859"
---
# <a name="azure-active-directory-libraries-for-net"></a><span data-ttu-id="e5455-104">Bibliothèques Azure Active Directory pour .NET</span><span class="sxs-lookup"><span data-stu-id="e5455-104">Azure Active Directory libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="e5455-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="e5455-105">Overview</span></span>

<span data-ttu-id="e5455-106">Authentifiez des utilisateurs et gérez l’accès aux applications et aux API avec Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e5455-106">Sign-on users and manage access to applications and APIs with Azure Active Directory.</span></span>

<span data-ttu-id="e5455-107">Pour découvrir Azure Active Directory, consultez [Connexion et déconnexion à une application web ASP.NET avec Azure AD](/azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet).</span><span class="sxs-lookup"><span data-stu-id="e5455-107">To get started with Azure Active Directory, see [ASP.NET web app sign-in and sign-out with Azure AD](/azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet).</span></span>

## <a name="client-library"></a><span data-ttu-id="e5455-108">Bibliothèque cliente</span><span class="sxs-lookup"><span data-stu-id="e5455-108">Client library</span></span>

<span data-ttu-id="e5455-109">Connectez et authentifiez des utilisateurs ou des applications sur OAuth2, OpenID Connect, l’API d’authentification Active Directory Graph ou [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference).</span><span class="sxs-lookup"><span data-stu-id="e5455-109">Connect and authenticate users or applications over OAuth2, OpenID Connect, Active Directory Graph API authentication or [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference).</span></span>

<span data-ttu-id="e5455-110">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.AppService.Fluent) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="e5455-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.AppService.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="e5455-111">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e5455-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

#### <a name="net-core-cli"></a><span data-ttu-id="e5455-112">CLI .NET Core</span><span class="sxs-lookup"><span data-stu-id="e5455-112">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.IdentityModel.Clients.ActiveDirectory
```

### <a name="code-example"></a><span data-ttu-id="e5455-113">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="e5455-113">Code Example</span></span>

<span data-ttu-id="e5455-114">Récupérez un jeton d’accès pour une application de bureau.</span><span class="sxs-lookup"><span data-stu-id="e5455-114">Retrieve an access token for a desktop application.</span></span>

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
> [<span data-ttu-id="e5455-115">Explorer les API clientes</span><span class="sxs-lookup"><span data-stu-id="e5455-115">Explore the client APIs</span></span>](/dotnet/api/overview/azure/activedirectory/client)

### <a name="samples"></a><span data-ttu-id="e5455-116">Exemples</span><span class="sxs-lookup"><span data-stu-id="e5455-116">Samples</span></span>

* [<span data-ttu-id="e5455-117">Utiliser OpenID Connect pour authentifier les utilisateurs à partir d’un locataire Azure AD</span><span class="sxs-lookup"><span data-stu-id="e5455-117">Use OpenID Connect to authenticate users from an Azure AD tenant</span></span>](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect)
* [<span data-ttu-id="e5455-118">Utiliser Oauth2 pour appeler une API web avec les autorisations d’application</span><span class="sxs-lookup"><span data-stu-id="e5455-118">Use Oauth2 to call a web API with application permissions</span></span>](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-appidentity)
* [<span data-ttu-id="e5455-119">Utiliser un contrôle d’accès basé sur les rôles (RBAC) dans une application</span><span class="sxs-lookup"><span data-stu-id="e5455-119">Use role-based access control (RBAC) in an application</span></span>](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims)

<span data-ttu-id="e5455-120">Explorez la collection complète d’[exemples de code Azure Active Directory](/azure/active-directory/develop/active-directory-code-samples).</span><span class="sxs-lookup"><span data-stu-id="e5455-120">Explore the full collection of [Azure Active Directory code samples](/azure/active-directory/develop/active-directory-code-samples).</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
