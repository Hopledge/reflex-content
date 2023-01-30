# IIS

- [x] Installation

IIS est un service [Microsoft](https://learn.microsoft.com/en-us/dynamics-nav/how-to--install-and-configure-internet-information-services-for-microsoft-dynamics-nav-web-client), nous pouvons donc l'ajouter à notre serveur comme n'importe quel autre service.

Il suffit donc d'aller dans le menu principal de notre Windows Server 2016, cliquer sur `Ajouter des rôles et fonctionnalités`, sélectionner son serveur, puis choisir le Rôle `Serveur IIS`. Ajouter les fonctionalités nécessaires au service et finir la configuration. 

- [x] Vérification

Pour vérifier le fonctionnement du service, il suffit de se rendre sur notre moteur de recherche et taper http://localhost/
![](https://md.floppy.sh/uploads/cd296d28-e610-4efe-bd80-13fb285b84b6.png)

## Serveur de fichiers

- [x] Renommer le serveur avec un nom explicite (SRV-FILER)
- [x] Ajouter le serveur au domaine
- [x] Ajouter le rôle "service de fichier et iSCSI" et la fonctionnalité "Support de partage de fichiers SMB"
- [x] Dans l'onglet "service de fichiers et de stockage", allez dans "Partages" > "Nouveau partage" et spécifier le dossier à partager
