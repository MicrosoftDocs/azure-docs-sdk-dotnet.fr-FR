---
title: Bibliothèques Azure Media Services pour .NET
description: Référence pour les bibliothèques Azure Media Services pour .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: media-services
ms.openlocfilehash: cbb37d5d80c152ef53dba14c83cf2a2695e6b0f0
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190582"
---
# <a name="azure-media-services-libraries-for-net"></a><span data-ttu-id="fc36f-103">Bibliothèques Azure Media Services pour .NET</span><span class="sxs-lookup"><span data-stu-id="fc36f-103">Azure Media Services libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="fc36f-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="fc36f-104">Overview</span></span>

<span data-ttu-id="fc36f-105">Microsoft Azure Media Services est une plateforme extensible basée sur le cloud qui permet aux développeurs de créer des applications évolutives de gestion et de diffusion de médias.</span><span class="sxs-lookup"><span data-stu-id="fc36f-105">Microsoft Azure Media Services is an extensible cloud-based platform that enables developers to build scalable media management and delivery applications.</span></span> <span data-ttu-id="fc36f-106">Media Services est basé sur les API REST qui permettent de télécharger, stocker, encoder et empaqueter en toute sécurité du contenu vidéo ou audio destiné à être diffusé à la demande ou en direct sur différents clients (par exemple, téléviseurs, PC et appareils mobiles).</span><span class="sxs-lookup"><span data-stu-id="fc36f-106">Media Services is based on REST APIs that enable you to securely upload, store, encode, and package video or audio content for both on-demand and live streaming delivery to various clients (for example, TV, PC, and mobile devices).</span></span> 

<span data-ttu-id="fc36f-107">Pour plus d’informations, consultez les articles [Vue d’ensemble](/azure/media-services/media-services-overview) et [Bien démarrer avec .NET](/azure/media-services/media-services-dotnet-how-to-use).</span><span class="sxs-lookup"><span data-stu-id="fc36f-107">To learn more, see [Overview](/azure/media-services/media-services-overview) and [Getting started with .NET](/azure/media-services/media-services-dotnet-how-to-use).</span></span> 

## <a name="client-library"></a><span data-ttu-id="fc36f-108">Bibliothèque cliente</span><span class="sxs-lookup"><span data-stu-id="fc36f-108">Client library</span></span>

<span data-ttu-id="fc36f-109">La bibliothèque du Kit de développement logiciel (SDK) Azure Media Services pour .NET permet de programmer pour Media Services à l'aide de .NET.</span><span class="sxs-lookup"><span data-stu-id="fc36f-109">The Azure Media Services .NET SDK library enables you to program against Media Services using .NET.</span></span> <span data-ttu-id="fc36f-110">Utilisez la bibliothèque cliente Azure Media Services pour vous connecter, vous authentifier et développer sur API Media Services.</span><span class="sxs-lookup"><span data-stu-id="fc36f-110">Use the Azure Media Services client library to connect, authenticate, and develop against Media Services APIs.</span></span>  

<span data-ttu-id="fc36f-111">Pour plus d’informations, consultez l’article [Prendre en main la diffusion de contenus à la demande à l’aide du Kit de développement logiciel (SDK) .NET](/azure/media-services/media-services-dotnet-get-started).</span><span class="sxs-lookup"><span data-stu-id="fc36f-111">For more information, see [Get started with delivering content on demand using .NET SDK](/azure/media-services/media-services-dotnet-get-started).</span></span>

<span data-ttu-id="fc36f-112">Installez le [package NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="fc36f-112">Install the [NuGet package](https://www.nuget.org/packages/windowsazure.mediaservices) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="fc36f-113">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fc36f-113">Visual Studio Package Manager</span></span>

```powershell
Install-Package windowsazure.mediaservices
```

### <a name="code-example"></a><span data-ttu-id="fc36f-114">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="fc36f-114">Code Example</span></span>

<span data-ttu-id="fc36f-115">Le code suivant utilise le Kit de développement logiciel (SDK) .NET de Media Services pour effectuer les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="fc36f-115">The following code example uses Media Services .NET SDK to perform the following tasks:</span></span>

- <span data-ttu-id="fc36f-116">Création d’une tâche d’encodage.</span><span class="sxs-lookup"><span data-stu-id="fc36f-116">Create an encoding job.</span></span>
- <span data-ttu-id="fc36f-117">Obtention d’une référence à l’encodeur Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="fc36f-117">Get a reference to the Media Encoder Standard encoder.</span></span>
- <span data-ttu-id="fc36f-118">Spécifiez l’utilisation de la présélection Diffusion en continu adaptative.</span><span class="sxs-lookup"><span data-stu-id="fc36f-118">Specify to use the Adaptive Streaming preset.</span></span>
- <span data-ttu-id="fc36f-119">Ajout d’une tâche d’encodage unique.</span><span class="sxs-lookup"><span data-stu-id="fc36f-119">Add a single encoding task to the job.</span></span>
- <span data-ttu-id="fc36f-120">Spécification de l’élément multimédia d’entrée à encoder.</span><span class="sxs-lookup"><span data-stu-id="fc36f-120">Specify the input asset to be encoded.</span></span>
- <span data-ttu-id="fc36f-121">Créez une ressource de sortie destinée à recevoir la ressource encodée.</span><span class="sxs-lookup"><span data-stu-id="fc36f-121">Create an output asset to receive the encoded asset.</span></span>
- <span data-ttu-id="fc36f-122">Envoyez le travail.</span><span class="sxs-lookup"><span data-stu-id="fc36f-122">Submit the job.</span></span>


```csharp
/* Include this 'using' directive:
using Microsoft.WindowsAzure.MediaServices.Client;
*/

CloudMediaContext context = new CloudMediaContext(new Uri(mediaServiceRESTAPIEndpoint), tokenProvider);

// Get an uploaded asset.
IAsset asset = context.Assets.FirstOrDefault();

// Encode and generate the output using the "Adaptive Streaming" preset.
// Declare a new job.
IJob job = context.Jobs.Create("Media Encoder Standard Job");
// Get a media processor reference, and pass to it the name of the 
// processor to use for the specific task.
IMediaProcessor processor = context.MediaProcessors.Where(p => p.Name == mediaProcessorName)
    .ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();
if (processor == null) 
{
    throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));
}

// Create a task with the encoding details, using a string preset.
// In this case "Adaptive Streaming" preset is used.
ITask task = job.Tasks.AddNew("My encoding task", processor, "Adaptive Streaming", TaskOptions.None);

// Specify the input asset to be encoded.
task.InputAssets.Add(asset);
// Add an output asset to contain the results of the job. 
// This output is specified as AssetCreationOptions.None, which 
// means the output asset is not encrypted. 
task.OutputAssets.AddNew("Output asset", AssetCreationOptions.None);

job.Submit();
job.GetExecutionProgressTask(CancellationToken.None).Wait();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="fc36f-123">Explorer les API clientes</span><span class="sxs-lookup"><span data-stu-id="fc36f-123">Explore the client APIs</span></span>](/dotnet/api/overview/azure/mediaservices/client)

## <a name="samples"></a><span data-ttu-id="fc36f-124">Exemples</span><span class="sxs-lookup"><span data-stu-id="fc36f-124">Samples</span></span>

- [<span data-ttu-id="fc36f-125">Diffuser en continu votre contenu HLS protégé avec Apple FairPlay</span><span class="sxs-lookup"><span data-stu-id="fc36f-125">Stream your HLS content Protected with Apple FairPlay</span></span>](https://azure.microsoft.com/resources/samples/media-services-dotnet-dynamic-encryption-with-fairplay/)
- [<span data-ttu-id="fc36f-126">Copier des objets blob dans une ressource Azure Media Services à l’aide des extensions du kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="fc36f-126">Copy blob into an Azure Media Services asset using .NET SDK Extensions</span></span>](https://azure.microsoft.com/resources/samples/media-services-dotnet-copy-blob-into-asset/)
- [<span data-ttu-id="fc36f-127">Encoder et diffuser un flux de métriques temps réel avec Azure Media Services à l’aide du Kit de développement logiciel .NET</span><span class="sxs-lookup"><span data-stu-id="fc36f-127">Encode and Deliver a Live Stream with Azure Media Services using .NET SDK</span></span>](https://azure.microsoft.com/resources/samples/media-services-dotnet-encode-live-stream-with-ams-clear/)

<span data-ttu-id="fc36f-128">Affichez la [liste complète](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=media-services) des échantillons Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="fc36f-128">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=media-services) of Azure Media Services samples.</span></span>


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
