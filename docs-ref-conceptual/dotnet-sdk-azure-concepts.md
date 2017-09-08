---
title: "Concepts et modèles d’utilisation des bibliothèques de gestion Azure pour .NET"
description: 
keywords: "Azure, .NET, Kit de développement logiciel (SDK), API, modèles, concepts, fluent, journalisation"
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
ms.openlocfilehash: b2e6849f06c36de18471e55c468e984f4205f646
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2017
---
# <a name="azure-management-library-for-net-fluent-concepts"></a>Concepts Fluent des bibliothèques de gestion Azure pour .NET

Cet article vous aide à comprendre comment utiliser efficacement l’interface Fluent dans les bibliothèques de gestion Azure pour .NET.

## <a name="building-resources-using-a-fluent-interface"></a>Générer des ressources à l’aide d’une interface Fluent

Une interface Fluent constitue une forme définie du modèle de générateur qui crée des objets via une chaîne de méthode qui applique la bonne configuration d’une ressource. Par exemple, l’objet Azure du point d’entrée est créé à l’aide d’une interface Fluent :

```csharp
var azure = Azure
    .Configure()
    .Authenticate(credentials)
    .WithDefaultSubscription();
```

## <a name="resource-collections"></a>Collections de ressources

L’objet `Microsoft.Azure.Management.Fluent.Azure` ci-dessous correspond au point d’entrée de toute création de ressources dans les bibliothèques de gestion Fluent. Sélectionnez le type de ressources à utiliser avec les collections de ressources dans l’objet `Azure`. Par exemple, pour SQL Database :

```csharp
var sql = azure.SqlServers.Define(sqlServerName)
    .WithRegion(Region.USEast)
    .WithNewResourceGroup(rgName)
    .WithAdministratorLogin(administratorLogin)
    .WithAdministratorPassword(administratorPassword)
    .Create();
```

Comme indiqué ci-dessus, la plupart des « conversations » Fluent que vous entretenez avec l’API commencent par la sélection de la collection de ressources appropriée pour les ressources Azure que vous avez besoin d’utiliser.  Intellisense dans Visual Studio vous guide ensuite dans la conversation. 

![Génération d’une conversation Fluent par un GIF d’Intellisense dans Visual Studio](media/dotnet-sdk-azure-concepts/vs-fluent.gif)   

## <a name="lists-and-iterations"></a>Listes et itérations

Chaque collection de ressources possède une méthode `List()` qui renvoie chaque instance de cette ressource dans votre abonnement actuel. Par exemple,la méthode `Azure.SqlServers.List()` renvoie tous les serveurs SQL dans l’abonnement.

Utilisez la méthode `ListByResourceGroup()` pour étendre la liste renvoyée à un [groupe de ressources Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups) spécifique.  

Itérez sur la collection renvoyée, comme vous le feriez pour un élément normal `List<T>` :

```csharp
var vmList = azure.VirtualMachines.List();
foreach(var vm in vmList)
{
    Console.WriteLine("VM Name: {0}", vm.Name);
}
```   

## <a name="actionable-verbs"></a>Verbes actionnables

Les méthodes de collection de ressources dont les noms contiennent des verbes prennent effet immédiatement dans Azure. Ces méthodes fonctionnent de façon synchrone et empêchent l’exécution dans le thread actuel jusqu’à ce qu’elles se terminent. 

| Verbe   |  Exemple d’utilisation |
|--------|---------------|
| Créer | `azure.VirtualMachines.Create(listOfVMCreatables)` |
| Appliquer  | `virtualMachineScaleSet.Update().WithCapacity(6).Apply()` |
| Supprimer | `azure.Disks.DeleteById(id)` | 
| Énumérer   | `azure.SqlServers.List()` | 
| Obtenir    | `var vm  = azure.VirtualMachines.GetByResourceGroup(group, vmName)` |

>[!NOTE]
> `Define()` et `Update()` sont des verbes mais ne bloquent pas, sauf s’ils sont suivis par les verbes `Create()` ou `Apply()`.
 
Des objets de ressources spécifiques disposent de verbes qui modifient l’état de la ressource dans Azure. Par exemple :

```csharp
var vmToRestart = azure.VirtualMachines.GetById(id);
vmToRestart.Restart();
```

La plupart des méthodes décrites dans cette section ont aussi une version asynchrone, désignée par le suffixe `Async`.

```csharp
Task restartTask = azure.VirtualMachines.GetById(id).RestartAsync();
```

## <a name="lazy-resource-creation"></a>Création de ressources différées

La création de ressources Azure peut constituer un défi lorsqu’une nouvelle ressource dépend d’une autre ressource qui n’existe pas. Exemple : la réservation d’une adresse IP publique et la configuration d’un disque lors de la création d’une machine virtuelle. Vous ne souhaitez pas vérifier lors de l’étape de réservation d’adresse ni de la création du disque, vous souhaitez juste configurer la machine virtuelle avec ces ressources.

Utilisez des objets « creatable » pour définir les ressources Azure à utiliser dans votre code, mais créez-les seulement lorsque vous en avez besoin dans Azure. Le code écrit avec des objets « creatable » permet de décharger la création de ressources dans l’environnement Azure vers l’API de gestion, ce qui renforce les performances. 

Générez des objets « creatable » via le verbe de collection de ressources `Define()`, sans avoir à utiliser le verbe `Create()` :

```csharp
// Init a creatable Public IP Address
var publicIpAddressCreatable = azure.PublicIPAddresses.Define("publicIPAddressName")
    .WithRegion(Region.USEast)
    .WithNewResourceGroup(rgName);
```

La ressource Azure définie par l’objet « creatable » n’existe pas encore dans votre abonnement. Un objet « creatable » est une représentation locale d’une ressource créée par l’API de gestion lorsque nécessaire (quand le verbe `.Create()` est utilisé). Utilisez cet objet « creatable » dans la définition d’autres ressources Azure nécessitant cette ressource. 

```csharp
// Init a creatable VM using the creatable Public IP Address
var vmCreatable = azure.VirtualMachines.Define("creatableVM")
    // ...
    .withNewPrimaryPublicIPAddress(publicIPAddressCreatable)
    // ...
```

Créez les ressources dans votre abonnement Azure à l’aide de la méthode `Create()` de la collection de ressources. 

```csharp
// Create the VM and its Public IP Address
var virtualMachine = azure.VirtualMachines.Create(vmCreatable);
```

L’utilisation de la méthode `Create()` sur un objet « creatable » renvoie un objet `ICreatedResources` et non un objet de ressource unique.  L’objet `CreatedRelatedResource` vous permet d’accéder à toutes les ressources créées par l’appel `Create()`, pas uniquement au type de la collection de ressources. Pour accéder à l’adresse IP publique créée dans Azure pour la machine virtuelle créée dans l’exemple ci-dessus :

```csharp
var pip = virtualMachine.CreatedRelatedResource(publicIPAddressCreatable.Key()) as PublicIPAddress;;
```    

## <a name="exception-handling"></a>Gestion des exceptions

L’API de gestion définit les classes d’exceptions qui étendent `Microsoft.Rest.RestException`. Interceptez des exceptions générées par l’API de gestion avec un bloc `catch (RestException exception)` après l’instruction pertinente `try`.

## <a name="logs-and-tracing"></a>Journaux et suivi

La journalisation dans les bibliothèques de gestion Fluent Azure pour .NET exploite le suivi sous-jacent du client du service [AutoRest](https://github.com/Azure/AutoRest).

Créez une classe qui implémente `Microsoft.Rest.IServiceClientTracingInterceptor`.  Cette classe est chargée d’intercepter les messages de journaux et de les transmettre au moyen de journalisation que vous utilisez.  Dans cet exemple, nous écrivons simplement des messages à la console, mais vous pouvez tout aussi bien les transmettre à Log4Net, `Microsoft.Extensions.Logging` ou à n’importe quel autre framework de journalisation.

```csharp
class ConsoleTracer : IServiceClientTracingInterceptor
{
    public void Information(string message)
    {
        Console.WriteLine(message);
    }

    public void TraceError(string invocationId, Exception exception)
    {
        Console.WriteLine("Exception in {0}: {1}", invocationId, exception);
    }

    public void ReceiveResponse(string invocationId, HttpResponseMessage response) { }

    public void SendRequest(string invocationId, HttpRequestMessage request) { }

    public void Configuration(string source, string name, string value) { }

    public void EnterMethod(string invocationId, object instance, string method, IDictionary<string, object> parameters) { }

    public void ExitMethod(string invocationId, object returnValue) { }
}
```

Avant de créer l’objet `Microsoft.Azure.Management.Fluent.Azure`, lancez le `IServiceClientTracingInterceptor` que vous avez créé ci-dessus en appelant la méthode `ServiceClientTracing.AddTracingInterceptor()` et en donnant la valeur *true* à l’élément `ServiceClientTracing.IsEnabled`.  Lorsque vous créez l’objet `Azure`, incluez les méthodes `.WithDelegatingHandler()` et `.WithLogLevel()` pour connecter le client au suivi du client de service AutoRest.

```csharp
ServiceClientTracing.AddTracingInterceptor(new ConsoleTracer());
ServiceClientTracing.IsEnabled = true;

var azure = Azure
    .Configure()
    .WithDelegatingHandler(new HttpLoggingDelegatingHandler())
    .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
    .Authenticate(credentials)
    .WithDefaultSubscription();
```

Les niveaux de consignation `HttpLoggingDelegatingHandler` sont définis comme suit :

| Niveau de trace | Journalisation activée 
| ------------ | ---------------
| HttpLoggingDelegatingHandler.Level.None | Aucune sortie
| HttpLoggingDelegatingHandler.Level.Basic | Consigne les URL vers des appels REST sous-jacentes, des codes de réponses et des temps
| HttpLoggingDelegatingHandler.Level.Body | Fonctions du niveau de consignation BASIC, ajoutées à des corps de demande et de réponse aux appels REST
| HttpLoggingDelegatingHandler.Level.Headers | Fonctions du niveau de consignation BASIC, ajoutées à des en-têtes de demande et de réponse aux appels REST
| HttpLoggingDelegatingHandler.Level.BodyAndHeaders | Fonction des niveaux de consignation BODY et HEADERS
