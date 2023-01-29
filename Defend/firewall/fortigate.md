# Fortigate

> [Documentation](https://docs.fortinet.com/document/fortigate/7.2.3/administration-guide/954635/getting-started)

???+ info "Installation"
    1. Connext with remote console
    2. Change the startup password
    3. `execute formatlogdisk` format the disk for logs (Init)

???+ info "Admin port"
    1. `config system interface` enter inside configuration menu for interfaces
    2. `edit port6` enter in edit menu for admin port
    3. `set ip x.x.x.x mask.mask.mask.mask` change ip adress
    4. `set allowaccess ping http https ssh` allow network trafic
    5. `end` quit menu

???+ info "Access to outside"
    1. `config system interface` enter inside configuration menu for interfaces
    2. `edit port1`  enter in edit menu for admin port
    3. `set ip x.x.x.x mask.mask.mask.mask` change ip adress
    4. `set allowaccess ping` allow network trafic
    5. `end` quit menu

???+ info "Default gateway"
    1. `config router static` enter inside configuration menu for gateway
    2. `Edit 1` edit entry 1
    3. `Set dst 0.0.0.0 0.0.0.0` edit destination adress
    4. `Set device port1` edit port
    5. `Set gateway x.x.x.x` edit gateway
    6. `End` quit menu

???+ info "DNS server"
    1. `Config system dns` enter inside configuration menu for DNS
    2. `Set primary x.x.x.x` edit IP adress
    3. `end` quit menu

???+ info "Add licence"
    1. Configure administration station to get access to fortigate
    2. Use web interface `https://$IP`
    3. Follow setup installer

???+ info "Reverse proxy"
    **Reverse Proxy**
    `Policy&Objects~>Virtual Server~>Create New`
    * Type : HTTP
    * Interface : WAN
    * Virtual server IP : \<IP WAN FW>
    * Virtual server port : \<Port exposé FW>
    * Load Balancing Method : HTTP host
    * Real Server : dns server dest / port dest / ip dest

    `Policy&Objects~>Firewall Policy~>Create New`
    * Inspection mode : Proxy-based
    * Incoming interface : WAN
    * Outgoing interface : DMZ-WEB
    * Source : all
    * Destination : \<nom object virtual server> # NB : doit être fait après avoir configuré l'inspection mode et les interfaces
    * Action : Accept
    * NAT : enable
    * Web filter : default
    * IPS : protect_http_server
    * SSL Inspection : certificate inspection

???+ info "VPN"
    VPN => IPsec Wizzard
    Template type : Custom
    Network :
    * IP Address : IP du pare-feu distant
    * Interface : Interface de sortie (WAN)
    * NAT Traversal : Disable
    * Deed Peer Detection : On Idle

    IKE : Version 2

    Phase 1 Proposal : (NB : Supprimer les proposisions non conformes)
    * Encryption : AES256GCM| PRF : PRFSHA256
    * Diffie-Hellman Groups : 19
    * Key Lifetime : 21600

    Phase 2 selectors : (NB : Supprimer les proposisions non conformes)
    New Phase 2 :
    * Local Address : <Subnet_local>
    * Remote Address : <Subnet_distant_to_access>
    * Advanced :	
        * Phase 2 Proposal :
            * Encryption : AES256GCM
            * Diffie-Hellman Groups : 19
            * Key Lifetime : 3600
    => Valider et si nécessaire, cliquer sur "Add" (dans Phase 2 Selectors), et configurer le prochain réseau en suivant la procédure ci-dessus.
