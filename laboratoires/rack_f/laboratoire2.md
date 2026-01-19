
# Laboratoire 2 - Configuration des ACL étendues et standards, OSPF, SSH

# Topologie

![Topo](../../topo/rack-f/topo1-4.png)

# Table d’adressage :

|Equipments|Interface     | IP Address     | Subnet Mask     | Default Gateway | Description
|----------|--------------|---------------|----------------|------------------|------------------|
|RACK-F-R1 |G0/0/1   |10.10.10.42       |255.255.255.248           | N/A|Connexion a internet via la switch
|          |G0/0/0   |10.0.0.25   |255.255.255.252| N/A|Connexion au routeur R2
|RACK-F-R2 |G0/0/1   |10.0.0.26   |255.255.255.252| N/A|Connexion au routeur R1
|          |G0/0/0.110|172.16.110.1|255.255.255.0  | N/A|Connexion au switch SW1 - VLAN 100
|          |G0/0/0.120|172.16.120.1|255.255.255.0  | N/A|Connexion au switch SW1 - VLAN 120
|RACK-F-PC1|Fa0      |DHCP       |DHCP  | DHCP   |    |
|RACK-F-PC2|Fa0      |DHCP       |DHCP  | DHCP   |    |

# Table VLAN
|Equipments|VLAN     | Nom VLAN    |
|----------|--------------|---------------|
|RACK-E-SW1, RACK-E-SW2 et RACK-E-SW3|VLAN 110| VLAN110
|          |VLAN 120| VLAN120
|          |VLAN 99| Mgmt_Native

# Table de ports
|Equipments|Ports |  |
|----------|-----|----------|
|RACK-F-SW1 |F1/0/1, F1/0/2, F1/0/3| Trunk
|RACK-F-SW2 |F1/0/2, F1/0/4| Trunk
||F1/0/5| Vlan 110
|RACK-F-SW3 |F1/0/3, F1/0/4| Trunk
||F1/0/5| Vlan 120

# Étape 1 – Configuration des paramètres de base
a. Configurez les noms d’hôte (hostname)

c. Désactivez la résolution des noms de domaine

d. Désactivez le délai d’attente sur la console

e. Activez la synchronisation des messages de la console

# Étape 2 – Configuration des VLANs et assignation des ports du switch			
a. À l’aide des tableaux des VLANs et des ports, configurez les VLANs et les ports.

# Étape 3 – Configuration des adresses IP et du routage inter-VLAN
a. À l’aide du tableau d’adresses IP, configurez les adresses IP.

b. Configurez le routage inter-VLAN et attribuez la première adresse IP disponible de chaque réseau aux sous-interfaces du routeur RACK-F-R2

# Étape 4 – Configuration du routage statique et dynamique 
a. Configurez le routage OSPF sur tous les routeurs.

•   Utilisez le numéro de processus ID 1 et la zone 0.

•   Annoncez dans OSPF uniquement les réseaux connectés à chaque routeur, sauf le réseau qui mène vers SW-Internet.

•   Configurez les interfaces passives aux endroits appropriés.

b. Sur RACK-F-R1, configurez une route par défaut pointant vers SW-Internet en utilisant l’interface de sortie. Sur RACK-F-R1, utilisez la commande appropriée pour propager cette route par défaut à ses voisins OSPF.

# Étape 5 – Configuration du DHCP 
Le serveur DHCP est déjà configuré pour vous. Son adresse IP est la suivante : 192.168.60.200
Vous devez configurer IP Helper pour qu’il pointe vers ce serveur DHCP.

# Étape 6 – Configuration de SSH 					
a. Configurez SSH sur le routeur RACK-F-R1.

b. Définissez le nom de domaine à rack-f.local

c. Créez un utilisateur cisco avec le mot de passe cisco1234.

d. Créez une clé RSA 2048 bits.

e. Version 2

f. Paramétrez toutes les lignes vty 0 4 pour utiliser SSH et un login local

# Étape 7 – Configuration des ACL standards	
Écrire une ACL standard nommée ALLOW_SSH qui permettra seulement au RACK F-PC1 de faire une connexion SSH sur RACK-F-R1. Toute tentatives de connexion via SSH depuis tout autre périphérique doit échouer.

# Étape 8 – Configuration des ACL étendues

🔴 Avant de commencer les ACL, assurez-vous de faire les tests sur les deux PC. Par exemple :

🔴 Accéder à une page web en HTTP et HTTPS.

🔴 Vérifier que le DNS fonctionne correctement.

🔴 Essayer de vous connecter au serveur en utilisant [Telnet](../../documentation/telnet_connection.md) et [FTP](../../documentation/ftp_connection.md).

Écrire une ACL étendue nommée DROITS-PC qui donne les accès suivants: 

•	Pour RACK F-PC1: autorise le trafic Telnet (23), DNS (53), DHCP(67, 68), HTTP (80) et HTTPS (443) sur le serveur 192.168.60.200, tout autre trafic partant de RACK F-PC1 vers le serveur externe est refusé.

•	Pour RACK F-PC2: autorise le trafic FTP (20, 21) et DHCP(67, 68) sur le serveur 192.168.60.200.

•	Appliquer la ACL convenablement.

# Captures à remettre dans le pigeonnier

a. Faites la commande show vlan brief sur tous les switches.

b. Faites la commande show ip interface brief sur tous les routeurs.

c. Faites la commande show ip route sur tous les routeurs.

d. Faites la commande ipconfig sur les PC.

e. Faites la commande show ip access-list sur le routeur RACK-F-R2, on doit voir des (match).