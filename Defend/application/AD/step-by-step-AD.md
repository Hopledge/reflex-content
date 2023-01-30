## Active Directory

### Configuration du contrôleur de domaine

- [x] Se connecter au DC en tant qu'Administrateur et accéder au tableau de bord
- [x] Changer le nom du Serveur pour y mettre un nom explicite (SRV-DC01)
- [x] Ajouter des rôles et fonctionnalités depuis "Gérer" en haut à droite
- [x] Dans "Rôles de serveurs", cocher "Service AD DS" et "Service DNS"
- [x] Laisser le reste par défaut, puis "Installer"

- [x] Promouvoir ce serveur en contrôleur de domaine

![](https://md.floppy.sh/uploads/2a492489-7bfb-4390-b73b-fa7da7e0c500.png)

- [x] Configurer le déploiement de l'AD

    - [x] Ajouter un nouvelle forêt : corp05.com
    - [x] Ajouter un mot de passe de restauration des services d'annuaires
    
![](https://md.floppy.sh/uploads/71680327-43ec-4ad5-80ec-87da77dba1b1.png)

- [x] Vérifier la configuration puis "Installer" (le serveur va redémarrer)

Pour gérer les services Active Directory, vous trouvez l'outil "Utilisateurs et ordinateurs Active Directory" dans le menu démarrer, et dans « Outils d’administration »

- [x] Création d’un nouvel objet “utilisateur” dans l'AD

![](https://md.floppy.sh/uploads/a2d28db9-33a6-47b7-aa27-7bb78ac49be5.png)

### Ajout d'un second contrôleur de domaine

- [x] Ajouter le serveur au domaine
- [x] Ajouter le rôle AD DS
- [x] Promouvoir le serveur en tant que contôleur de domaine
- [x] Cocher "Ajouter un contrôleur de domaine à un domaine existant"

![](https://md.floppy.sh/uploads/4aa684ef-e7a9-45be-a1e0-0e754f0eaa47.png)

- [x] Sélectionner le serveur à partir duquel vous voulez répliquer les données AD

![](https://md.floppy.sh/uploads/b08c0b17-e290-449b-8e02-20b9d7863661.png)

- [x] Vérifier la bonne remontée du DC02 depuis la console du DC01

![](https://md.floppy.sh/uploads/1be37ec3-ee33-4fcd-9eaa-d5e65f74745d.png)

### Jonction d'une machine Windows au domaine
Sur le poste client, commencez par lui attribuer une adresse IP fixe et     une adresse de DNS principal (préféré) du serveur AD.
   
Dans les paramètres avancés, allez dans l’onglet DNS.
Dans la partie « Suffixe DNS pour cette connexion », renseignez le nom     complet de votre domaine.
Cochez la case « Utiliser le suffixe DNS de cette connexion pour           l’enregistrement DNS ».

- [x] Test de ping sur le nom du serveur (ping SRV-DC01)

Depuis les paramètres de la machine (Panneau de config> Système et         Sécurité > Système > Renommer ce PC), renommez le poste client par un       nom identifiable ou une appelation définie par la politique de             nommage de l’entreprise (PC-001, PC-COMPTA-1…).
Dans la partie « Membre d’un », cochez Domaine et renseignez le nom de     votre domaine.
    
![](https://md.floppy.sh/uploads/8dd248ef-9ffd-4cfe-a920-4199cb96a623.png)

- [x] Renommer le client et le joindre au domaine (identifiants admin nécessaires)

![](https://md.floppy.sh/uploads/8313ece1-97da-4394-a60e-dd3752eb9189.png)

  - [x] Redémarrer et se connection avec un compte user du domaine

### GPO

#### Stratégie d'audit

On modifie la default domain policy puis on suit le guide d'hygiène de l'ANSSI.

On active toutes les stratégies d'audit de base à cet endroit : 

`Configuration ordinateur\Stratégies\Paramètres Windows\Paramètres de sécurité\Stratégies locales\
Stratégie d'audit`

![](https://md.floppy.sh/uploads/7785614d-5119-4308-a1e3-a1fb20166b2c.png)

Et on fait la même chose, plus finement, avec les stratégies d'audit avancées : 

`Configuration ordinateur\Stratégies\Paramètres Windows\Paramètres de sécurité\Configuration avancée de la stratégie d'audit\Stratégies d'audit système - Objet Stratégie de groupe`

#### Monter un disque réseau

- [x] Ouvrir la console "Gestion de stratégie de groupe" depuis le DC ou depuis un poste utilisateur avec [RSAT](#Remote-Server-Administration-Tools-RSAT)

- [x] Clic droit sur "Objets de stratégie de groupe" puis "Nouveau". Nommer cette GPO, par exemple "U_Lecteur-<nom_partage>".

- [x] Modifier cette GPO et accéder à l'emplacement suivant :
`Configuration utilisateur > Préférences > Paramètres Windows > Mappages de lecteur`

Puis `Sur la droite, effectuer un clic droit : Nouveau > Lecteur mappé`

- [x] Saisir les informations du lecteur réseau
> L'emplacement du lecteur réseau peut se trouver sur un serveur de fichier

![](https://md.floppy.sh/uploads/46b84c2b-dfdc-424a-bf51-f87a5b0eba84.png)

- [x] Lier la GPO à un OU / Groupe de sécurité / User

Afin de déployer la GPO à un ou des utilisateur(s) spécifique(s) :
1. Sélectionner la GPO dans "Objets de stratégie de groupe"
2. Ajouter un utilisateur, Groupe de sécurité, ordinateur dans le menu "Etendue" > Filtrage de sécurité
3. Supprimer "Utilisateurs authentifiés"

![](https://md.floppy.sh/uploads/1201a2b9-d8cd-41e8-a135-bd1d3ff2dce3.png)

4. Ajouter "Utilisateurs authentifiés dans "Délégation" avec des autorisations de Lecture.

- [x] Tester la GPO un ordinateur du domaine avec un utilisateur authentifié
> Commande powershell pour forcer le déploiement : gpupdate /force
> Commande powershell pour voir le contenue du déploiement : gpresult /r

#### Installation d'un logiciel 

- [x] Ouvrir la console "Gestion de stratégie de groupe" depuis le DC ou depuis un poste utilisateur avec [RSAT](#Remote-Server-Administration-Tools-RSAT)

- [x] Clic droit sur "Objets de stratégie de groupe" puis "Nouveau". Nommez cette GPO, par exemple "O_Deployer-<nom_service>".

- [x] Modifier cette GPO et accéder à l'emplacement suivant :
`Configuration ordinateur > Stratégies > Paramètres du logiciel > Installation de logiciel`

- [x] Effectuer un clic droit sur "Installation de logiciel" puis sous "Nouveau" cliqurz sur "Package"

- [x] Indiquer le chemin vers le fichier MSI. 
> Utiliser un chemin réseau vers un partage réseau (serveur de fichier) pour rechercher le fichier MSI.

Lorsque l'on déploie un logiciel, il y a deux modes principaux :

> **Publié** : ce mode est disponible dans le cas de l'installation d'un logiciel dans les paramètres utilisateurs. Le logiciel est alors disponible à l'installation sur la machine, mais il ne s'installe pas automatiquement. L'utilisateur peut installer le logiciel s'il en a besoin.
> **Attribué** : ce mode sert à installer un logiciel par GPO sur une machine, de manière automatique. C'est ce qui nous intéresse aujourd'hui.

- [x] Sélectionner le mode "Attribué"

- [x] Lier la GPO à un OU / Groupe de sécurité / User / Ordinateur

Afin de déployer la GPO à un ou des utilisateur(s) spécifique(s) :
1. Sélectionner la GPO dans "Objets de stratégie de groupe"
2. Ajouter un ordinateur dans le menu "Etendue" > Filtrage de sécurité
3. Supprimer "Utilisateurs authentifiés"

![](https://md.floppy.sh/uploads/bcaa4f81-ca2c-45ab-beb2-2a5d165584c6.png)

4. Ajouter "Utilisateurs authentifiés dans "Délégation" avec des autorisations de Lecture.

- [x] Tester la GPO sur un ordinateur du domaine avec un utilisateur authentifié
> Commande powershell pour forcer le déploiement : gpupdate /force
> Commande powershell pour voir contenue du déploiement : gpresult /r
