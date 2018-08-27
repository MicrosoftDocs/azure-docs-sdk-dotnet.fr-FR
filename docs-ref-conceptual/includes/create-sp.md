Votre application .NET a besoin d’autorisations pour lire et créer des ressources dans votre abonnement Azure afin d’utiliser les bibliothèques de gestion Azure pour .NET. Créez un principal de service et configurez votre application pour qu’elle s’exécute avec ses informations d’identification pour accorder cet accès. Les principaux de service permettent de créer un compte non interactif associé à votre identité, auquel vous accordez seulement les privilèges que votre application doit exécuter.

Tout d’abord, connectez-vous à [Azure Cloud Shell](https://shell.azure.com/bash). Vérifiez que vous utilisez actuellement l’abonnement dans lequel vous souhaitez que le principal de service soit créé. 

```azurecli-interactive
az account show
```

Les information relatives à votre abonnement sont affichées.

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

Si vous n’êtes pas connecté au bon abonnement, sélectionnez le bon en saisissant `az account set -s <name or ID of subscription>`.

Créez le principal de service avec la commande suivante :

```azurecli-interactive
az ad sp create-for-rbac --sdk-auth
```

Les informations relatives au principal de service sont affichées en tant que JSON.

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

Copiez et collez la sortie JSON dans un éditeur de texte pour plus tard.
