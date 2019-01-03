---
title: Bibliothèques Azure IoT pour .NET
description: Référence pour les bibliothèques Azure IoT pour .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: iot-hub
ms.openlocfilehash: 667663c5f5e3452fcc5ec0c4f3ded997370c5852
ms.sourcegitcommit: 7f1a1bf275d8489f8df266b746baa33d66fcb2c8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/21/2018
ms.locfileid: "53737074"
---
# <a name="azure-iot-libraries-for-net"></a><span data-ttu-id="7caf4-103">Bibliothèques Azure IoT pour .NET</span><span class="sxs-lookup"><span data-stu-id="7caf4-103">Azure IoT libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="7caf4-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="7caf4-104">Overview</span></span>

<span data-ttu-id="7caf4-105">[Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/) est un service entièrement géré qui permet des communications bidirectionnelles fiables et sécurisées entre des millions d’appareils et un serveur principal de solution.</span><span class="sxs-lookup"><span data-stu-id="7caf4-105">[Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/) is a fully managed service that enables reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span>

<span data-ttu-id="7caf4-106">Les appareils et les sources de données d’une solution IoT comprennent aussi bien un détecteur simple connecté au réseau qu’un puissant appareil informatique autonome.</span><span class="sxs-lookup"><span data-stu-id="7caf4-106">Devices and data sources in an IoT solution can range from a simple network-connected sensor to a powerful, standalone computing device.</span></span> <span data-ttu-id="7caf4-107">La capabilité de processus, la mémoire, la bande passante de communication et la prise en charge du protocole de communication des appareils peuvent être limitées.</span><span class="sxs-lookup"><span data-stu-id="7caf4-107">Devices may have limited processing capability, memory, communication bandwidth, and communication protocol support.</span></span> <span data-ttu-id="7caf4-108">Les [Kits de développement logiciel (SDK) des appareils](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-sdks) IoT vous permettent d’implémenter des applications clientes à un large éventail d’appareils et d’applications back-end.</span><span class="sxs-lookup"><span data-stu-id="7caf4-108">The IoT [device SDKs](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-sdks) enable you to implement client applications for a wide variety of devices and back-end applications.</span></span>

<span data-ttu-id="7caf4-109">Le Kit de développement logiciel (SDK) des appareils pour .NET facilite la génération d’appareils fonctionnant avec .NET capables de se connecter à IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="7caf4-109">The device SDK for .NET facilitates building devices running .NET that connect to Azure IoT Hub.</span></span>

<span data-ttu-id="7caf4-110">Le Kit de développement logiciel (SDK) des services pour .NET facilite la génération d’applications back-end fonctionnant avec .NET capables de gérer et de permettre le contrôle des appareils à partir du cloud.</span><span class="sxs-lookup"><span data-stu-id="7caf4-110">The service SDK for .NET facilitates building back-end applications using .NET that manage and allow controlling devices from the Cloud.</span></span>

<span data-ttu-id="7caf4-111">[En savoir plus sur Azure IoT](https://docs.microsoft.com/azure/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="7caf4-111">[Learn more about Azure IoT](https://docs.microsoft.com/azure/iot-hub/).</span></span>


## <a name="client-library"></a><span data-ttu-id="7caf4-112">Bibliothèque cliente</span><span class="sxs-lookup"><span data-stu-id="7caf4-112">Client library</span></span>

<span data-ttu-id="7caf4-113">Utilisez le client des appareils IoT .NET pour vous connecter et envoyer des messages à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="7caf4-113">Use the .NET IoT devices client to connect and send messages to your IoT Hub.</span></span>

<span data-ttu-id="7caf4-114">Installez le [package NuGet]( https://www.nuget.org/packages/Microsoft.Azure.Devices.Client) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="7caf4-114">Install the [NuGet package]( https://www.nuget.org/packages/Microsoft.Azure.Devices.Client) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="7caf4-115">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7caf4-115">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Devices.Client
```

```bash
dotnet add package Microsoft.Azure.Devices.Client
```
### <a name="code-examples"></a><span data-ttu-id="7caf4-116">Exemples de code</span><span class="sxs-lookup"><span data-stu-id="7caf4-116">Code Examples</span></span> 

<span data-ttu-id="7caf4-117">Cet exemple se connecte à IoT Hub et envoie un message par seconde.</span><span class="sxs-lookup"><span data-stu-id="7caf4-117">This example connects to the IoT Hub and sends one message per second.</span></span>

```csharp
string deviceKey = "<deviceKey>";
string deviceId = "<deviceId>";
string iotHubHostName = "<IoTHubHostname>";
var deviceAuthentication = new DeviceAuthenticationWithRegistrySymmetricKey(deviceId, deviceKey);

DeviceClient deviceClient = DeviceClient.Create(iotHubHostName, deviceAuthentication, TransportType.Mqtt);

while (true)
{
    double currentTemperature = 20 + Rand.NextDouble() * 15;
    double currentHumidity = 60 + Rand.NextDouble() * 20;

    var telemetryDataPoint = new
    {
        messageId = _messageId++,
        deviceId = deviceId,
        temperature = currentTemperature,
        humidity = currentHumidity
    };
    string messageString = JsonConvert.SerializeObject(telemetryDataPoint);
    Message message = new Message(Encoding.ASCII.GetBytes(messageString));
    message.Properties.Add("temperatureAlert", (currentTemperature > 30) ? "true" : "false");

    await deviceClient.SendEventAsync(message);
    Console.WriteLine("{0} > Sending message: {1}", DateTime.Now, messageString);

    await Task.Delay(1000);
}
```


> [!div class="nextstepaction"]
> [<span data-ttu-id="7caf4-118">Explorer les API clientes</span><span class="sxs-lookup"><span data-stu-id="7caf4-118">Explore the client APIs</span></span>](/dotnet/api/overview/azure/iot/client)

## <a name="samples"></a><span data-ttu-id="7caf4-119">Exemples</span><span class="sxs-lookup"><span data-stu-id="7caf4-119">Samples</span></span>

- [<span data-ttu-id="7caf4-120">Service web générique à scénario Event Hub</span><span class="sxs-lookup"><span data-stu-id="7caf4-120">Generic Web Service to Event Hub scenario</span></span>](https://azure.microsoft.com/resources/samples/event-hubs-dotnet-importfromweb/)

<span data-ttu-id="7caf4-121">Afficher la [liste complète](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=iot-hub) de Azure IoT Upsamples.</span><span class="sxs-lookup"><span data-stu-id="7caf4-121">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=iot-hub) of Azure IoT Upsamples.</span></span>

<span data-ttu-id="7caf4-122">Consultez le [Guide du développeur IoT Hub](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide) pour obtenir d’autres conseils.</span><span class="sxs-lookup"><span data-stu-id="7caf4-122">View the [Azure IoT Hub developer guide](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide) for more guidance.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
