---
title: "Bibliothèques Azure Media Services pour .NET"
description: "Référence pour les bibliothèques Azure Media Services pour .NET"
keywords: Azure, .NET, SDK, API, Media Services
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/21/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: ee852258819e75867888f4a5fa1cbd72c7f91685
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2017
---
# <a name="azure-media-services-libraries-for-net"></a>Bibliothèques Azure Media Services pour .NET

## <a name="overview"></a>Vue d'ensemble

Microsoft Azure Media Services est une plateforme extensible basée sur le cloud qui permet aux développeurs de créer des applications évolutives de gestion et de diffusion de médias. Media Services est basé sur les API REST qui permettent de télécharger, stocker, encoder et empaqueter en toute sécurité du contenu vidéo ou audio destiné à être diffusé à la demande ou en direct sur différents clients (par exemple, téléviseurs, PC et appareils mobiles). 

Pour plus d’informations, consultez les articles [Vue d’ensemble](/azure/media-services/media-services-overview) et [Bien démarrer avec .NET](/azure/media-services/media-services-dotnet-how-to-use). 

## <a name="client-library"></a>Bibliothèque cliente

La bibliothèque du Kit de développement logiciel (SDK) Azure Media Services pour .NET permet de programmer pour Media Services à l'aide de .NET. Utilisez la bibliothèque cliente Azure Media Services pour vous connecter, vous authentifier et développer sur API Media Services.  

Pour plus d’informations, consultez l’article [Prendre en main la diffusion de contenus à la demande à l’aide du Kit de développement logiciel (SDK) .NET](/azure/media-services/media-services-dotnet-get-started).

Installez le [package NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package windowsazure.mediaservices
```

### <a name="code-example"></a>Exemple de code

Le code suivant utilise le Kit de développement logiciel (SDK) .NET de Media Services pour effectuer les tâches suivantes :

- Création d’une tâche d’encodage.
- Obtention d’une référence à l’encodeur Media Encoder Standard.
- Spécifiez l’utilisation de la présélection Diffusion en continu adaptative.
- Ajout d’une tâche d’encodage unique.
- Spécification de l’élément multimédia d’entrée à encoder.
- Créez une ressource de sortie destinée à recevoir la ressource encodée.
- Envoyez le travail.


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
> [Explorer les API client](/dotnet/api/overview/azure/mediaservices/client)

## <a name="samples"></a>Exemples

- [Diffuser en continu votre contenu HLS protégé avec Apple FairPlay](https://azure.microsoft.com/resources/samples/media-services-dotnet-dynamic-encryption-with-fairplay/)
- [Copier des objets blob dans une ressource Azure Media Services à l’aide des extensions du kit de développement logiciel (SDK) .NET](https://azure.microsoft.com/resources/samples/media-services-dotnet-copy-blob-into-asset/)
- [Encoder et diffuser un flux de métriques temps réel avec Azure Media Services à l’aide du Kit de développement logiciel .NET](https://azure.microsoft.com/resources/samples/media-services-dotnet-encode-live-stream-with-ams-clear/)

Affichez la [liste complète](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=media-services) des échantillons Azure Media Services.


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
