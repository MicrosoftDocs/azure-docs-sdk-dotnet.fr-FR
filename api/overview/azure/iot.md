---
title: Bibliothèques Azure IoT pour .NET
description: Référence pour les bibliothèques Azure IoT pour .NET
keywords: Azure, .NET, SDK, API, IoT
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: iot-hub
ms.custom: devcenter, svc-overview
ms.openlocfilehash: af823e910acedd4f204034b12a31ba61fd53e090
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065269"
---
# <a name="azure-iot-libraries-for-net"></a>Bibliothèques Azure IoT pour .NET

## <a name="overview"></a>Vue d'ensemble

[Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/) est un service entièrement géré qui permet des communications bidirectionnelles fiables et sécurisées entre des millions d’appareils et un serveur principal de solution.

Les appareils et les sources de données d’une solution IoT comprennent aussi bien un détecteur simple connecté au réseau qu’un puissant appareil informatique autonome. La capabilité de processus, la mémoire, la bande passante de communication et la prise en charge du protocole de communication des appareils peuvent être limitées. Les [Kits de développement logiciel (SDK) des appareils](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-sdks) IoT vous permettent d’implémenter des applications clientes à un large éventail d’appareils et d’applications back-end.

Le Kit de développement logiciel (SDK) des appareils pour .NET facilite la génération d’appareils fonctionnant avec .NET capables de se connecter à IoT Hub.

Le Kit de développement logiciel (SDK) des services pour .NET facilite la génération d’applications back-end fonctionnant avec .NET capables de gérer et de permettre le contrôle des appareils à partir du cloud.

[En savoir plus sur Azure IoT](https://docs.microsoft.com/azure/iot-hub/).


## <a name="client-library"></a>Bibliothèque cliente

Utilisez le client des appareils IoT .NET pour vous connecter et envoyer des messages à votre IoT Hub.

Installez le [package NuGet]( https://www.nuget.org/packages/Microsoft.Azure.Devices.Client) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Microsoft.Azure.Devices.Client
```

```bash
dotnet add package Microsoft.Azure.Devices.Client
```
### <a name="code-examples"></a>Exemples de code 

Cet exemple se connecte à IoT Hub et envoie un message par seconde.

```csharp
string deviceKey = "<deviceKey>";
string deviceId = "<deviceId>";
string iotHubHostName = "<IoTHubHostname>";
DeviceAuthenticationWithRegistrySymmetricKeyvar deviceAuthentication = new DeviceAuthenticationWithRegistrySymmetricKey(deviceId, deviceKey);

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
> [Explorer les API clientes](/dotnet/api/overview/azure/iot/client)

## <a name="samples"></a>Exemples

- [Service web générique à scénario Event Hub](https://azure.microsoft.com/resources/samples/event-hubs-dotnet-importfromweb/)

Afficher la [liste complète](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=iot-hub) de Azure IoT Upsamples.

Consultez le [Guide du développeur IoT Hub](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide) pour obtenir d’autres conseils.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
