### Stormshield

- [x] Effectuer la première configuration des interfaces en CLI

```
VMSNSX01B2085A9>defaultconfig -f -r -p

Interface out (sortie internet) : 192.168.1.205 / 255.255.255.0 / 192.168.1.254

Interface in : 10.101.5.254 / 255.255.255.0
```

- [x] Accéder à la WEB interface depuis un poste admin (http://10.101.5.254)
> admin:Passw0rd

### VPN IPsec Fortinet - Stormshield

#### Configuration VPN Fortinet
- [x] Création d'un "IPsec Tunnels" dans `VPN > IPsec Tunnels > Create New > IPsec Tunnel`

1.  VPN Setup 
- Name : Donner un nom explicite
- Template type : Sélectionner "Site to Site"
- Remote device type : Sélectionner Fortigate

2. Authentication
- Remote IP address : Adresse IP du pare-feu distant
- Outgoing interface : WAN
- Authentication method : Pre-shared Key (puis indiquer la clé)

3. Policy & Routing
- Local interface : interface du (ou des) réseau local que l'on veut connecter au VPN
- Local subnets : normalement autocomplété
- Remote subnet : réseau local distant à joindre/masque

3. Review Settings
Vérifier la configuration et cliquer sur `Create`

- [x] Passer la configuration VPN en custom

* Sélectionner le VPN IPsec précédemment crée puis cliquer sur `Edit`
* Cliquer sur `Convert To Custom Tunnel`

![](https://md.floppy.sh/uploads/a75906c5-fe8d-494b-9fdd-e0a5e3ff005f.png)

- [x] Noter les information de la Phase 1
> Sélectionner qu'un Diffie-Hellman Group

![](https://md.floppy.sh/uploads/cc11c2a8-2a1a-424d-9182-876012c2e621.png)

- [x] Noter les information de la Phase 2
> Ne garder que les 4 premiers algorithmes de chiffrement et authentification
> Sélectionner qu'un Diffie-Hellman Group

![](https://md.floppy.sh/uploads/7c1483aa-da3d-4612-8e22-fbf40d32422c.png)

> Ajouter chaque réseau local dans la phase 2 

![](https://md.floppy.sh/uploads/022a3713-6ea8-4c9f-bbd3-adfd8809287f.png)

- [x] Finir la configuration en cliquant sur `OK`

#### Configuration VPN Stormshield

- [x] Création d'un "IPsec Tunnels" dans `VPN > IPsec VPN > Encryption Policy - tunnels > Add > Site-to-Site tunnel`

1. Local Network

- Sélectionner le réseau local du FW : Network_in

2. Peer selection

- Create an IKEv1 peer
- Remote Gateway : Créer un objet ou Sélectionner l'objet correspondant à l'adresse IP du pare-feu distant
- Peer creation wizard : Sélectionner `Pre-shared key (PSK)` puis écrire la même clé inscrite dans le Fortinet.

3. Remote network

- Créer un objet ou Sélectionner l'objet correspondant au réseau distant à joindre

> Répéter cette étape pour chaque LAN distant

![](https://md.floppy.sh/uploads/beb10849-cd37-4936-b5dd-8d51c2a0dc41.png)

- [x] Modifier les valeurs du chiffrement du VPN site-to-site dans `VPN > IPsec VPN > Encryption profiles`

* Indiquer les valeurs de la configuration Fortinet précedente pour l phase 1 et 2

![](https://md.floppy.sh/uploads/da4cd0b9-2de1-4ac3-97af-a3ee368f9196.png)

* Sauvegarder la configuration

- [x] Création d'une règle statique dans `Network > Routing > IPv4 Static routes > Add`

> Répéter cette étape pour chaque LAN distant

![](https://md.floppy.sh/uploads/d56b8e55-65df-42d8-b6c1-31e31ef864dc.png)

- [x] Création d'une règle autorisant le flux entre le LAN Distant et le réseau interne

> Attention, Stormshield requiert une règle dans les 2 sens pour ICMP par exemple

![](https://md.floppy.sh/uploads/13269045-20cf-4e4b-b854-d177280e8237.png)