---
title: "Didacticiels pour l’envoi de message et IoT avec .NET sur Azure | Microsoft Docs"
description: "Envoyez des messages entre les applications cloud ainsi qu’entre les appareils et le cloud à l’aide de .NET et des services Azure."
author: camsoper
manager: douge
ms.assetid: 2ce6ea06-7b0b-45e6-8ca0-44e4e4030b82
ms.devlang: dotnet
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 4/10/2017
ms.author: casoper
ms.openlocfilehash: 0c3e81231ac88b2418778b83ecabcbb553608e24
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2017
---
# <a name="net-tutorials-for-enterprise-messaging-and-internet-of-things-iot"></a><span data-ttu-id="e0f9b-103">Didacticiels .NET pour la messagerie d’entreprise et l’Internet des objets (IoT)</span><span class="sxs-lookup"><span data-stu-id="e0f9b-103">.NET tutorials for enterprise messaging and Internet of Things (IoT)</span></span>

<span data-ttu-id="e0f9b-104">Le tableau suivant renvoie à des didacticiels approfondis permettant d’envoyer et de lire des messages entre les applications et les appareils à partir de votre code .NET à l’aide des services Azure.</span><span class="sxs-lookup"><span data-stu-id="e0f9b-104">The following table links to in-depth tutorials for sending and reading messages between applications and devices in from your .NET code using Azure services.</span></span>

<span data-ttu-id="e0f9b-105">Pour un exemple de code source, consultez la liste des [exemples de service Azure](https://azure.microsoft.com/resources/samples/?platform=dotnet).</span><span class="sxs-lookup"><span data-stu-id="e0f9b-105">For sample source code, see the list of [Azure service samples](https://azure.microsoft.com/resources/samples/?platform=dotnet).</span></span>


| | |
|---|---|
| <span data-ttu-id="e0f9b-106">**Service Bus**</span><span class="sxs-lookup"><span data-stu-id="e0f9b-106">**Service Bus**</span></span> | |
| <span data-ttu-id="e0f9b-107">[Utilisation des files d’attente Service Bus][1]</span><span class="sxs-lookup"><span data-stu-id="e0f9b-107">[How to use Service Bus queues][1]</span></span> | <span data-ttu-id="e0f9b-108">Créez des files d’attente, envoyez et recevez des messages, et supprimez les files d’attente.</span><span class="sxs-lookup"><span data-stu-id="e0f9b-108">Create queues, send and receive messages, and delete queues.</span></span> | 
| <span data-ttu-id="e0f9b-109">[Utilisation des rubriques et abonnements Service Bus][2]</span><span class="sxs-lookup"><span data-stu-id="e0f9b-109">[How to use Service Bus topics and subscriptions][2]</span></span> | <span data-ttu-id="e0f9b-110">Découvrez comment utiliser le modèle de communication par publication/abonnement avec Service Bus.</span><span class="sxs-lookup"><span data-stu-id="e0f9b-110">Learn how to use publish/subscribe communication model with Service Bus.</span></span>
| <span data-ttu-id="e0f9b-111">[Utilisation de Service Bus à partir de .NET avec AMQP 1.0][3]</span><span class="sxs-lookup"><span data-stu-id="e0f9b-111">[Using Service Bus from .NET with AMQP 1.0][3]</span></span> | <span data-ttu-id="e0f9b-112">Découvrez comment utiliser AMQP dans vos applications Service Bus.</span><span class="sxs-lookup"><span data-stu-id="e0f9b-112">Learn how to use AMQP in you Service Bus applications.</span></span>
|<span data-ttu-id="e0f9b-113">**IoT Hub**</span><span class="sxs-lookup"><span data-stu-id="e0f9b-113">**IoT Hub**</span></span>|
| <span data-ttu-id="e0f9b-114">[Connexion du périphérique simulé à votre hub IoT][4]</span><span class="sxs-lookup"><span data-stu-id="e0f9b-114">[Connect a simulated device to your IoT Hub][4]</span></span> | <span data-ttu-id="e0f9b-115">Créez une identité d’appareil, envoyez des messages et traitez les données de télémétrie de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="e0f9b-115">Create a device identity, send messages, and process telemetry from your IoT Hub.</span></span> |   
| <span data-ttu-id="e0f9b-116">[Traitement des messages appareil-à-cloud][5]</span><span class="sxs-lookup"><span data-stu-id="e0f9b-116">[Process device-to-cloud messages][5]</span></span> | <span data-ttu-id="e0f9b-117">Envoyez des messages à partir d’un appareil simulé et traitez-les dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="e0f9b-117">Send messages from a simulated device and process them in the cloud.</span></span> |
|<span data-ttu-id="e0f9b-118">**Concentrateur d’événements**</span><span class="sxs-lookup"><span data-stu-id="e0f9b-118">**Event Hub**</span></span>|
| <span data-ttu-id="e0f9b-119">[Envoyer des événements à un Event Hub][6]</span><span class="sxs-lookup"><span data-stu-id="e0f9b-119">[Send events to an Event Hub][6]</span></span> | <span data-ttu-id="e0f9b-120">Envoyez des événements à un Event Hub à partir d’une application console.</span><span class="sxs-lookup"><span data-stu-id="e0f9b-120">Send events to Event hub from a console application.</span></span>
| <span data-ttu-id="e0f9b-121">[Recevoir des événements d’Event Hubs][7]</span><span class="sxs-lookup"><span data-stu-id="e0f9b-121">[Receive events from Event Hubs][7]</span></span> | <span data-ttu-id="e0f9b-122">Recevez des messages et traitez-les en parallèle.</span><span class="sxs-lookup"><span data-stu-id="e0f9b-122">Receive messages and process them in parallel.</span></span>


[1]: /azure/service-bus-messaging/service-bus-dotnet-get-started-with-queues
[2]: /azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions
[3]: /azure/service-bus-messaging/service-bus-amqp-dotnet
[4]: /azure/iot-hub/iot-hub-csharp-csharp-getstarted
[5]: /azure/iot-hub/iot-hub-csharp-csharp-process-d2c
[6]: /azure/event-hubs/event-hubs-dotnet-standard-getstarted-send
[7]: /azure/event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph


