---
title: Concepts et modèles d’utilisation des bibliothèques de gestion Azure pour .NET
description: ''
keywords: Azure, .NET, Kit de développement logiciel (SDK), API, modèles, concepts, fluent, journalisation
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter
ms.openlocfilehash: b817216e114e5ab3ff22c1c5adb0f892c7874147
ms.sourcegitcommit: 1c2e1fd031ad012d6888fcde3cd325f7e8e49e0f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/09/2018
ms.locfileid: "29752861"
---
# <a name="azure-management-library-for-net-fluent-concepts"></a><span data-ttu-id="1b4ae-103">Concepts Fluent des bibliothèques de gestion Azure pour .NET</span><span class="sxs-lookup"><span data-stu-id="1b4ae-103">Azure management library for .NET fluent concepts</span></span>

<span data-ttu-id="1b4ae-104">Cet article vous aide à comprendre comment utiliser efficacement l’interface Fluent dans les bibliothèques de gestion Azure pour .NET.</span><span class="sxs-lookup"><span data-stu-id="1b4ae-104">This article will help you understand how to effectively use the fluent interface in the Azure management libraries for .NET.</span></span>

## <a name="building-resources-using-a-fluent-interface"></a><span data-ttu-id="1b4ae-105">Générer des ressources à l’aide d’une interface Fluent</span><span class="sxs-lookup"><span data-stu-id="1b4ae-105">Building resources using a fluent interface</span></span>

<span data-ttu-id="1b4ae-106">Une interface Fluent constitue une forme définie du modèle de générateur qui crée des objets via une chaîne de méthode qui applique la bonne configuration d’une ressource.</span><span class="sxs-lookup"><span data-stu-id="1b4ae-106">A fluent interface is a specific form of the builder pattern that creates objects through a method chain that enforces correct configuration of a resource.</span></span> <span data-ttu-id="1b4ae-107">Par exemple, l’objet Azure du point d’entrée est créé à l’aide d’une interface Fluent :</span><span class="sxs-lookup"><span data-stu-id="1b4ae-107">For example, the entry-point Azure object is created using a fluent interface:</span></span>

```csharp
var azure = Azure
    .Configure()
    .Authenticate(credentials)
    .WithDefaultSubscription();
```

## <a name="resource-collections"></a><span data-ttu-id="1b4ae-108">Collections de ressources</span><span class="sxs-lookup"><span data-stu-id="1b4ae-108">Resource collections</span></span>

<span data-ttu-id="1b4ae-109">L’objet `Microsoft.Azure.Management.Fluent.Azure` ci-dessous correspond au point d’entrée de toute création de ressources dans les bibliothèques de gestion Fluent.</span><span class="sxs-lookup"><span data-stu-id="1b4ae-109">The `Microsoft.Azure.Management.Fluent.Azure` object shown above is the entry point for all resource creation in the fluent management libraries.</span></span> <span data-ttu-id="1b4ae-110">Sélectionnez le type de ressources à utiliser avec les collections de ressources dans l’objet `Azure`.</span><span class="sxs-lookup"><span data-stu-id="1b4ae-110">Select which type of resources to work with using the resource collections in the `Azure` object.</span></span> <span data-ttu-id="1b4ae-111">Par exemple, pour SQL Database :</span><span class="sxs-lookup"><span data-stu-id="1b4ae-111">For example, for SQL Database:</span></span>

```csharp
var sql = azure.SqlServers.Define(sqlServerName)
    .WithRegion(Region.USEast)
    .WithNewResourceGroup(rgName)
    .WithAdministratorLogin(administratorLogin)
    .WithAdministratorPassword(administratorPassword)
    .Create();
```

<span data-ttu-id="1b4ae-112">Comme indiqué ci-dessus, la plupart des « conversations » Fluent que vous entretenez avec l’API commencent par la sélection de la collection de ressources appropriée pour les ressources Azure que vous avez besoin d’utiliser.</span><span class="sxs-lookup"><span data-stu-id="1b4ae-112">As seen above, most fluent "conversations" you have with the API start with selecting the appropriate resource collection for the Azure resources you need to work with.</span></span>  <span data-ttu-id="1b4ae-113">Intellisense dans Visual Studio vous guide ensuite dans la conversation.</span><span class="sxs-lookup"><span data-stu-id="1b4ae-113">Intellisense in Visual Studio then guides you through the conversation.</span></span> 

![Génération d’une conversation Fluent par un GIF d’Intellisense dans Visual Studio](media/dotnet-sdk-azure-concepts/vs-fluent.gif)   

## <a name="lists-and-iterations"></a><span data-ttu-id="1b4ae-115">Listes et itérations</span><span class="sxs-lookup"><span data-stu-id="1b4ae-115">Lists and iterations</span></span>

<span data-ttu-id="1b4ae-116">Chaque collection de ressources possède une méthode `List()` qui renvoie chaque instance de cette ressource dans votre abonnement actuel.</span><span class="sxs-lookup"><span data-stu-id="1b4ae-116">Every resource collection has a `List()` method to return every instance of that resource in your current subscription.</span></span> <span data-ttu-id="1b4ae-117">Par exemple,la méthode `Azure.SqlServers.List()` renvoie tous les serveurs SQL dans l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="1b4ae-117">For example, `Azure.SqlServers.List()` returns all SQL servers in the subscription.</span></span>

<span data-ttu-id="1b4ae-118">Utilisez la méthode `ListByResourceGroup()` pour étendre la liste renvoyée à un [groupe de ressources Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups) spécifique.</span><span class="sxs-lookup"><span data-stu-id="1b4ae-118">Use the `ListByResourceGroup()` method to scope the returned List to a specific [Azure resource group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups).</span></span>  

<span data-ttu-id="1b4ae-119">Itérez sur la collection renvoyée, comme vous le feriez pour un élément normal `List<T>` :</span><span class="sxs-lookup"><span data-stu-id="1b4ae-119">Iterate over the returned collection just as you would a normal `List<T>`:</span></span>

```csharp
var vmList = azure.VirtualMachines.List();
foreach(var vm in vmList)
{
    Console.WriteLine("VM Name: {0}", vm.Name);
}
```   

## <a name="actionable-verbs"></a><span data-ttu-id="1b4ae-120">Verbes actionnables</span><span class="sxs-lookup"><span data-stu-id="1b4ae-120">Actionable verbs</span></span>

<span data-ttu-id="1b4ae-121">Les méthodes de collection de ressources dont les noms contiennent des verbes prennent effet immédiatement dans Azure.</span><span class="sxs-lookup"><span data-stu-id="1b4ae-121">Resource collection methods with verbs in their names take immediate action in Azure.</span></span> <span data-ttu-id="1b4ae-122">Ces méthodes fonctionnent de façon synchrone et empêchent l’exécution dans le thread actuel jusqu’à ce qu’elles se terminent.</span><span class="sxs-lookup"><span data-stu-id="1b4ae-122">These methods work synchronously and block execution in the current thread until they complete.</span></span> 

| <span data-ttu-id="1b4ae-123">Verbe</span><span class="sxs-lookup"><span data-stu-id="1b4ae-123">Verb</span></span>   |  <span data-ttu-id="1b4ae-124">Exemple d’utilisation</span><span class="sxs-lookup"><span data-stu-id="1b4ae-124">Sample usage</span></span> |
|--------|---------------|
| <span data-ttu-id="1b4ae-125">Créer</span><span class="sxs-lookup"><span data-stu-id="1b4ae-125">Create</span></span> | `azure.VirtualMachines.Create(listOfVMCreatables)` |
| <span data-ttu-id="1b4ae-126">Appliquer</span><span class="sxs-lookup"><span data-stu-id="1b4ae-126">Apply</span></span>  | `virtualMachineScaleSet.Update().WithCapacity(6).Apply()` |
| <span data-ttu-id="1b4ae-127">Supprimer</span><span class="sxs-lookup"><span data-stu-id="1b4ae-127">Delete</span></span> | `azure.Disks.DeleteById(id)` | 
| <span data-ttu-id="1b4ae-128">Liste</span><span class="sxs-lookup"><span data-stu-id="1b4ae-128">List</span></span>   | `azure.SqlServers.List()` | 
| <span data-ttu-id="1b4ae-129">Obtenir</span><span class="sxs-lookup"><span data-stu-id="1b4ae-129">Get</span></span>    | `var vm  = azure.VirtualMachines.GetByResourceGroup(group, vmName)` |

>[!NOTE]
> <span data-ttu-id="1b4ae-130">`Define()` et `Update()` sont des verbes mais ne bloquent pas, sauf s’ils sont suivis par les verbes `Create()` ou `Apply()`.</span><span class="sxs-lookup"><span data-stu-id="1b4ae-130">`Define()` and `Update()` are verbs but do not block unless followed by a `Create()` or `Apply()`.</span></span>
 
<span data-ttu-id="1b4ae-131">Des objets de ressources spécifiques disposent de verbes qui modifient l’état de la ressource dans Azure.</span><span class="sxs-lookup"><span data-stu-id="1b4ae-131">Specific resource objects have verbs that change the state of the resource in Azure.</span></span> <span data-ttu-id="1b4ae-132">Par exemple : </span><span class="sxs-lookup"><span data-stu-id="1b4ae-132">For example:</span></span>

```csharp
var vmToRestart = azure.VirtualMachines.GetById(id);
vmToRestart.Restart();
```

<span data-ttu-id="1b4ae-133">La plupart des méthodes décrites dans cette section ont aussi une version asynchrone, désignée par le suffixe `Async`.</span><span class="sxs-lookup"><span data-stu-id="1b4ae-133">Most of the methods described in this section have an asynchronous version as well, denoted by the suffix `Async`.</span></span>

```csharp
Task restartTask = azure.VirtualMachines.GetById(id).RestartAsync();
```

## <a name="lazy-resource-creation"></a><span data-ttu-id="1b4ae-134">Création de ressources différées</span><span class="sxs-lookup"><span data-stu-id="1b4ae-134">Lazy resource creation</span></span>

<span data-ttu-id="1b4ae-135">La création de ressources Azure peut constituer un défi lorsqu’une nouvelle ressource dépend d’une autre ressource qui n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="1b4ae-135">A challenge when creating Azure resources arises when a new resource depends on another resource that doesn't yet exist.</span></span> <span data-ttu-id="1b4ae-136">Exemple : la réservation d’une adresse IP publique et la configuration d’un disque lors de la création d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1b4ae-136">An example is reserving a public IP address and setting up a disk when creating a new virtual machine.</span></span> <span data-ttu-id="1b4ae-137">Vous ne souhaitez pas vérifier lors de l’étape de réservation d’adresse ni de la création du disque, vous souhaitez juste configurer la machine virtuelle avec ces ressources.</span><span class="sxs-lookup"><span data-stu-id="1b4ae-137">You don't want to verify reserving the address or the creating the disk, you just want to configure the virtual machine with those resources.</span></span>

<span data-ttu-id="1b4ae-138">Utilisez des objets « creatable » pour définir les ressources Azure à utiliser dans votre code, mais créez-les seulement lorsque vous en avez besoin dans Azure.</span><span class="sxs-lookup"><span data-stu-id="1b4ae-138">Use creatable objects to define Azure resources for use in your code but only create them when needed in Azure.</span></span> <span data-ttu-id="1b4ae-139">Le code écrit avec des objets « creatable » permet de décharger la création de ressources dans l’environnement Azure vers l’API de gestion, ce qui renforce les performances.</span><span class="sxs-lookup"><span data-stu-id="1b4ae-139">Code written with creatable objects offloads resource creation in the Azure environment to the management API, boosting performance.</span></span> 

<span data-ttu-id="1b4ae-140">Générez des objets « creatable » via le verbe de collection de ressources `Define()`, sans avoir à utiliser le verbe `Create()` :</span><span class="sxs-lookup"><span data-stu-id="1b4ae-140">Generate creatable objects through the resource collections' `Define()` verb without a `Create()` verb:</span></span>

```csharp
// Init a creatable Public IP Address
var publicIpAddressCreatable = azure.PublicIPAddresses.Define("publicIPAddressName")
    .WithRegion(Region.USEast)
    .WithNewResourceGroup(rgName);
```

<span data-ttu-id="1b4ae-141">La ressource Azure définie par l’objet « creatable » n’existe pas encore dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="1b4ae-141">The Azure resource defined by the creatable object does not yet exist in your subscription.</span></span> <span data-ttu-id="1b4ae-142">Un objet « creatable » est une représentation locale d’une ressource créée par l’API de gestion lorsque nécessaire (quand le verbe `.Create()` est utilisé).</span><span class="sxs-lookup"><span data-stu-id="1b4ae-142">A creatable object is a local representation of a resource that the management API will create when it's needed (when `.Create()` is called).</span></span> <span data-ttu-id="1b4ae-143">Utilisez cet objet « creatable » dans la définition d’autres ressources Azure nécessitant cette ressource.</span><span class="sxs-lookup"><span data-stu-id="1b4ae-143">Use this creatable object in the definition of other Azure resources that need this resource.</span></span> 

```csharp
// Init a creatable VM using the creatable Public IP Address
var vmCreatable = azure.VirtualMachines.Define("creatableVM")
    // ...
    .withNewPrimaryPublicIPAddress(publicIPAddressCreatable)
    // ...
```

<span data-ttu-id="1b4ae-144">Créez les ressources dans votre abonnement Azure à l’aide de la méthode `Create()` de la collection de ressources.</span><span class="sxs-lookup"><span data-stu-id="1b4ae-144">Create the resources in your Azure subscription using the `Create()` method for the resource collection.</span></span> 

```csharp
// Create the VM and its Public IP Address
var virtualMachine = azure.VirtualMachines.Create(vmCreatable);
```

<span data-ttu-id="1b4ae-145">L’utilisation de la méthode `Create()` sur un objet « creatable » renvoie un objet `ICreatedResources` et non un objet de ressource unique.</span><span class="sxs-lookup"><span data-stu-id="1b4ae-145">Passing creatable objects to `Create()` returns a `ICreatedResources` object instead of a single resource object.</span></span>  <span data-ttu-id="1b4ae-146">L’objet `CreatedRelatedResource` vous permet d’accéder à toutes les ressources créées par l’appel `Create()`, pas uniquement au type de la collection de ressources.</span><span class="sxs-lookup"><span data-stu-id="1b4ae-146">The `CreatedRelatedResource` object lets you access all resources created by the `Create()` call, not just the type from the resource collection.</span></span> <span data-ttu-id="1b4ae-147">Pour accéder à l’adresse IP publique créée dans Azure pour la machine virtuelle créée dans l’exemple ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="1b4ae-147">To access the public IP address created in Azure for the virtual machine created in the above example:</span></span>

```csharp
var pip = virtualMachine.CreatedRelatedResource(publicIPAddressCreatable.Key()) as PublicIPAddress;;
```    

## <a name="exception-handling"></a><span data-ttu-id="1b4ae-148">Gestion des exceptions</span><span class="sxs-lookup"><span data-stu-id="1b4ae-148">Exception handling</span></span>

<span data-ttu-id="1b4ae-149">L’API de gestion définit les classes d’exceptions qui étendent `Microsoft.Rest.RestException`.</span><span class="sxs-lookup"><span data-stu-id="1b4ae-149">The management API defines exception classes that extend `Microsoft.Rest.RestException`.</span></span> <span data-ttu-id="1b4ae-150">Interceptez des exceptions générées par l’API de gestion avec un bloc `catch (RestException exception)` après l’instruction pertinente `try`.</span><span class="sxs-lookup"><span data-stu-id="1b4ae-150">Catch exceptions generated by management API, with a `catch (RestException exception)` block after the relevant `try` statement.</span></span>

## <a name="logs-and-tracing"></a><span data-ttu-id="1b4ae-151">Journaux et suivi</span><span class="sxs-lookup"><span data-stu-id="1b4ae-151">Logs and tracing</span></span>

<span data-ttu-id="1b4ae-152">La journalisation dans les bibliothèques de gestion Fluent Azure pour .NET exploite le suivi sous-jacent du client du service [AutoRest](https://github.com/Azure/AutoRest).</span><span class="sxs-lookup"><span data-stu-id="1b4ae-152">Logging in the fluent Azure management libraries for .NET leverages the underlying [AutoRest](https://github.com/Azure/AutoRest) service client tracing.</span></span>

<span data-ttu-id="1b4ae-153">Créez une classe qui implémente `Microsoft.Rest.IServiceClientTracingInterceptor`.</span><span class="sxs-lookup"><span data-stu-id="1b4ae-153">Create a class that implements `Microsoft.Rest.IServiceClientTracingInterceptor`.</span></span>  <span data-ttu-id="1b4ae-154">Cette classe est chargée d’intercepter les messages de journaux et de les transmettre au moyen de journalisation que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="1b4ae-154">This class will be responsible for intercepting log messages and passing them to whatever logging mechanism you're using.</span></span>  <span data-ttu-id="1b4ae-155">Dans cet exemple, nous écrivons simplement des messages à la console, mais vous pouvez tout aussi bien les transmettre à Log4Net, `Microsoft.Extensions.Logging` ou à n’importe quel autre framework de journalisation.</span><span class="sxs-lookup"><span data-stu-id="1b4ae-155">In this example, we're just writing messages to the console, but you could also pass them to Log4Net, `Microsoft.Extensions.Logging`, or any other logging framework.</span></span>

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

<span data-ttu-id="1b4ae-156">Avant de créer l’objet `Microsoft.Azure.Management.Fluent.Azure`, lancez le `IServiceClientTracingInterceptor` que vous avez créé ci-dessus en appelant la méthode `ServiceClientTracing.AddTracingInterceptor()` et en donnant la valeur *true* à l’élément `ServiceClientTracing.IsEnabled`.</span><span class="sxs-lookup"><span data-stu-id="1b4ae-156">Before creating the `Microsoft.Azure.Management.Fluent.Azure` object, initialize the `IServiceClientTracingInterceptor` you created above by calling `ServiceClientTracing.AddTracingInterceptor()` and set `ServiceClientTracing.IsEnabled` to *true*.</span></span>  <span data-ttu-id="1b4ae-157">Lorsque vous créez l’objet `Azure`, incluez les méthodes `.WithDelegatingHandler()` et `.WithLogLevel()` pour connecter le client au suivi du client de service AutoRest.</span><span class="sxs-lookup"><span data-stu-id="1b4ae-157">When you create the `Azure` object, include the `.WithDelegatingHandler()` and `.WithLogLevel()` methods to wire up the client to AutoRest's service client tracing.</span></span>

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

<span data-ttu-id="1b4ae-158">Les niveaux de consignation `HttpLoggingDelegatingHandler` sont définis comme suit :</span><span class="sxs-lookup"><span data-stu-id="1b4ae-158">The `HttpLoggingDelegatingHandler` log levels are defined as follows:</span></span>

| <span data-ttu-id="1b4ae-159">Niveau de trace</span><span class="sxs-lookup"><span data-stu-id="1b4ae-159">Trace level</span></span> | <span data-ttu-id="1b4ae-160">Journalisation activée</span><span class="sxs-lookup"><span data-stu-id="1b4ae-160">Logging enabled</span></span> 
| ------------ | ---------------
| <span data-ttu-id="1b4ae-161">HttpLoggingDelegatingHandler.Level.None</span><span class="sxs-lookup"><span data-stu-id="1b4ae-161">HttpLoggingDelegatingHandler.Level.None</span></span> | <span data-ttu-id="1b4ae-162">Aucune sortie</span><span class="sxs-lookup"><span data-stu-id="1b4ae-162">No output</span></span>
| <span data-ttu-id="1b4ae-163">HttpLoggingDelegatingHandler.Level.Basic</span><span class="sxs-lookup"><span data-stu-id="1b4ae-163">HttpLoggingDelegatingHandler.Level.Basic</span></span> | <span data-ttu-id="1b4ae-164">Consigne les URL vers des appels REST sous-jacentes, des codes de réponses et des temps</span><span class="sxs-lookup"><span data-stu-id="1b4ae-164">Logs the URLs to underlying REST calls, response codes and times</span></span>
| <span data-ttu-id="1b4ae-165">HttpLoggingDelegatingHandler.Level.Body</span><span class="sxs-lookup"><span data-stu-id="1b4ae-165">HttpLoggingDelegatingHandler.Level.Body</span></span> | <span data-ttu-id="1b4ae-166">Fonctions du niveau de consignation BASIC, ajoutées à des corps de demande et de réponse aux appels REST</span><span class="sxs-lookup"><span data-stu-id="1b4ae-166">Everything in Basic plus request and response bodies for the REST calls</span></span>
| <span data-ttu-id="1b4ae-167">HttpLoggingDelegatingHandler.Level.Headers</span><span class="sxs-lookup"><span data-stu-id="1b4ae-167">HttpLoggingDelegatingHandler.Level.Headers</span></span> | <span data-ttu-id="1b4ae-168">Fonctions du niveau de consignation BASIC, ajoutées à des en-têtes de demande et de réponse aux appels REST</span><span class="sxs-lookup"><span data-stu-id="1b4ae-168">Everything in Basic plus the request and response headers REST calls</span></span>
| <span data-ttu-id="1b4ae-169">HttpLoggingDelegatingHandler.Level.BodyAndHeaders</span><span class="sxs-lookup"><span data-stu-id="1b4ae-169">HttpLoggingDelegatingHandler.Level.BodyAndHeaders</span></span> | <span data-ttu-id="1b4ae-170">Fonction des niveaux de consignation BODY et HEADERS</span><span class="sxs-lookup"><span data-stu-id="1b4ae-170">Everything in both Body and Headers log level</span></span>
