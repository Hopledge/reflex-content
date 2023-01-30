## Exchange

### Configuration Serveur Exchange
Nous configurons le serveur Windows Exchange en tant que **serveur mail**.
Pour cela nous suivons la [documentation Microsoft](https://learn.microsoft.com/en-us/exchange/plan-and-deploy/deploy-new-installations/install-mailbox-role?view=exchserver-2019).

![](https://md.floppy.sh/uploads/ed3ed1b9-e0f6-43a2-ab00-c35ece2a50ac.png)

Afin d'éviter les erreurs, il faut avoir quelques prérequis : 
- [x] Renommer le serveur avec un nom explicite
- [x] Joindre le domaine AD
- [x] Installer [.NET Framework 4.8](https://download.visualstudio.microsoft.com/download/pr/014120d7-d689-4305-befd-3cb711108212/0fd66638cde16859462a6243a4629a50/ndp48-x86-x64-allos-enu.exe)
- [x] Installer [Visual Studio 2013](https://support.microsoft.com/fr-fr/topic/update-for-visual-c-2013-redistributable-package-d8ccd6a5-4e26-c290-517b-8da6cfdf4f10)
- [x] Installer la fonctionnalité [Server Media Foundation] : `Install-WindowsFeature Server-Media-Foundation`
- [x] Installer les outils Remote Server Administration via PS Admin : `Install-WindowsFeature NET-Framework-45-Features, RSAT-ADDS`
- [x] Préparer le "Schéma" pour le setup : `Setup.exe /PrepareSchema /IAcceptExchangeServerLicenseTerms`
- [x] Préparer l'AD pour le setup : `Setup.exe /PrepareAD /OrganizationName:”corp05” /IAcceptExchangeServerLicenseTerms`
- [x] Lancer le `Setup.exe` et laisser les paramètres par défaut

Une fois cela fait : 
- [x] Se connecter au **Centre d'Administration Exchange** (depuis le menu démarrer)
- [x] Configurer Outlook de sortes à ce que nos utilisateurs AD bénéficie d'une boite mail : Destinataire > BAL > Nouveau (+) > Sélectionner les utilisateurs de l'AD et leur attribuer un alias.
    
En tant qu'utilisateur, nous pouvons nous connecter à l'[interface web](https://srv-exch/owa), avec notre identifiant mail et le mot de passe de notre session AD.
> il faut penser à ouvrir les flux Web entre les USER et l'EXCHANGE
