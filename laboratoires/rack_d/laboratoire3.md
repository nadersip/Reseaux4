
# Laboratoire 3 - Configuration des ACL étendues, OSPF, SSH et NAT

# Topologie

![Topo](../../topo/rack-d/topo1-4.png)

# Table d’adressage :

|Equipments|Interface     | IP Address     | Subnet Mask     | Default Gateway | Description
|----------|--------------|---------------|----------------|------------------|------------------|
|RACK-D-R1 |G0/0/1   |10.10.10.26       |255.255.255.248           | N/A|Connexion a internet via la switch
|          |G0/0/0   |10.0.0.17   |255.255.255.252| N/A|Connexion au routeur R2
|RACK-D-R2 |G0/0/1   |10.0.0.18   |255.255.255.252| N/A|Connexion au routeur R1
|          |G0/0/0.70|172.16.70.1|255.255.255.0  | N/A|Connexion au switch SW1 - VLAN 70
|          |G0/0/0.80|172.16.80.1|255.255.255.0  | N/A|Connexion au switch SW1 - VLAN 80
|RACK-D-PC1|Fa0      |DHCP       |DHCP  | DHCP   |    |
|RACK-D-PC2|Fa0      |DHCP       |DHCP  | DHCP   |    |

# Table VLAN
|Equipments|VLAN     | Nom VLAN    |
|----------|--------------|---------------|
|RACK-D-SW1, RACK-D-SW2 et RACK-D-SW3|VLAN 70| VLAN70
|          |VLAN 80| VLAN80
|          |VLAN 99| Mgmt_Native

# Table de ports
|Equipments|Ports |  |
|----------|-----|----------|
|RACK-D-SW1 |F1/0/1, F1/0/2, F1/0/3| Trunk
|RACK-D-SW2 |F1/0/2, F1/0/4| Trunk
||F1/0/5| Vlan 70
|RACK-D-SW3 |F1/0/3, F1/0/4| Trunk
||F1/0/5| Vlan 80

# Étape 1 – Configuration des paramètres de base
a. Configurez les noms d’hôte (hostname)

c. Désactivez la résolution des noms de domaine

d. Désactivez le délai d’attente sur la console

e. Activez la synchronisation des messages de la console

# Étape 2 – Configuration des VLANs et assignation des ports du switch			
a. À l’aide des tableaux des VLANs et des ports, configurez les VLANs et les ports.

# Étape 3 – Configuration des adresses IP et du routage inter-VLAN
a. À l’aide du tableau d’adresses IP, configurez les adresses IP.

b. Configurez le routage inter-VLAN et attribuez la première adresse IP disponible de chaque réseau aux sous-interfaces du routeur RACK-D-R2

# Étape 4 – Configuration du routage statique et dynamique 
a. Configurez le routage OSPF sur tous les routeurs.

•   Utilisez le numéro de processus ID 1 et la zone 0.

•   Annoncez dans OSPF uniquement les réseaux connectés à chaque routeur, sauf le réseau qui mène vers SW-Internet.

•   Configurez les interfaces passives aux endroits appropriés.

b. Sur RACK-D-R1, configurez une route par défaut pointant vers SW-Internet en utilisant l’interface de sortie. Sur RACK-D-R1, utilisez la commande appropriée pour propager cette route par défaut à ses voisins OSPF.

# Étape 5 – Configuration du DHCP 
Le serveur DHCP est déjà configuré pour vous. Son adresse IP est la suivante : 192.168.40.200
Vous devez configurer IP Helper pour qu’il pointe vers ce serveur DHCP.

# Étape 6 – Configuration de SSH 					
a. Configurez SSH sur le routeur RACK-D-R1.

b. Définissez le nom de domaine à rack-d.local

c. Créez un utilisateur cisco avec le mot de passe cisco1234.

d. Créez une clé RSA 2048 bits.

e. Version 2

f. Paramétrez toutes les lignes vty 0 4 pour utiliser SSH et un login local

# Étape 7 – Configuration du NAT
a.	Créer une liste d’accès standard nommée NAT pour permettre les réseaux du 
VLAN 70, du VLAN 80 et interdire tout autres réseaux.

b.	Créer un NAT pool nommée NAT-POOL entre les adresses 10.10.10.27 et 10.10.10.29.

c.	Créer un NAT statique pour le serveur RACK-D-PC1 avec l’adresse 10.10.10.30.

d.	Tester le NAT avant de continuer.

# Étape 8 – Configuration des ACL étendues	
Écrire une ACL étendue nommée FIREWALL qui donne les accès suivants: 

•	Appliquer la ACL convenablement sur le routeur RACK-D-R1.

•	Autorise le retour du trafic FTP (ports 20 et 21), DNS (53), HTTPS (443) du serveur externe (192.168.40.200) au réseaux privés.

•	Autorise les pings du serveur externe (192.168.40.200) vers le serveur RACK-D-PC1.

•	Interdire tout autres trafics.