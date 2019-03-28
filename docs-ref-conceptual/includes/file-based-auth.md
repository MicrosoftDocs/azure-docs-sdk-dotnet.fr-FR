---
ms.service: multiple
ms.date: 9/20/2018
ms.topic: include
ms.openlocfilehash: 7f7c24957d2bc0574fc0b1bf2a8ae8fe8b4dfc64
ms.sourcegitcommit: e534dad2d96b72ab6a9bc4b5567508962bd7e05c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58343338"
---
Créez un fichier texte nommé `azureauth.json`. Collez la sortie JSON obtenue à la création du principal de service.

Enregistrez ce fichier dans un emplacement sécurisé sur votre système que votre code peut lire. Utilisez PowerShell pour définir une variable d’environnement nommée `AZURE_AUTH_LOCATION` avec le chemin d’accès complet au fichier, par exemple :

```powershell
[Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\src\azureauth.json", "User")
```
