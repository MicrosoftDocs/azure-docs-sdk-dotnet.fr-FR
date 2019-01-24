---
title: Bibliothèques Azure Container Instances pour .NET
description: Référence pour les bibliothèques Azure Container Instances pour .NET
ms.date: 06/11/2018
ms.topic: reference
ms.service: container-instances
ms.openlocfilehash: 552746b316f1ba80adce5f55bb22412749fd93bc
ms.sourcegitcommit: 4f7bc5c5cd333e41446a3ebe5639a211d8ac9b90
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54841276"
---
# <a name="azure-container-instances-libraries-for-net"></a>Bibliothèques Azure Container Instances pour .NET

Les bibliothèques Azure Container Instances pour .NET permettent de créer et gérer des instances de conteneurs Azure. Pour en savoir plus, consultez [Vue d’ensemble d’Azure Container Instances](/azure/container-instances/container-instances-overview).

## <a name="management-library"></a>Bibliothèque de gestion

Utilisez la bibliothèque de gestion pour créer et gérer des instances de conteneurs Azure dans Azure.

Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.ContainerInstance.Fluent) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.ContainerInstance.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.ContainerInstance.Fluent
```

## <a name="example-source"></a>Exemple de source

Si vous souhaitez voir les exemples de code suivants en contexte, vous pouvez les trouver dans le référentiel GitHub suivant :

[Azure-Samples/aci-docs-sample-dotnet](https://github.com/Azure-Samples/aci-docs-sample-dotnet)

## <a name="authentication"></a>Authentification

Une des méthodes les plus simples pour authentifier les clients du Kit de développement logiciel (SDK) consiste à utiliser [l’authentification basée sur le fichier][sdk-auth]. L’authentification basée sur le fichier analyse un fichier d’informations d’identification lors de l’instanciation de l’objet client [IAzure][iazure], qui utilise ensuite ces informations d’identification lors de l’authentification avec Azure. Pour utiliser l’authentification basée sur un fichier :

1. Créer un fichier d’informations d’identification avec [Azure CLI](/cli/azure) ou [Cloud Shell](https://shell.azure.com/) :

   `az ad sp create-for-rbac --sdk-auth > my.azureauth`

   Si vous utilisez [Cloud Shell](https://shell.azure.com/) pour générer le fichier d’informations d’identification, copiez son contenu dans un fichier local auquel votre application .NET peut accéder.

2. Définissez la `AZURE_AUTH_LOCATION` variable d’environnement sur le chemin d’accès complet au fichier d’informations d’identification généré. Par exemple (dans l’interpréteur de commandes Bash) :

   ```bash
   export AZURE_AUTH_LOCATION=/home/yourusername/my.azureauth
   ```

Une fois que vous avez créé le fichier d’informations d’identification et rempli la variable d’environnement `AZURE_AUTH_LOCATION`, utilisez la méthode [Azure.Authenticate][iazure-authenticate] pour initialiser l’objet client [IAzure][iazure]. Le projet exemple obtient d’abord la valeur `AZURE_AUTH_LOCATION`, puis appelle une méthode qui retourne un objet client `IAzure` initialisé :

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->  
[!code-csharp[authenticate](~/aci-docs-sample-dotnet/Program.cs#L29-L35 "Get environment variable")]

Cette méthode issue de l’application exemple retourne l’instance [IAzure][iazure] initialisée, qui est ensuite transmise en tant que premier paramètre à toutes les autres méthodes de l’exemple :

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->  
[!code-csharp[authenticate](~/aci-docs-sample-dotnet/Program.cs#azure_auth "Authenticate IAzure client object")]

Pour plus d’informations sur les méthodes d’authentification disponibles dans les bibliothèques de gestion .NET pour Azure, consultez [Authentification avec les bibliothèques de gestion Azure pour .NET][sdk-auth].

## <a name="create-container-group---single-container"></a>Créer un groupe de conteneurs : conteneur unique

Cet exemple crée un groupe de conteneurs à un seul conteneur.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->  
[!code-csharp[create_container_group](~/aci-docs-sample-dotnet/Program.cs#create_container_group "Create single-container group")]

## <a name="create-container-group---multiple-containers"></a>Créer un groupe de conteneurs : plusieurs conteneurs

Cet exemple crée un groupe de conteneurs avec deux conteneurs : un conteneur d’application et un conteneur side-car.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->  
[!code-csharp[create_container_group_multi](~/aci-docs-sample-dotnet/Program.cs#create_container_group_multi "Create multi-container group")]

## <a name="asynchronous-container-create-with-polling"></a>Création d’un conteneur asynchrone avec interrogation

Cet exemple crée un groupe de conteneurs à un seul conteneur à l’aide de la méthode de création asynchrone. Il interroge ensuite Azure au sujet du groupe de conteneurs, puis génère l’état du groupe de conteneurs jusqu'à ce que son état change en « En cours d’exécution ».

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->  
[!code-csharp[create_container_group_polling](~/aci-docs-sample-dotnet/Program.cs#create_container_group_polling "Create single-container group with async and polling")]

## <a name="create-task-based-container-group"></a>Créer un groupe de conteneurs basé sur des tâches

Cet exemple crée un groupe de conteneurs à un seul conteneur basé sur des tâches. Le conteneur est configuré avec une [stratégie de redémarrage](/azure/container-instances/container-instances-restart-policy) sur « Jamais » et une [ligne de commande personnalisée](/azure/container-instances/container-instances-restart-policy#command-line-override).

Si vous souhaitez exécuter une commande unique avec des arguments avec plusieurs lignes de commande, par exemple `echo FOO BAR`, vous devez les fournir en tant que tableau de chaînes à la méthode `WithStartingCommandLines`. Par exemple : 

`WithStartingCommandLines("echo", "FOO", "BAR")`

Si, toutefois, vous souhaitez exécuter plusieurs commandes avec (éventuellement) plusieurs arguments, vous devez exécuter un interpréteur de commandes et passer les commandes en chaînes en tant qu’argument. Par exemple, cela exécute à la fois une commande `echo` et une commande `tail` :

`WithStartingCommandLines("/bin/sh", "-c", "echo FOO BAR && tail -f /dev/null")`

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->  
[!code-csharp[create_container_group_task](~/aci-docs-sample-dotnet/Program.cs#create_container_group_task "Run a task-based container")]

## <a name="list-container-groups"></a>Répertorier les groupes de conteneurs

Cet exemple répertorie les groupes de conteneur dans un groupe de ressources.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->  
[!code-csharp[list_container_groups](~/aci-docs-sample-dotnet/Program.cs#list_container_groups "List container groups")]

## <a name="get-an-existing-container-group"></a>Obtenir un groupe de conteneurs existant

Cet exemple obtient un groupe de conteneurs spécifique résidant dans un groupe de ressources, puis imprime certaines de ses propriétés et ses valeurs.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->  
[!code-csharp[get_container_group](~/aci-docs-sample-dotnet/Program.cs#get_container_group "Get container group")]

## <a name="delete-a-container-group"></a>Supprimer un groupe de conteneurs

Cet exemple supprime un groupe de conteneurs à partir d’un groupe de ressources.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->  
[!code-csharp[delete_container_group](~/aci-docs-sample-dotnet/Program.cs#delete_container_group "Delete container group")]

## <a name="api-reference"></a>Informations de référence sur l'API

> [!div class="nextstepaction"]
> [Explorer les API de gestion](/dotnet/api/overview/azure/containerinstances/management)

## <a name="samples"></a>Exemples

* Le code source pour les exemples précédents est accessible sur GitHub :

  [Azure-Samples/aci-docs-sample-dotnet][aci-docs-sample-dotnet]

* Plus d’exemples de code Azure Container Instances :

  [Exemples de code Azure][samples]

Découvrez d’autres [exemples de code .NET](https://azure.microsoft.com/resources/samples/?platform=dotnet) à utiliser dans vos applications.

<!-- LINKS - External -->
[aci-docs-sample-dotnet]: https://github.com/Azure-Samples/aci-docs-sample-dotnet
[samples]: https://azure.microsoft.com/resources/samples/?sort=0&term=ACI
[sdk-auth]: https://github.com/Azure/azure-libraries-for-net/blob/master/AUTH.md

<!-- LINKS - Internal -->
[DotNetCLI]: /dotnet/core/tools/dotnet-add-package
[PackageManager]: /nuget/tools/package-manager-console
[iazure]: /dotnet/api/microsoft.azure.management.fluent.azure
[iazure-authenticate]: /dotnet/api/microsoft.azure.management.fluent.azure.authenticate
