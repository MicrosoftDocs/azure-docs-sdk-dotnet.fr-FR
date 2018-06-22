---
title: Bibliothèques Azure Container Instances pour .NET
description: Référence pour les bibliothèques Azure Container Instances pour .NET
keywords: Azure, .NET, SDK, API, Container Instances, ACI
author: mmacy
ms.author: marsma
manager: jeconnoc
ms.date: 05/25/2018
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: dcontainer-instances
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 033f67a989b0ed6cfcb67a6212c0d5c46c485afa
ms.sourcegitcommit: 4ae9f77a9300a4fe54d0179055ae61191078f207
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/07/2018
ms.locfileid: "34567181"
---
# <a name="azure-container-instances-libraries-for-net"></a>Bibliothèques Azure Container Instances pour .NET

Les bibliothèques Azure Container Instances pour .NET permettent de créer et gérer des instances de conteneurs Azure. Pour en savoir plus, consultez [vue d’ensemble d’Azure Container Instances](/azure/container-instances/container-instances-overview).

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

## <a name="examples"></a>Exemples

### <a name="create-container-group---single-container"></a>Créer un groupe de conteneurs : conteneur unique

Cet exemple crée un groupe de conteneurs à un seul conteneur.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[create_container_group](~/aci-docs-sample-dotnet/Program.cs#create_container_group "Create single-container group")]

### <a name="create-container-group---multiple-containers"></a>Créer un groupe de conteneurs : plusieurs conteneurs

Cet exemple crée un groupe de conteneurs avec deux conteneurs : un conteneur d’application et un conteneur side-car.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[create_container_group_multi](~/aci-docs-sample-dotnet/Program.cs#create_container_group_multi "Create multi-container group")]

### <a name="asynchronous-container-create-with-polling"></a>Création d’un conteneur asynchrone avec interrogation

Cet exemple crée un groupe de conteneurs à un seul conteneur à l’aide de la méthode de création asynchrone. Il interroge ensuite Azure au sujet du groupe de conteneurs, puis génère l’état du groupe de conteneurs jusqu'à ce que son état change en « En cours d’exécution ».

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[create_container_group_polling](~/aci-docs-sample-dotnet/Program.cs#create_container_group_polling "Create single-container group with async and polling")]

### <a name="create-task-based-container-group"></a>Créer un groupe de conteneurs basé sur des tâches

Cet exemple crée un groupe de conteneurs à un seul conteneur basé sur des tâches. Le conteneur est configuré avec une [stratégie de redémarrage](/azure/container-instances/container-instances-restart-policy) sur « Jamais » et une [ligne de commande personnalisée](/azure/container-instances/container-instances-restart-policy#command-line-override).

Si vous souhaitez exécuter une commande unique avec des arguments avec plusieurs lignes de commande, par exemple `echo FOO BAR`, vous devez les fournir en tant que tableau de chaînes à la méthode `WithStartingCommandLines`. Par exemple : 

`WithStartingCommandLines("echo", "FOO", "BAR")`

Si, toutefois, vous souhaitez exécuter plusieurs commandes avec (éventuellement) plusieurs arguments, vous devez exécuter un interpréteur de commandes et passer les commandes en chaînes en tant qu’argument. Par exemple, cela exécute à la fois une commande `echo` et une commande `tail` :

`WithStartingCommandLines("/bin/sh", "-c", "echo FOO BAR && tail -f /dev/null")`

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[create_container_group_task](~/aci-docs-sample-dotnet/Program.cs#create_container_group_task "Run a task-based container")]

### <a name="list-container-groups"></a>Répertorier les groupes de conteneurs

Cet exemple répertorie les groupes de conteneur dans un groupe de ressources.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[list_container_groups](~/aci-docs-sample-dotnet/Program.cs#list_container_groups "List container groups")]

### <a name="get-an-existing-container-group"></a>Obtenir un groupe de conteneurs existant

Cet exemple obtient un groupe de conteneurs spécifique résidant dans un groupe de ressources, puis imprime certaines de ses propriétés et ses valeurs.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[get_container_group](~/aci-docs-sample-dotnet/Program.cs#get_container_group "Get container group")]

### <a name="delete-a-container-group"></a>Supprimer un groupe de conteneurs

Cet exemple supprime un groupe de conteneurs à partir d’un groupe de ressources.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[delete_container_group](~/aci-docs-sample-dotnet/Program.cs#delete_container_group "Delete container group")]

## <a name="api-reference"></a>Informations de référence sur l'API

> [!div class="nextstepaction"]
> [Explorer les API de gestion](/dotnet/api/overview/azure/containerinstances/management)

## <a name="samples"></a>Exemples

* Le code source pour les exemples précédents sont accessibles sur GitHub :

  [Azure-Samples/aci-docs-sample-dotnet][aci-docs-sample-dotnet]

* Plus d’exemples de code Azure Container Instances :

  [Exemples de code Azure][samples]

Découvrez d’autres [exemples de code .NET](https://azure.microsoft.com/resources/samples/?platform=dotnet) à utiliser dans vos applications.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
[samples]: https://azure.microsoft.com/resources/samples/?sort=0&term=ACI
[aci-docs-sample-dotnet]: https://github.com/Azure-Samples/aci-docs-sample-dotnet