<span data-ttu-id="9e846-101">Créez un fichier texte nommé `azureauth.properties` à l’aide des informations d’identification du principal de service :</span><span class="sxs-lookup"><span data-stu-id="9e846-101">Create a text file named `azureauth.properties` using the service principal credentials:</span></span>

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

- <span data-ttu-id="9e846-102">abonnement : utilisez la valeur *SubscriptionId* à partir de laquelle vous avez exécuté `Login-AzureRmAccount`.</span><span class="sxs-lookup"><span data-stu-id="9e846-102">subscription: use the *SubscriptionId* value from when you ran `Login-AzureRmAccount`.</span></span>
- <span data-ttu-id="9e846-103">client : utilisez la valeur *ApplicationId* à partir de la sortie du principal de service.</span><span class="sxs-lookup"><span data-stu-id="9e846-103">client: use the *ApplicationId* value from the service principal output.</span></span>
- <span data-ttu-id="9e846-104">clé : utilisez le paramètre *-Password* que vous avez affecté lorsque vous avez exécuté `New-AzureRmADServicePrincipal` (sans guillemets).</span><span class="sxs-lookup"><span data-stu-id="9e846-104">key: use the *-Password* parameter you assigned when you ran `New-AzureRmADServicePrincipal` (without quotes).</span></span>
- <span data-ttu-id="9e846-105">tenant : utilisez la valeur *TenantId* qui a servi lors de l’exécution de `Login-AzureRmAccount`.</span><span class="sxs-lookup"><span data-stu-id="9e846-105">tenant: use the *TenantId* value from when you ran `Login-AzureRmAccount`.</span></span>

<span data-ttu-id="9e846-106">Enregistrez ce fichier dans un emplacement sécurisé sur votre système que votre code peut lire.</span><span class="sxs-lookup"><span data-stu-id="9e846-106">Save this file in a secure location on your system where your code can read it.</span></span> <span data-ttu-id="9e846-107">Utilisez PowerShell pour définir une variable d’environnement nommée `AZURE_AUTH_LOCATION` avec le chemin d’accès complet au fichier, par exemple :</span><span class="sxs-lookup"><span data-stu-id="9e846-107">Use PowerShell to set an environment variable named `AZURE_AUTH_LOCATION` with the full path to the file, for example:</span></span>

```powershell
[Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\src\azureauth.properties", "User")
```
