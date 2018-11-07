---
ms.service: multiple
ms.date: 9/20/2018
ms.topic: include
ms.openlocfilehash: 5c8cb328802cfb94e944e4241852fb9568e8507f
ms.sourcegitcommit: 70982e900bd4adfbc121eba55d94544f17c6b495
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/06/2018
ms.locfileid: "51196056"
---
<span data-ttu-id="e0744-101">Votre application .NET a besoin d’autorisations pour lire et créer des ressources dans votre abonnement Azure afin d’utiliser les bibliothèques de gestion Azure pour .NET.</span><span class="sxs-lookup"><span data-stu-id="e0744-101">Your .NET application needs permissions to read and create resources in your Azure subscription in order to use the Azure Management Libraries for .NET.</span></span> <span data-ttu-id="e0744-102">Créez un principal de service et configurez votre application pour qu’elle s’exécute avec ses informations d’identification pour accorder cet accès.</span><span class="sxs-lookup"><span data-stu-id="e0744-102">Create a service principal and configure your app to run with its credentials to grant this access.</span></span> <span data-ttu-id="e0744-103">Les principaux de service permettent de créer un compte non interactif associé à votre identité, auquel vous accordez seulement les privilèges que votre application doit exécuter.</span><span class="sxs-lookup"><span data-stu-id="e0744-103">Service principals provide a way to create a non-interactive account associated with your identity to which you grant only the privileges your app needs to run.</span></span>

<span data-ttu-id="e0744-104">Tout d’abord, connectez-vous à [Azure Cloud Shell](https://shell.azure.com/bash).</span><span class="sxs-lookup"><span data-stu-id="e0744-104">First, login to [Azure Cloud Shell](https://shell.azure.com/bash).</span></span> <span data-ttu-id="e0744-105">Vérifiez que vous utilisez actuellement l’abonnement dans lequel vous souhaitez que le principal de service soit créé.</span><span class="sxs-lookup"><span data-stu-id="e0744-105">Verify you are currently using the subscription in which you want the service principal created.</span></span> 

```azurecli-interactive
az account show
```

<span data-ttu-id="e0744-106">Les information relatives à votre abonnement sont affichées.</span><span class="sxs-lookup"><span data-stu-id="e0744-106">Your subscription information is displayed.</span></span>

```json
{
  "environmentName": "AzureCloud",
  "id": "15dbcfa8-4b93-4c9a-881c-6189d39f04d4",
  "isDefault": true,
  "name": "my-subscription",
  "state": "Enabled",
  "tenantId": "43413cc1-5886-4711-9804-8cfea3d1c3ee",
  "user": {
    "cloudShellID": true,
    "name": "jane@contoso.com",
    "type": "user"
  }
}
```

<span data-ttu-id="e0744-107">Si vous n’êtes pas connecté au bon abonnement, sélectionnez le bon en saisissant `az account set -s <name or ID of subscription>`.</span><span class="sxs-lookup"><span data-stu-id="e0744-107">If you're not logged into the correct subscription, select the correct one by typing `az account set -s <name or ID of subscription>`.</span></span>

<span data-ttu-id="e0744-108">Créez le principal de service avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="e0744-108">Create the service principal with the following command:</span></span>

```azurecli-interactive
az ad sp create-for-rbac --sdk-auth
```

<span data-ttu-id="e0744-109">Les informations relatives au principal de service sont affichées en tant que JSON.</span><span class="sxs-lookup"><span data-stu-id="e0744-109">The service principal information is displayed as JSON.</span></span>

```json
{
  "clientId": "b52dd125-9272-4b21-9862-0be667bdf6dc",
  "clientSecret": "ebc6e170-72b2-4b6f-9de2-99410964d2d0",
  "subscriptionId": "ffa52f27-be12-4cad-b1ea-c2c241b6cceb",
  "tenantId": "72f988bf-86f1-41af-91ab-2d7cd011db47",
  "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
  "resourceManagerEndpointUrl": "https://management.azure.com/",
  "activeDirectoryGraphResourceId": "https://graph.windows.net/",
  "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
  "galleryEndpointUrl": "https://gallery.azure.com/",
  "managementEndpointUrl": "https://management.core.windows.net/"
}
```

<span data-ttu-id="e0744-110">Copiez et collez la sortie JSON dans un éditeur de texte pour plus tard.</span><span class="sxs-lookup"><span data-stu-id="e0744-110">Copy and paste the JSON output to a text editor for use later.</span></span>
