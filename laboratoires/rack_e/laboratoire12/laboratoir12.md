# Laboratoire 11 - Configuration GRE, OSPF, NAT, SNMP, ACL et TFTP
# Topologie

![Topo](../../topo/rack-e/topo6.png)

# Table d’adressage :

|Equipments|Interface     | IP Address     | Subnet Mask     | Default Gateway | Description
|----------|--------------|---------------|----------------|------------------|------------------|
|ISP |G1/0/1   |10.10.10.34       |255.255.255.248         | N/A|Connexion a internet 
|          |G1/0/2   |10.0.0.37   |255.255.255.252| N/A|Connexion a RACK-E-R1-MTL
|          |G1/0/3   |10.0.0.41   |255.255.255.252| N/A|Connexion a RACK-E-R2-Ottawa
|RACK-E-R1-MTL |G0/0/1   |10.0.0.38       |255.255.255.252           | N/A|Connexion a ISP
|          |G0/0/0   |172.16.90.1   |255.255.255.0| N/A|Connexion au switch RACK E-SW-MTL
|          |Tunnel 1   |172.16.105.1   |255.255.255.252| N/A|Connexion Tunnel au RACK-E-R2-Ottawa
|RACK-E-R2-Ottawa |G0/0/1   |10.0.0.42   |255.255.255.252| N/A|Connexion a ISP
|          |G0/0/0|172.16.100.1|255.255.255.0  | N/A|Connexion au switch RACK E-SW-Ottawa
|          |Tunnel 1   |172.16.105.2   |255.255.255.252| N/A|Connexion Tunnel au RACK-E-R1-MTL
|RACK-A-SW1-MTL |SVI  |172.16.90.2   |255.255.255.0| 172.16.90.1|
|RACK-A-SW2-Ottawa |SVI  |172.16.100.2   |255.255.255.0| 172.16.100.1|
|RACK-E-PC1|Fa0      |172.16.90.100       |255.255.255.0  | 172.16.90.1   |    |
|RACK-E-PC2|Fa0      |172.16.100.100       |255.255.255.0  | 172.16.100.1   |    |

Note: utiliser le serveur 192.168.50.200 pour DNS

# Étape 1 – Configuration des paramètres de base
a. Configurez les noms d’hôte (hostname)

# Étape 2 – Configuration des adresses IP
a. À l’aide du tableau d’adresses IP, configurez les adresses IP.

# Étape 3 – Configuration du routage statique
a. Sur ISP, configurez une route par défaut route entièrement spécifiée pointant vers SW-Internet.

b. Sur RACK-E-R1-MTL, configurez une route par défaut route entièrement spécifiée pointant vers ISP.

c. Sur RACK-E-R2-Ottawa, configurez une route par défaut route entièrement spécifiée pointant vers ISP.

# Étape 4 – Configuration du tunnel GRE
a. Configurer le tunnel GRE entre les routeurs RACK-E-R1-MTL et RACK-E-R2-Ottawa

# Étape 5 – Configuration du routage dynamique 
a. Configurez le routage OSPF sur tous les routeurs RACK-E-R1-MTL et RACK-E-R2-Ottawa.

•   Utilisez le numéro de processus ID 1 et la zone 0.

•   Annoncez dans OSPF uniquement les réseaux connectés, sauf les réseaux qui mène vers ISP.

•   Configurez les interfaces passives aux endroits appropriés.

# Étape 6 – Configuration du NAT sur RACK-E-R1-MTL et RACK-E-R2-Ottawa
a.	Créer une liste d’accès standard nommée NAT sur RACK-E-R1-MTL pour permettre le réseau
172.16.90.0/24 et interdire tout autres réseaux.

b.	Configurer le NAT avec PAT sur l'interface de sortie de RACK-E-R1-MTL.

a.	Créer une liste d’accès standard nommée NAT sur RACK-E-R2-Ottawa pour permettre le réseau
172.16.100.0/24 et interdire tout autres réseaux.

b.	Configurer le NAT avec PAT sur l'interface de sortie de RACK-E-R2-Ottawa.

d.	Tester le NAT avant de continuer.

# Étape 7 – Configuration SNMP

a. Configurer une communauté read-only nommée "rack-e" sur les routeurs RACK-E-R1-MTL et RACK-E-R2-Ottawa.

b. Configurer le serveur Zabbix pour se connecter aux routeurs RACK-E-R1-MTL et RACK-E-R2-Ottawa. Suivre la documentation [SNMP](../../documentation/snmp_client.md).

# Étape 8 – Configuration des ACL étendues sur RACK-E-R1-MTL et RACK-E-R2-Ottawa

🔴 Avant de commencer les ACL, assurez-vous de faire les tests sur les deux PC. Par exemple :

🔴 Accéder à une page web www.rack-e.local en HTTP et HTTPS.

🔴 Accéder à une page web google.com en HTTP et HTTPS.

🔴 Vérifier que le DNS fonctionne correctement.

🔴 Essayer de vous connecter au serveur en utilisant [FTP](../../documentation/ftp_connection.md) et SSH

Écrire une ACL étendue nommée ACL-LAN-TO-WAN qui donne les accès suivants: 

•	Autoriser le trafic FTP (ports 20 et 21), SSH (22), DNS (53), HTTPS (443), HTTP (80) et TFTP (69) provenant des réseaux locaux vers le serveur externe (192.168.50.200).

•	Autoriser le trafic HTTPS (443) et HTTP (80) provenant des réseaux locaux vers n’importe quelle destination.

•	Autorise le trafic HTTPS (443) et HTTP (80) provenant des reseaux loceau vers n'import quelle destination.

•	Refuser le trafic HTTP (80) provenant des réseaux locaux vers le serveur hackme.computcenter.ca.

•	Interdire tout autres trafics.

# Étape 9 – Sauvegarde des configurations sur le serveur TFTP

a. Effectuer la sauvegarde des configurations des routeurs et des commutateurs vers le serveur TFTP (192.168.50.200).

# Captures à remettre dans le pigeonnier

a. Vous devez effectuer un traceroute entre le PC RACK-E-PC1 et le PC RACK-E-PC2. Le trafic doit passer à travers le tunnel.

b. Vous devez effectuer un traceroute entre le PC RACK-E-PC1 et www.rack-e.local
. Le trafic ne doit pas passer dans le tunnel.

c. Vous devez effectuer un traceroute entre le PC RACK-E-PC2 et www.rack-e.local
. Le trafic ne doit pas passer dans le tunnel.

d. Ouvrir www.google.com
 dans le navigateur web sur RACK-E-PC1. Vous devez être capable d’ouvrir cette page.

e. Ouvrir www.google.com
 dans le navigateur web sur RACK-E-PC2. Vous devez être capable d’ouvrir cette page.

f. Ouvrir hackme.computcenter.ca dans le navigateur web sur RACK-E-PC1. Vous ne devez pas être capable d’ouvrir cette page.

g. Ouvrir hackme.computcenter.ca dans le navigateur web sur RACK-E-PC2. Vous ne devez pas être capable d’ouvrir cette page.

h. Prenez une capture d’écran de la page web de Zabbix montrant vos appareils qui ont été ajoutés.

i. Connectez-vous au serveur 192.168.50.200 en SSH, puis déplacez-vous dans le dossier « /backup ». Exécutez la commande « ls » pour voir les configurations de chaque routeur et switch. Exécutez ensuite un « cat » sur un des fichiers afin de vérifier les configurations.

    Utilisez les identifiants suivants :
    
    • Nom d’utilisateur : user

    • Mot de passe : cisco1234

j. Exécuter la commande "show ip access-lists" sur les routeurs RACK-E-R1-MTL et RACK-E-R2-Ottawa. Vous devez voir des correspondances (matches) sur toutes les lignes.