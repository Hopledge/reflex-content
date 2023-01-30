# Apache

- [x] Installation
Pour installer le service Apache sur notre hôte WEB 1 (sous Debian 10), nous devons installer le paquet apache2. (droit sudo nécessaire)

```
sudo apt update 
sudo apt install apache2
```

Le service tourne par défaut sur le port 80.

- [x] Vérification

Nous pouvons lancer cette commande pour vérifier si notre service est bien en cours d'exécution

```
sudo systemctl status apache2
```

Nous pouvons désormais nous connecter via notre naviguateur à notre "serveur WEB" : http://localhost

![](https://md.floppy.sh/uploads/7b11eb97-3320-472e-8fce-7709159e6418.png)

#### Additionnal command

| Command 	                    | Action|
|-|-|
| sudo systemctl stop apache2 	| Stop|
| sudo systemctl start apache2 	| Start|
| sudo systemctl restart apache2 	| Restart|
| sudo systemctl enable apache2 	| Start automatically on server boot|
| sudo systemctl disable apache2 	| Deactivate the automatically start|