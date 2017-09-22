---
<span data-ttu-id="aca8c-101">uid: Microsoft.Azure.Management.Compute.VirtualMachinesOperationsExtensions.Capture(Microsoft.Azure.Management.Compute.IVirtualMachinesOperations,System.String,System.String,Microsoft.Azure.Management.Compute.Models.VirtualMachineCaptureParameters) summary: *content</span><span class="sxs-lookup"><span data-stu-id="aca8c-101">uid: Microsoft.Azure.Management.Compute.VirtualMachinesOperationsExtensions.Capture(Microsoft.Azure.Management.Compute.IVirtualMachinesOperations,System.String,System.String,Microsoft.Azure.Management.Compute.Models.VirtualMachineCaptureParameters) summary: *content</span></span>
---

<span data-ttu-id="aca8c-102">Voici du contenu envoyé par la méthode de remplacement de fichier, afin que les enregistreurs puissent ajouter autant de contenu qu’ils souhaitent dans la documentation de l’API générée au format Markdown.</span><span class="sxs-lookup"><span data-stu-id="aca8c-102">Here is content that is injected by the overwrite file method, so writers can add as much as they want to the generated API documentation in Markown format.</span></span>

---
<span data-ttu-id="aca8c-103">uid: Microsoft.Azure.Management.Compute.VirtualMachinesOperationsExtensions.Capture(Microsoft.Azure.Management.Compute.IVirtualMachinesOperations,System.String,System.String,Microsoft.Azure.Management.Compute.Models.VirtualMachineCaptureParameters) remarks: *content</span><span class="sxs-lookup"><span data-stu-id="aca8c-103">uid: Microsoft.Azure.Management.Compute.VirtualMachinesOperationsExtensions.Capture(Microsoft.Azure.Management.Compute.IVirtualMachinesOperations,System.String,System.String,Microsoft.Azure.Management.Compute.Models.VirtualMachineCaptureParameters) remarks: *content</span></span>
---

<span data-ttu-id="aca8c-104">Le code ci-dessous montre comment appeler la méthode de capture à l’aide du kit de développement logiciel (SDK) Azure .NET.</span><span class="sxs-lookup"><span data-stu-id="aca8c-104">The code below demonstrates how to call the Capture method using the Azure .NET SDK.</span></span> 

```csharp
using Microsoft.Azure.Management.Compute;
using Microsoft.Azure.Management.Compute.Models;
using Microsoft.Rest;

namespace MyAzureVmClientApp
{
    class Program
    {
        static void Main(string[] args)
        {
            var token = "[Token Obtained from ADAL]";

            var credential = new TokenCredentials(token);

            var captureResponse = 
                new ComputeManagementClient(credential)
                .VirtualMachines
                    .Capture(
                        "myResourceGroup",
                        "myVmName",
                        new VirtualMachineCaptureParameters
                        {
                            DestinationContainerName = "myblobcontainer",
                            OverwriteVhds = true,
                            VhdPrefix = "backup"
                        });
        }
    }
}
```

