## 1 – Installation de Veeam Agent pour Linx

Nous allons nous connecter sur la VM debian en ssh via l’utilitaire putty et lancer les commandes suivantes

```
apt-get update && apt-get upgrade
```

Ensuite nous allons nous rendre dans le répertoire temporaire de notre VM

```
cd /tmp
```

Nous allons nous connecter sur le site de Veeam https://www.veeam.com/fr/linux-backup-free.html sur notre machine en local pour récupérer le lien de téléchargement de la dernière version de Veeam Agent pour Linux. Si vous avez installé une interface graphique sur votre Debian, vous pouvez télécharger directement le package sur la VM

<img width="790" height="336" src=":/eca9a19e0a6a4219bf52e9050bcd351a" class="jop-noMdConv">

Créer un compte ou se connecter sur le site de Veeam, choisir la version de votre système d’opération et l’architecture

![](:/cfdbae98550e405ba290bb681d9e91ed)

Cliquez sur **Download** pour récupérer le lien de téléchargement

![](:/08ca9dbc479c434dabcd363a42ae11b6)

Il faut copier le lien de téléchargement pour récupérer le package sur votre machine Debian

<img width="790" height="160" src=":/756fe4ada0bf4e3897ca53c645a145bc" class="jop-noMdConv">

Par la même occasion il faut télécharger l’iso Veeam Linux Recovery Media pour la restauration barre métal que nous verrons après

<img width="790" height="366" src=":/30b5004e8ab8410c95dd2c421e9e98c0" class="jop-noMdConv">

Maintenant sur notre VM Linux, lancer les commandes suivantes

```
# wget https://download2.veeam.com/veeam-release-deb_1.0.7_amd64.deb
# dpkg -i veeam*.deb
# apt-get update && apt-get upgrade
```

Installons les packages suivants

```
apt-get install -y veeam  nfs-common
```

Démarrer Veeam

```
veeam
```

Accepter les conditions et cliquer sur suivant

<img width="790" height="577" src=":/f8a5fea06a1c48b8b823c858b2d6dc77" class="jop-noMdConv">

Cliquer sur suivant

<img width="790" height="558" src=":/c2075a67b4f94aaaa08552a1a97848c6" class="jop-noMdConv">

Si vous avez une clé de produit il faut la valider sinon cliquez sur Finish

<img width="790" height="556" src=":/31d915b37ad0467d87ee012007972c0e" class="jop-noMdConv">

Appuyez sur la touche de clavier « **C** » pour configurer votre sauvegarde

<img width="790" height="564" src=":/57729335888149a584b7ab6f47882e3d" class="jop-noMdConv">

Nommer votre sauvegarde et cliquer sur suivant

<img width="790" height="562" src=":/e86691158e2a4a1bbb6ccc69212f6ff0" class="jop-noMdConv">

Choisir votre type de sauvegarde

- Entire machine : pour sauvegarder toute la machine et avoir la possibilité de faire une sauvegarde barre métal
- Volume Level vackup : pour sauvegarder une partition précise de votre machine
- File level backup : Pour sauvegarder des répertoires précis de votre serveur

Pour ce tuto nous allons choisir la première option

<img width="790" height="558" src=":/1e860dd51c844135a08c9eb0950b85e1" class="jop-noMdConv">

Choisir l’option Veam Backup & Replication
Et faire les configurations nécéssaires.

<img width="790" height="558" src=":/ab7085d01a6342d18c4b2a673abfebb7" class="jop-noMdConv">

Il faut choisir les jours et l’heure de sauvegarde

<img width="790" height="557" src=":/e95155d0959d4e2bb8690057dcbcdaf0" class="jop-noMdConv">

Pour finir laisser la case cochée pour démarrer la sauvegarde immédiatement

<img width="790" height="559" src=":/51cfe551de454400bdc1c504b17cd768" class="jop-noMdConv">

Cliquer sur OK

<img width="790" height="553" src=":/83baface30f141feb05774e061f9fcd7" class="jop-noMdConv">

Patienter jusqu’à la fin de la sauvegarde

<img width="790" height="560" src=":/cdac041d9d3c4db0951904816a1e5e97" class="jop-noMdConv"> <img width="790" height="552" src=":/65c45a05516447918d932bebc13e0d46" class="jop-noMdConv">

Depuis l'interface de veam vous pouvez constater que votre backup a bien été effectuée.

Source : https://www.networks-it.fr/sauvegarder-une-machine-linux-avec-veeam-agent-sur-un-nas-synology/