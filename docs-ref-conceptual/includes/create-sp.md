<span data-ttu-id="c7ded-101">Votre application .NET a besoin d’autorisations pour lire et créer des ressources dans votre abonnement Azure afin d’utiliser les bibliothèques de gestion Azure pour .NET.</span><span class="sxs-lookup"><span data-stu-id="c7ded-101">Your .NET application needs permissions to read and create resources in your Azure subscription in order to use the Azure Management Libraries for .NET.</span></span> <span data-ttu-id="c7ded-102">Créez un principal de service et configurez votre application pour qu’elle s’exécute avec ses informations d’identification pour accorder cet accès.</span><span class="sxs-lookup"><span data-stu-id="c7ded-102">Create a service principal and configure your app to run with its credentials to grant this access.</span></span> <span data-ttu-id="c7ded-103">Les principaux de service permettent de créer un compte non interactif associé à votre identité, auquel vous accordez seulement les privilèges que votre application doit exécuter.</span><span class="sxs-lookup"><span data-stu-id="c7ded-103">Service principals provide a way to create a non-interactive account associated with your identity to which you grant only the privileges your app needs to run.</span></span>

<span data-ttu-id="c7ded-104">Tout d’abord, connectez-vous à Azure PowerShell :</span><span class="sxs-lookup"><span data-stu-id="c7ded-104">First, login to Azure PowerShell:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="c7ded-105">Notez les informations affichées concernant votre tenant et votre abonnement :</span><span class="sxs-lookup"><span data-stu-id="c7ded-105">Note the information displayed about your tenant and subscription:</span></span>

```plaintext
Environment           : AzureCloud
Account               : jane@contoso.com
TenantId              : 43413cc1-5886-4711-9804-8cfea3d1c3ee
SubscriptionId        : 15dbcfa8-4b93-4c9a-881c-6189d39f04d4
SubscriptionName      : my-subscription
CurrentStorageAccount : 
```

<span data-ttu-id="c7ded-106">[Créez un principal de service à l’aide de PowerShell](/powershell/azure/create-azure-service-principal-azureps), comme illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="c7ded-106">[Create a service principal using PowerShell](/powershell/azure/create-azure-service-principal-azureps) as shown below.</span></span> 

> [!NOTE]
> <span data-ttu-id="c7ded-107">Si le cmdlet `New-AzureRmADServicePrincipal` ci-dessous retourne « Un autre objet avec la même valeur pour la propriété identifierUris existe déjà », cela signifie qu’un principal de service portant ce nom existe déjà dans votre client.</span><span class="sxs-lookup"><span data-stu-id="c7ded-107">If the `New-AzureRmADServicePrincipal` cmdlet below returns "Another object with the same value for property identifierUris already exists," there is already a service principal by that name in your tenant.</span></span> <span data-ttu-id="c7ded-108">Utilisez une autre valeur pour le paramètre **DisplayName**.</span><span class="sxs-lookup"><span data-stu-id="c7ded-108">Use a different value for the **DisplayName** parameter.</span></span> 

```powershell
# Create the service principal (use a strong password)
$cred = Get-Credential
$sp = New-AzureRmADServicePrincipal -DisplayName "AzureDotNetTest" -Password $cred.Password

# Give it the permissions it needs...
New-AzureRmRoleAssignment -ServicePrincipalName $sp.ApplicationId -RoleDefinitionName Contributor

# Display the Application ID, because we'll need it later.
$sp | Select DisplayName, ApplicationId
```

<span data-ttu-id="c7ded-109">Veillez à noter l’ApplicationId :</span><span class="sxs-lookup"><span data-stu-id="c7ded-109">Make sure to note the ApplicationId:</span></span>

```plaintext
DisplayName     ApplicationId
-----------     -------------
AzureDotNetTest a2ab11af-01aa-4759-8345-7803287dbd39
```
