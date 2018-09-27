---
title: Bibliothèques Azure Automation pour .NET
description: Référence pour les bibliothèques Azure Automation pour .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: automation
ms.openlocfilehash: 4890faab86d1319fe802a30e3735419ac65e8d64
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190282"
---
# <a name="azure-automation-libraries-for-net"></a><span data-ttu-id="7b1b2-103">Bibliothèques Azure Automation pour .NET</span><span class="sxs-lookup"><span data-stu-id="7b1b2-103">Azure Automation libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="7b1b2-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="7b1b2-104">Overview</span></span>

<span data-ttu-id="7b1b2-105">Microsoft Azure Automation permet aux utilisateurs d’automatiser les tâches communément exécutées dans un environnement cloud et d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-105">Microsoft Azure Automation provides a way for users to automate the tasks that are commonly performed in a cloud and enterprise environment.</span></span> 

<span data-ttu-id="7b1b2-106">Pour en savoir plus, consultez [Vue d’ensemble d’Azure Automation](/azure/automation/automation-intro).</span><span class="sxs-lookup"><span data-stu-id="7b1b2-106">Learn more by reading the [Azure Automation Overview](/azure/automation/automation-intro).</span></span>

## <a name="management-library"></a><span data-ttu-id="7b1b2-107">Bibliothèque de gestion</span><span class="sxs-lookup"><span data-stu-id="7b1b2-107">Management library</span></span>

<span data-ttu-id="7b1b2-108">Utilisez la bibliothèque de gestion pour gérer les runbooks, les travaux et les paramètres de la Configuration d’état souhaitée.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-108">Using the management library to manage runbooks and jobs and manage Desired State Configuration settings.</span></span>

<span data-ttu-id="7b1b2-109">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Automation) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="7b1b2-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Automation) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="7b1b2-110">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7b1b2-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Automation
```

```bash
dotnet add package Microsoft.Azure.Management.Automation
```

### <a name="code-example"></a><span data-ttu-id="7b1b2-111">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="7b1b2-111">Code Example</span></span>

<span data-ttu-id="7b1b2-112">L’exemple suivant montre comment démarrer un nouveau travail basé sur un runbook existant.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-112">The following example illustrates how to start a new job based on an existing runbook.</span></span>

```csharp
/*
  using Microsoft.Azure.Management.Automation;
*/
AutomationManagementClient client =
    new AutomationManagementClient(new CertificateCloudCredentials(subscriptionId, cert));

// Create job create parameters
JobCreateParameters jcParam = new JobCreateParameters
{
    Properties = new JobCreateProperties
    {
        Runbook = new RunbookAssociationProperty
        {
            Name = runbookName
        },
        Parameters = null // optional parameters here
    }
};

// create runbook job. This gives back the Job
Job job = automationManagementClient.Jobs.Create(automationAccountName, jcParam).Job;
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="7b1b2-113">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="7b1b2-113">Explore the management APIs</span></span>](/dotnet/api/overview/azure/automation/management)

## <a name="samples"></a><span data-ttu-id="7b1b2-114">Exemples</span><span class="sxs-lookup"><span data-stu-id="7b1b2-114">Samples</span></span>

* <span data-ttu-id="7b1b2-115">[AzureBot](https://github.com/Microsoft/AzureBot) utilise la bibliothèque automatisation avec l’infrastructure [Bot Framework](https://docs.microsoft.com/bot-framework/) et les [Services cognitifs](/cognitive-services) afin d’améliorer la productivité des développeurs sur Azure</span><span class="sxs-lookup"><span data-stu-id="7b1b2-115">[AzureBot](https://github.com/Microsoft/AzureBot) uses the automation library with the [Bot Framework](https://docs.microsoft.com/bot-framework/) and [Cognitive Services](/cognitive-services) to improve developer productivity on Azure</span></span>

<span data-ttu-id="7b1b2-116">Découvrez d’autres [exemples de code .NET](https://azure.microsoft.com/resources/samples/?platform=dotnet) à utiliser dans vos applications.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-116">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
