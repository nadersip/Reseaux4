# Laboratoire 12 - Configuration GRE, OSPF, NAT, SNMP, ACL et TFTP
# Topologie

![Topo](../../../topo/rack-f/topo6.png)

# Table d’adressage :

|Equipments|Interface     | IP Address     | Subnet Mask     | Default Gateway | Description
|----------|--------------|---------------|----------------|------------------|------------------|
|ISP |G1/0/1   |10.10.10.42       |255.255.255.248         | N/A|Connexion a internet 
|          |G1/0/2   |10.0.0.45   |255.255.255.252| N/A|Connexion a RACK-F-R1-MTL
|          |G1/0/3   |10.0.0.49   |255.255.255.252| N/A|Connexion a RACK-F-R2-Ottawa
|RACK-F-R1-MTL |G0/0/1   |10.0.0.46       |255.255.255.252           | N/A|Connexion a ISP
|          |G0/0/0   |172.16.110.1   |255.255.255.0| N/A|Connexion au switch RACK F-SW-MTL
|          |Tunnel 1   |172.16.125.1   |255.255.255.252| N/A|Connexion Tunnel au RACK-F-R2-Ottawa
|RACK-F-R2-Ottawa |G0/0/1   |10.0.0.50   |255.255.255.252| N/A|Connexion a ISP
|          |G0/0/0|172.16.120.1|255.255.255.0  | N/A|Connexion au switch RACK F-SW-Ottawa
|          |Tunnel 1   |172.16.125.2   |255.255.255.252| N/A|Connexion Tunnel au RACK-F-R1-MTL
|RACK-F-SW1-MTL |SVI  |172.16.110.2   |255.255.255.0| 172.16.110.1|
|RACK-F-SW2-Ottawa |SVI  |172.16.120.2   |255.255.255.0| 172.16.120.1|
|RACK-F-PC1|Fa0      |172.16.110.100       |255.255.255.0  | 172.16.110.1   |    |
|RACK-F-PC2|Fa0      |172.16.120.100       |255.255.255.0  | 172.16.120.1   |    |

Note: utiliser le serveur 192.168.60.200 pour DNS

# Étape 1 – Configuration des paramètres de base
a. Configurez les noms d’hôte (hostname)

# Étape 2 – Configuration des adresses IP
a. À l’aide du tableau d’adresses IP, configurez les adresses IP.

# Étape 3 – Configuration du routage statique
a. Sur ISP, configurez une route par défaut route entièrement spécifiée pointant vers SW-Internet.

b. Sur RACK-F-R1-MTL, configurez une route par défaut route entièrement spécifiée pointant vers ISP.

c. Sur RACK-F-R2-Ottawa, configurez une route par défaut route entièrement spécifiée pointant vers ISP.

# Étape 4 – Configuration du tunnel GRE
a. Configurer le tunnel GRE entre les routeurs RACK-F-R1-MTL et RACK-F-R2-Ottawa

# Étape 5 – Configuration du routage dynamique 
a. Configurez le routage OSPF sur tous les routeurs RACK-F-R1-MTL et RACK-F-R2-Ottawa.

•   Utilisez le numéro de processus ID 1 et la zone 0.

•   Annoncez dans OSPF uniquement les réseaux connectés, sauf les réseaux qui mène vers ISP.

•   Configurez les interfaces passives aux endroits appropriés.

# Étape 6 – Configuration du NAT sur RACK-F-R1-MTL et RACK-F-R2-Ottawa
a.	Créer une liste d’accès standard nommée NAT sur RACK-F-R1-MTL pour permettre le réseau
172.16.110.0/24 et interdire tout autres réseaux.

b.	Configurer le NAT avec PAT sur l'interface de sortie de RACK-F-R1-MTL.

a.	Créer une liste d’accès standard nommée NAT sur RACK-F-R2-Ottawa pour permettre le réseau
172.16.120.0/24 et interdire tout autres réseaux.

b.	Configurer le NAT avec PAT sur l'interface de sortie de RACK-F-R2-Ottawa.

d.	Tester le NAT avant de continuer.

# Étape 7 – Configuration SNMP

a. Configurer une communauté read-only nommée "rack-f" sur les routeurs RACK-F-R1-MTL et RACK-F-R2-Ottawa.

b. Configurer le serveur Zabbix pour se connecter aux routeurs RACK-F-R1-MTL et RACK-F-R2-Ottawa. Suivre la documentation [SNMP](../../documentation/snmp_client.md).

# Étape 8 – Configuration des ACL étendues sur RACK-F-R1-MTL et RACK-F-R2-Ottawa

🔴 Avant de commencer les ACL, assurez-vous de faire les tests sur les deux PC. Par exemple :

🔴 Accéder à une page web www.rack-f.local en HTTP et HTTPS.

🔴 Accéder à une page web google.com en HTTP et HTTPS.

🔴 Vérifier que le DNS fonctionne correctement.

🔴 Essayer de vous connecter au serveur en utilisant [FTP](../../documentation/ftp_connection.md) et SSH

Écrire une ACL étendue nommée ACL-LAN-TO-WAN qui donne les accès suivants: 

•	Autoriser le trafic FTP (ports 20 et 21), SSH (22), DNS (53), HTTPS (443), HTTP (80) et TFTP (69) provenant des réseaux locaux vers le serveur externe (192.168.60.200).

•	Autoriser le trafic HTTPS (443) et HTTP (80) provenant des réseaux locaux vers n’importe quelle destination.

•	Autorise le trafic HTTPS (443) et HTTP (80) provenant des reseaux loceau vers n'import quelle destination.

•	Refuser le trafic HTTP (80) provenant des réseaux locaux vers le serveur hackme.computcenter.ca.

•	Interdire tout autres trafics.

# Étape 9 – Sauvegarde des configurations sur le serveur TFTP

a. Effectuer la sauvegarde des configurations des routeurs et des commutateurs vers le serveur TFTP (192.168.60.200).

# Captures à remettre dans le pigeonnier

a. Vous devez effectuer un traceroute entre le PC RACK-F-PC1 et le PC RACK-F-PC2. Le trafic doit passer à travers le tunnel.

b. Vous devez effectuer un traceroute entre le PC RACK-F-PC1 et www.rack-f.local
. Le trafic ne doit pas passer dans le tunnel.

c. Vous devez effectuer un traceroute entre le PC RACK-F-PC2 et www.rack-f.local
. Le trafic ne doit pas passer dans le tunnel.

d. Ouvrir www.google.com
 dans le navigateur web sur RACK-F-PC1. Vous devez être capable d’ouvrir cette page.

e. Ouvrir www.google.com
 dans le navigateur web sur RACK-F-PC2. Vous devez être capable d’ouvrir cette page.

f. Ouvrir hackme.computcenter.ca dans le navigateur web sur RACK-F-PC1. Vous ne devez pas être capable d’ouvrir cette page.

g. Ouvrir hackme.computcenter.ca dans le navigateur web sur RACK-F-PC2. Vous ne devez pas être capable d’ouvrir cette page.

h. Prenez une capture d’écran de la page web de Zabbix montrant vos appareils qui ont été ajoutés.

i. Connectez-vous au serveur 192.168.60.200 en SSH, puis déplacez-vous dans le dossier « /backup ». Exécutez la commande « ls » pour voir les configurations de chaque routeur et switch. Exécutez ensuite un « cat » sur un des fichiers afin de vérifier les configurations.

    Utilisez les identifiants suivants :
    
    • Nom d’utilisateur : user

    • Mot de passe : cisco1234

j. Exécuter la commande "show ip access-lists" sur les routeurs RACK-F-R1-MTL et RACK-F-R2-Ottawa. Vous devez voir des correspondances (matches) sur toutes les lignes.