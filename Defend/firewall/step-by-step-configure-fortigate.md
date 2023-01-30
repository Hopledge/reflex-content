### Fortigate

#### Configuration de base

- [x] Connexion par défaut `admin`:` `
- [x] Changement mdp : `admin`
- [x] Réinitialiser les logs :`execute fomatlogdisk`
> Le reboot qui suivra permettra de prendre en compte les nouvelles interfaces réseaux, et dans le bon ordre (1 → 6)
- [x] Interface ADMIN : 
```
config system interface
	edit port6
	set ip 10.5.5.254 255.255.255.0
	set allowaccess ping http https ssh
	end
```
> port 6 étant l'interface de notre LAN ADMIN dans laquelle se trouve notre VM admin
- [x] Interface WAN : 
```
config system interface
	edit port1
	set ip 192.168.1.105 255.255.255.0
	set allowaccess ping
	end
```
- [x] Route par défaut : 
```
config router static
	edit 1
	set dst 0.0.0.0 0.0.0.0
	set device port1
	set gateway 192.168.1.254
	end
```
- [x] Serveur DNS : 
```
config system dns
    set primary 172.16.1.1
    end
```

- [x] Test sur FW :
```
execute ping 192.168.1.254 (connectivité vers INTERCO C4)
execute ping www.free.fr (résoltution DNS)
```

#### Configuration des règles Fortinet depuis le poste ADMIN

- [x] Test sur la machine du VLAN-ADMIN
    1. connecter la machine au LAN
    2. déactiver l'interface réseau par défaut et n'utiliser que la seconde que l'on vient de créer : `ip link set dev ens192 down`
    3. tester la connectivité vers le FW
```
ping 10.5.5.254
```

- [x] Transférer le fichier de licence (depuis notre hôte) sur la machine ADMIN dans `/tmp` : 
    1. right click on Debian ADMIN machine 
    2. File sharing > Upload file on host
    3. Select file : `FGVM01TM19003425.lic`
    > présent dans nos ressources Teams
    5. Destination folder : `/tmp`

Désormais on utilisera l'interface web : http://10.5.5.254/
- [x] Upload la licence du FW : Fortigate va redémarrer automatiquement
- [x] Se connecter au FW sur https://10.5.5.254/
HOSTNAME : `FORTIGATE05`
Dashboard Setup : Optimal

- [x] Changement des interfaces de chaque port dans Network > Interfaces

- [x] Changement des numéros de ports, l'heure et le timeout dans System > settings
    > 80:8080 et 443:4343
    > GMT +1 
    > Idle Timeout : 480
    
Attention le changement de port va modifier notre accès à l'interface d'admin web qui sera désormais sur https://10.5.5.254:4343/

- [x] Ajout et suppression de features dans System > Feature Visibility

![](https://md.floppy.sh/uploads/c4cf308b-c633-4c8b-a002-89942f91f494.png)

- [x] Configuration du firewall en indiquant les port autorisés de chaque interface dans Network > Interfaces

![](https://md.floppy.sh/uploads/af1eeab1-4423-4e0c-a13c-6875efe75a2f.png)

- [x] Configuration du SMTP avec du NAT (serveur mail) dans Policy & Objects > Virtual IPs

Il faut pour cela créer une Virtual IP, qui relie 192.168.1.105 (interface de sortie) vers 10.5.1.1 (serveur relai en DMZ)

![](https://md.floppy.sh/uploads/309e7b12-63a8-41cb-8145-cdc34d8395fc.png)


- [x] Création des HOSTS correspondants aux machines en place dans Policy & Objects > Addresses
    - [x] HOST_ADMIN
    - [x] HOST_SRV-DNS-C4
    - [x] HOST_SPLUNK
    - [x] HOST_DC01
    - [x] HOST_DC02
    - [x] HOST_EXCH
    - [x] HOST_FILER
    - [x] HOST_WEB1
    - [x] HOST_WEB2
    - [x] HOST_WEB3
    - [x] HOST_USR
    - [x] HOST_MTA
    - [x] HOST_RODC
    - [x] HOST_GLPI
    - [x] HOST_ADMINSITE 
    
- [x] Création de serveur virtuel dans Policy & Objects > Virtual Servers
    - [x] iis.corp05.com
    - [x] apache.corp05.com
    - [x] shop.corp05.com 

![](https://md.floppy.sh/uploads/420249f9-955a-4ee3-a362-a35390ce99cb.png)


- [x] Création des politiques firewall dans Policy & Objects > Firewall Policy

|Name|Description|Source|Destination|Service|
|-|-|-|-|-|
|ADMIN vers WAN|autoriser l'hôte admin à naviguer sur le web en http et https|HOST_ADMIN|all|HTTP, HTTPS|
|ADMIN vers DNS| autoriser l'hote admin a utilisé le DNS quand on sort vers l'extérieur| HOST_ADMIN|HOST_SERV-DNS-C4|DNS|
|ADMIN vers LOG SPLUNK|autoriser l'hote admin à ping et joindre le service web de splunk (log supervisor)|HOST_ADMIN|HOST_SPLUNK|HTTP, HTTPS, PING|
|ADMIN vers DMZ WEB| autoriser l'admin à accéder au site WEB (VS) en HTTP et HTTPS|HOST_ADMIN|HOST_WEB1, HOST_WEB2, HOST_WEB3|HTTP,HTTPS, PING|
|ADMIN vers DMZ RELAY| autoriser l'admin uniquement à PING le relay MAIL|HOST_ADMIN|HOST_MTA|PING|
|ADMIN vers DC| autorier l'admin à se connecter au DC et à communiquer avec|HOST_ADMIN|HOST_DC01|PING, RDP, Windows AD (LDAP, Kerberos etc.)|
|ADMIN vers FILER| autoriser l'admin à utiliser le serveur de fichier|HOST_ADMIN|HOST_FILER|PING, RDP, SMB|
|ADMIN vers EXCH| autorisé l'admin à intervenir sur l'exchange|HOST_ADMIN|HOST_EXCH|RDP, Exchange Server|
|WAN vers DMZ RELAY| n'autoriser que le flux SMTP depuis l'extérieur vers notre serveur mail relay en DMZ|all|VIP_192.168.1.105_SMTP|SMTP|
|WAN vers DMZ WEB| autoriser les connexions web extérieurs uniquement sur nos VS en DMZ WEB sur le port HTTP|all|VS_192.168.1.105_HTTP|HTTP|
|USER vers Service AD|autoriser les utilisateurs à communiquer avec les DC avec les services Windows AD (LDAP, Kerberos etc.)|HOST_USER|HOST_DC01, HOST_DC02|Windows AD, PING|
|USER vers FILER|autoriser les utilisateurs à joindre le serveur de fichier|HOST_USER|HOST_FILER|SMB, PING|
|ADMIN vers USER|autoriser l'admin à interagir sur l'hote utilisateur|HOST_ADMIN|HOST_USER|all services|

Voici les profils de sécurité que nous ajoutons pour les connexions vers les serveurs WEB en DMZ.

![](https://md.floppy.sh/uploads/63e21af5-4e3f-4522-b69d-adf5ecbc3839.png)

> pensez à passez l'inspection mode en Proxy-based
