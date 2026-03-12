# Laboratoire 8 - Configuration GRE, NAT, QoS 
# Topologie

![Topo](../../topo/rack-f/topo6.png)

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

# Étape 7 – Configuration NTP.

a.  Configurer les routeurs et les commutateurs afin qu’ils utilisent le serveur de votre rack (192.168.60.200) en tant que serveur NTP.

# Étape 8 – Configuration Syslog.

a.  Configurer les routeurs et les commutateurs afin qu’ils utilisent le serveur de votre rack (192.168.60.200) en tant que serveur Syslog.

# Étape 9 – Configuration des ACL étendues sur RACK-F-R1-MTL et RACK-F-R2-Ottawa

🔴 Avant de commencer les ACL, assurez-vous de faire les tests sur les deux PC. Par exemple :

🔴 Accéder à une page web www.rack-f.local en HTTP et HTTPS.

🔴 Vérifier que le DNS fonctionne correctement.

🔴 Essayer de vous connecter au serveur en utilisant [FTP](../../documentation/ftp_connection.md) et SSH

Écrire une ACL étendue nommée FIREWALL qui donne les accès suivants: 

•	Autorise le trafic FTP (ports 20 et 21), SSH (22), DNS (53), HTTPS (443) et NTP (123) provenant du serveur externe (192.168.60.200) à retourner.

•   Autorise le trafic GRE entre les routeurs.

•	Interdire tout autres trafics.

# Captures à remettre dans le pigeonnier

a. Vous devez effectuer un traceroute entre le PC RACK-F-PC1 et le PC RACK-F-PC2. Le trafic doit passer à travers le tunnel.

b. Vous devez effectuer un traceroute entre le PC RACK-F-PC1 et www.rack-f.local. Le trafic ne doit pas passer dans le tunnel (Avant d’appliquer l’ACL FIREWALL).

c. Vous devez effectuer un traceroute entre le PC RACK-F-PC2 et www.rack-f.local. Le trafic ne doit pas passer dans le tunnel (Avant d’appliquer l’ACL FIREWALL).

d. Exécuter la commande "show ip access-list" sur les routeurs RACK-F-R1-MTL et RACK-F-R2-Ottawa. On doit voir des match sur toutes les lignes.

e. Exécuter la commande "show ntp associations" sur les routeurs RACK-F-R1-MTL, RACK-F-R2-Ottawa, RACK-F-SW1-MTL et RACK-F-SW2-Ottawa. Vous devriez voir un résultat similaire à celui-ci.

![NTP](../../documentation/screenshots/6.png)

f. Connectez-vous au serveur et déplacez-vous dans le dossier suivant « /var/log/cisco ». Exécutez la commande « ls » pour voir les répertoires. Vous devriez voir un répertoire pour chaque routeur et pour chaque commutateur. Entrez dans les répertoires et utilisez la commande « cat » pour afficher les messages de log.