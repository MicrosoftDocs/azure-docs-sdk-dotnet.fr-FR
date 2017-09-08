---
title: "Exemples d’instruction de bibliothèques de gestion Azure pour .NET"
description: "Obtenez des exemples de code pour créer et mettre à jour des ressources à l’aide des bibliothèques de gestion Azure pour .NET."
keywords: Azure, .NET, SDK, API, exemple, exemple
author: camsoper
ms.author: casoper
manager: douge
ms.date: 06/20/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.assetid: 
ms.openlocfilehash: ffda7cca724962e6f953432c5cab04485ddabb03
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2017
---
# <a name="azure-management-libraries-for-net-sample-instructions"></a><span data-ttu-id="dc4ff-104">Exemple d’instructions de bibliothèques de gestion Azure pour .NET</span><span class="sxs-lookup"><span data-stu-id="dc4ff-104">Azure management libraries for .NET sample instructions</span></span>

<span data-ttu-id="dc4ff-105">Cet article décrit l’authentification et les conditions préalables requises pour exécuter des exemples pour les bibliothèques de gestion Azure pour .NET.</span><span class="sxs-lookup"><span data-stu-id="dc4ff-105">This article describes the prerequisites and authentication required for running the samples for the Azure management libraries for .NET.</span></span>

## <a name="prerequisties"></a><span data-ttu-id="dc4ff-106">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="dc4ff-106">Prerequisties</span></span> 

* [<span data-ttu-id="dc4ff-107">Visual Studio 2017](https://www.visualstudio.com/vs/) ou [SDK .NET Core</span><span class="sxs-lookup"><span data-stu-id="dc4ff-107">Visual Studio 2017](https://www.visualstudio.com/vs/) or [.NET Core SDK</span></span>](https://www.microsoft.com/net/download/core)
* <span data-ttu-id="dc4ff-108">Un [Abonnement Microsoft Azure](https://azure.microsoft.com/free/)</span><span class="sxs-lookup"><span data-stu-id="dc4ff-108">A [Microsoft Azure subscription](https://azure.microsoft.com/free/)</span></span>
* [<span data-ttu-id="dc4ff-109">Client de ligne de commande Git</span><span class="sxs-lookup"><span data-stu-id="dc4ff-109">Git command line client</span></span>](https://git-scm.com/)
* [<span data-ttu-id="dc4ff-110">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="dc4ff-110">Azure PowerShell</span></span>](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps)

## <a name="authentication-for-all-samples"></a><span data-ttu-id="dc4ff-111">Authentification pour tous les exemples</span><span class="sxs-lookup"><span data-stu-id="dc4ff-111">Authentication for all samples</span></span>

[!include[Create service principal](includes/create-sp.md)]

[!include[File-based authentication](includes/file-based-auth.md)]

## <a name="running-the-samples"></a><span data-ttu-id="dc4ff-112">Exécuter les exemples</span><span class="sxs-lookup"><span data-stu-id="dc4ff-112">Running the samples</span></span>

<span data-ttu-id="dc4ff-113">Une fois que vous avez utilisé Git pour cloner l’exemple, vous pouvez ouvrir l’exemple dans Visual Studio et l’exécuter à l’aide de l’IDE.</span><span class="sxs-lookup"><span data-stu-id="dc4ff-113">Once you have used Git to clone the sample, you can open the sample in Visual Studio and run the sample using the IDE.</span></span>  <span data-ttu-id="dc4ff-114">Vous pouvez également utiliser le Kit de développement logiciel (SDK) .NET Core pour générer et exécuter l’exemple à partir de la ligne de commande, comme suit :</span><span class="sxs-lookup"><span data-stu-id="dc4ff-114">Alternatively, use the .NET Core SDK to build and run the sample from the command line, like this:</span></span>

```cmd
git clone https://github.com/Azure-Samples/app-service-dotnet-configure-deployment-sources-for-web-apps.git
cd app-service-dotnet-configure-deployment-sources-for-web-apps
dotnet restore
dotnet run
```