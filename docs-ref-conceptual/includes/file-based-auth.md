---
ms.service: multiple
ms.date: 9/20/2018
ms.topic: include
ms.openlocfilehash: 7f7c24957d2bc0574fc0b1bf2a8ae8fe8b4dfc64
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190712"
---
<span data-ttu-id="2311e-101">Créez un fichier texte nommé `azureauth.json`.</span><span class="sxs-lookup"><span data-stu-id="2311e-101">Create a text file named `azureauth.json`.</span></span> <span data-ttu-id="2311e-102">Collez la sortie JSON obtenue à la création du principal de service.</span><span class="sxs-lookup"><span data-stu-id="2311e-102">Paste the JSON output from when you created the service principal.</span></span>

<span data-ttu-id="2311e-103">Enregistrez ce fichier dans un emplacement sécurisé sur votre système que votre code peut lire.</span><span class="sxs-lookup"><span data-stu-id="2311e-103">Save this file in a secure location on your system where your code can read it.</span></span> <span data-ttu-id="2311e-104">Utilisez PowerShell pour définir une variable d’environnement nommée `AZURE_AUTH_LOCATION` avec le chemin d’accès complet au fichier, par exemple :</span><span class="sxs-lookup"><span data-stu-id="2311e-104">Use PowerShell to set an environment variable named `AZURE_AUTH_LOCATION` with the full path to the file, for example:</span></span>

```powershell
[Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\src\azureauth.json", "User")
```
