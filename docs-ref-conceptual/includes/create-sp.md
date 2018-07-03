Votre application .NET a besoin d’autorisations pour lire et créer des ressources dans votre abonnement Azure afin d’utiliser les bibliothèques de gestion Azure pour .NET. Créez un principal de service et configurez votre application pour qu’elle s’exécute avec ses informations d’identification pour accorder cet accès. Les principaux de service permettent de créer un compte non interactif associé à votre identité, auquel vous accordez seulement les privilèges que votre application doit exécuter.

Tout d’abord, connectez-vous à Azure PowerShell :

```powershell
Login-AzureRmAccount
```

Notez les informations affichées concernant votre tenant et votre abonnement :

```plaintext
Environment           : AzureCloud
Account               : jane@contoso.com
TenantId              : 43413cc1-5886-4711-9804-8cfea3d1c3ee
SubscriptionId        : 15dbcfa8-4b93-4c9a-881c-6189d39f04d4
SubscriptionName      : my-subscription
CurrentStorageAccount : 
```

[Créez un principal de service à l’aide de PowerShell](/powershell/azure/create-azure-service-principal-azureps), comme illustré ci-dessous. 

> [!NOTE]
> Si le cmdlet `New-AzureRmADServicePrincipal` ci-dessous retourne « Un autre objet avec la même valeur pour la propriété identifierUris existe déjà », cela signifie qu’un principal de service portant ce nom existe déjà dans votre client. Utilisez une autre valeur pour le paramètre **DisplayName**. 

```powershell
# Create the service principal (use a strong password)
$cred = Get-Credential
$sp = New-AzureRmADServicePrincipal -DisplayName "AzureDotNetTest" -Password $cred.Password

# Give it the permissions it needs...
New-AzureRmRoleAssignment -ServicePrincipalName $sp.ApplicationId -RoleDefinitionName Contributor

# Display the Application ID, because we'll need it later.
$sp | Select DisplayName, ApplicationId
```

Veillez à noter l’ApplicationId :

```plaintext
DisplayName     ApplicationId
-----------     -------------
AzureDotNetTest a2ab11af-01aa-4759-8345-7803287dbd39
```
