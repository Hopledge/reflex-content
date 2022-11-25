# Fortigate

> [Documentation](https://docs.fortinet.com/document/fortigate/7.2.3/administration-guide/954635/getting-started)

> Translation in progress

### Installation

1. Connext with remote console
2. Change the startup password
3. `execute formatlogdisk` format the disk for logs (Init)
**Admin Port**
1. `config system interface` enter inside configuration menu for interfaces
2. `edit port6` enter in edit menu for admin port
3. `set ip x.x.x.x mask.mask.mask.mask` change ip adress
4. `set allowaccess ping http https ssh` allow network trafic
5. `end` quit menu
**Accès vers l'exterieur**
9. `config system interface` entre dans le menu de configuration des interfaces 
10. `edit port1` entre en mode édition du port admin
11. `set ip x.x.x.x mask.mask.mask.mask` change l'adresse ip
12. `set allowaccess ping`autorise les fluxs
13. `end` quitte l'édition
**Route par défaut**
14. `config router static` entre dans le menu de configuration de la route par défaut
15. `Edit 1` édite l'entrée 1
16. `Set dst 0.0.0.0 0.0.0.0` modifie la destination
17. `Set device port1` modifie le port
18. `Set gateway x.x.x.x` modifie la passerelle
19. `End` quitte l'édition
**Serveur DNS**
20. `Config system dns` entre dans le menu DNS
21. `Set primary x.x.x.x` modifie l'IP
22. `end` quitte l'édition
**Ajouter licence**
23. Configurer le poste d'administration pour accéder au fortigate
24. Accéder à l'interface web
**Configuration initiale**
25. Suivre le setup
