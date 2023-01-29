# Splunk

## Server

### Installation

Install the debian package, but required curl.

Installation folder `/opt/splunk`

Launch server, and create the administrator account

```bash
./splunk start --accept-license --answer-yes
```

## Forwarders

### Installation

You can easilly deploy agent with GPO with this [tutorial](https://techexpert.tips/fr/windows-fr/gpo-creer-une-tache-planifiee/).

#### Fortigate

**Côté SPLUNK**
Récupérer l'app et l'add-on pour splunk (sur teams => en .tgz) et les mettre sur la machine Splunk
Sur l'interface web du splunk (127.0.0.1:8000), dans le bandeau du haut (a gauche), cliquer sur `Apps ->Manage Apps`, puis en haut a droite `Install ap from file`

Settings -> Data inputs
UDP -> Add new
Port 514 => Next
Source type :  Select => Source type : `fgt_log` (s'il n'est pas déjà présent, faire :  Source type => New => Source type : `fgt_log` | Source Type Category `Custom`)

**Côté Fortigate**
Log & Report => Send logs to Syslog : Enable | Ip address/FQDN : <ip_splunk>

**Validation**
Sur splunk, des logs doivent être présent dans "Apps" (sur le menu de gauche) > Fortinet Fortigate App for Splunk

#### Linux

**Côté client**
cd /opt
tar -zxf splunkforwarder-[...].tgz
chown -R root splunkforwarder
/opt/splunkforwarder/bin/splunk boot-start
/opt/splunkforwarder/bin/splunk start --accept-license

**Côté SPLUNK**
Settings -> Forwarding and receiving
Configure receiving -> Add new
Spécifier le port "9997"

**Côté pare-feu**
Créer un object service pour le port 9997
Ajouter une règle de filtrage passante du client vers splunk pour l'object précedement créé. 

**Côté client**
/opt/splunkforwarder/bin/splunk add forward-server <ip_splunk_serv>:9997
Vérifier que le serveur est bien dans les "Active forwards" à l'aide de la commade suivante : `/opt/splunkforwarder/bin/splunk list forward-server`
/opt/splunkforwarder/bin/splunk add monitor /var/log/apache2/access.log -index main -sourcetype apache2_access

**Validation**
Sur Splunk, aller dans les logs (cliquer sur splunk => Search & Reporting), chercher `*`, et dans les events, lister les "sourcetype" (volet de gauche) => vérifier que notre source-type y est bien.
