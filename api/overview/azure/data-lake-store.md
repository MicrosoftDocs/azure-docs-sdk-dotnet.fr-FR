---
title: Bibliothèques Azure Data Lake Store pour .NET
description: Référence pour les bibliothèques Azure Data Lake Store pour .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: data-lake-store
ms.openlocfilehash: 8e55a21d84eae2ef4104c8253adec2cbc4b008e5
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190562"
---
# <a name="azure-data-lake-store-libraries-for-net"></a>Bibliothèques Azure Data Lake Store pour .NET

## <a name="overview"></a>Vue d’ensemble

Azure Data Lake Store est un référentiel d'entreprise à très grande échelle pour les charges de travail d'analyse du Big Data. Azure Data Lake vous permet de capturer les données de toute taille, de tout type et à toute vitesse d'ingestion dans un emplacement unique en vue d'une analyse opérationnelle et exploratoire.

Pour en savoir plus, consultez [Vue d’ensemble d’Azure Data Lake Store](/azure/data-lake-store/data-lake-store-overview).

## <a name="client-library"></a>Bibliothèque cliente

Utilisez la bibliothèque de client pour exécuter des opérations de système de fichiers sur Data Lake Store, telles que la création de dossiers dans un compte Data Lake Store, le chargement et le téléchargement de fichiers.  Pour obtenir un didacticiel complet sur l’utilisation de Data Lake Store avec .NET, consultez la section [Opérations de gestion du système de fichiers sur Data Lake Store à l’aide du kit de développement logiciel (SDK) .NET](/azure/data-lake-store/data-lake-store-data-operations-net-sdk).

Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Microsoft.Azure.DataLake.Store
```

```bash
dotnet add package Microsoft.Azure.DataLake.Store
```
### <a name="authentication"></a>Authentification

* Pour en savoir plus sur l’authentification des utilisateurs accédant à votre application, consultez la section relative à [l’authentification de l’utilisateur avec Data Lake Store à l’aide du Kit de développement logiciel (SDK) .NET](/azure/data-lake-store/data-lake-store-end-user-authenticate-net-sdk).
* Pour en savoir plus sur l’authentification entre les services dans le cadre de votre application, consultez la section relative à [l’authentification entre les services avec Data Lake Store à l’aide du Kit de développement logiciel (SDK) .NET](/azure/data-lake-store/data-lake-store-service-to-service-authenticate-net-sdk).

### <a name="code-example"></a>Exemple de code

L’extrait de code suivant permet de créer l’objet client filesystem Data Lake Store qui est utilisé pour adresser des requêtes au service.

```csharp
// Create client objects
AdlsClient client = AdlsClient.CreateClient(_adlsAccountName, adlCreds);
```

> [!div class="nextstepaction"]
> [Explorer les API clientes](/dotnet/api/overview/azure/datalakestore/client)


## <a name="management-library"></a>Bibliothèque de gestion

Utilisez la bibliothèque de gestion pour vous connecter à vos référentiels de données volumineuses et les gérer.

Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.DataLake.Store
```

```bash
dotnet add package Microsoft.Azure.Management.DataLake.Store
```

> [!div class="nextstepaction"]
> [Explorer les API clientes](/dotnet/api/overview/azure/datalakestore/management)


## <a name="samples"></a>Exemples

* [Exemple de Client Azure Data Lake .NET](https://azure.microsoft.com/resources/samples/data-lake-dotnet-client/)

Découvrez d’autres [exemples de code .NET](https://azure.microsoft.com/resources/samples/?platform=dotnet) à utiliser dans vos applications.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
