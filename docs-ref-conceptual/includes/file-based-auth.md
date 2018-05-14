Créez un fichier texte nommé `azureauth.properties` à l’aide des informations d’identification du principal de service :

```plaintext
# sample management library properties file
subscription=15dbcfa8-4b93-4c9a-881c-6189d39f04d4
client=a2ab11af-01aa-4759-8345-7803287dbd39
key=password
tenant=43413cc1-5886-4711-9804-8cfea3d1c3ee
managementURI=https://management.core.windows.net/
baseURL=https://management.azure.com/
authURL=https://login.windows.net/
graphURL=https://graph.windows.net/
```

- abonnement : utilisez la valeur *SubscriptionId* à partir de laquelle vous avez exécuté `Login-AzureRmAccount`.
- client : utilisez la valeur *ApplicationId* à partir de la sortie du principal de service.
- clé : utilisez le paramètre *-Password* que vous avez affecté lorsque vous avez exécuté `New-AzureRmADServicePrincipal` (sans guillemets).
- tenant : utilisez la valeur *TenantId* qui a servi lors de l’exécution de `Login-AzureRmAccount`.

Enregistrez ce fichier dans un emplacement sécurisé sur votre système que votre code peut lire. Utilisez PowerShell pour définir une variable d’environnement nommée `AZURE_AUTH_LOCATION` avec le chemin d’accès complet au fichier, par exemple :

```powershell
[Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\src\azureauth.properties", "User")
```
