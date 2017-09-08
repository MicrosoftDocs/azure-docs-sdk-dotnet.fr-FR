---
title: "Bibliothèques Azure Automation pour .NET"
description: "Référence pour les bibliothèques Azure Automation pour .NET"
keywords: Azure, .NET, SDK, API, Automation
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/21/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 1e1b5a662947503ff71f3e4a9b67f20a1e2d5f87
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2017
---
# <a name="azure-automation-libraries-for-net"></a>Bibliothèques Azure Automation pour .NET

## <a name="overview"></a>Vue d'ensemble

Microsoft Azure Automation permet aux utilisateurs d’automatiser les tâches communément exécutées dans un environnement cloud et d’entreprise. 

Pour en savoir plus, consultez [Vue d’ensemble d’Azure Automation](/azure/automation/automation-intro).

## <a name="management-library"></a>Bibliothèque de gestion

Utilisez la bibliothèque de gestion pour gérer les runbooks, les travaux et les paramètres de la Configuration d’état souhaitée.

Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Automation) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.Automation
```

```bash
dotnet add package Microsoft.Azure.Management.Automation
```

### <a name="code-example"></a>Exemple de code

L’exemple suivant montre comment démarrer un nouveau travail basé sur un runbook existant.

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
> [Explorer les API de gestion](/dotnet/api/overview/azure/automation/management)

## <a name="samples"></a>Exemples

* [AzureBot](https://github.com/Microsoft/AzureBot) utilise la bibliothèque automatisation avec l’infrastructure [Bot Framework](https://docs.microsoft.com/bot-framework/) et les [Services cognitifs](/cognitive-services) afin d’améliorer la productivité des développeurs sur Azure

Découvrez d’autres [exemples de code .NET](https://azure.microsoft.com/resources/samples/?platform=dotnet) à utiliser dans vos applications.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
