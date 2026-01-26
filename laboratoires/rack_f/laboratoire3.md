
# Laboratoire 3 - Configuration des ACL étendues, OSPF et NAT

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
|RACK-F-PC1|Fa0      |172.16.110.100       |255.255.255.0  | 172.16.110.1   |    |
|RACK-F-PC2|Fa0      |172.16.120.100       |255.255.255.0  | 172.16.120.1   |    |

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

# Étape 5 – Configuration du NAT
a.	Créer une liste d’accès standard nommée NAT pour permettre les réseaux du 
VLAN 110, du VLAN 120 et interdire tout autres réseaux.

b.	Créer un NAT pool nommée NAT-POOL entre les adresses 10.10.10.43 et 10.10.10.45.

c.	Créer un NAT statique pour le serveur RACK-F-PC1 avec l’adresse 10.10.10.46.

🔴 Test a effectuer avant de continuer: 

🔴 Connectez-vous en SSH au serveur 192.168.60.200 en utilisant l’utilisateur "user" et le mot de passe "cisco1234", puis essayez de pinguer le PC RACK-F-PC1.

🔴 Essayez ensuite de ping 8.8.8.8 à travers les PC. (Capture à remettre)

🔴 Essayez d’ouvrir la page Web google.ca. (Capture à remettre)

🔴 Si tous vos tests sont concluants, vous pouvez continuer avec les ACL étendues.

# Étape 6 – Configuration des ACL étendues	

🔴 Avant de commencer les ACL, assurez-vous de faire les tests sur les deux PC. Par exemple :

🔴 Accéder à une page web www.rack-f.local en HTTP et HTTPS.

🔴 Vérifier que le DNS fonctionne correctement.

🔴 Essayer de vous connecter au serveur en utilisant [Telnet](../../documentation/telnet_connection.md), [FTP](../../documentation/ftp_connection.md) et SSH

Écrire une ACL étendue nommée FIREWALL qui donne les accès suivants: 

•	Appliquer la ACL convenablement sur le routeur RACK-F-R1.

•	Autorise le retour du trafic FTP (ports 20 et 21), SSH (22), DNS (53), HTTPS (443) du serveur externe (192.168.60.200) au réseaux du VLAN110 et VLAN120.

•	Autorise les pings du serveur externe (192.168.60.200) vers le PC RACK-F-PC1.

•	Interdire tout autres trafics.

# Captures à remettre dans le pigeonnier

a. Exécuter la commande show ip access-list sur le routeur RACK-F-R2. On doit voir des match sur toutes les lignes.

b. Exécuter la commande show ip nat translations sur le routeur RACK-F-R1.