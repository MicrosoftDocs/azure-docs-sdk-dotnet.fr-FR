Créez un fichier texte nommé `azureauth.json`. Collez la sortie JSON obtenue à la création du principal de service.

Enregistrez ce fichier dans un emplacement sécurisé sur votre système que votre code peut lire. Utilisez PowerShell pour définir une variable d’environnement nommée `AZURE_AUTH_LOCATION` avec le chemin d’accès complet au fichier, par exemple :

```powershell
[Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\src\azureauth.json", "User")
```
