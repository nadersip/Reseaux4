
# Laboratoire 6 - Configuration GRE, NAT, SSH 
# Topologie

![Topo](../../topo/rack-a/topo6.png)

# Table d’adressage :

|Equipments|Interface     | IP Address     | Subnet Mask     | Default Gateway | Description
|----------|--------------|---------------|----------------|------------------|------------------|
|ISP |G1/0/1   |10.10.10.2       |255.255.255.248         | N/A|Connexion a internet 
|          |G1/0/2   |10.0.0.5   |255.255.255.252| N/A|Connexion a RACK-A-R1-MTL
|          |G1/0/3   |10.0.0.9   |255.255.255.252| N/A|Connexion a RACK-A-R2-Ottawa
|RACK-A-R1-MTL |G0/0/1   |10.0.0.6       |255.255.255.252           | N/A|Connexion a ISP
|          |G0/0/0   |172.16.10.1   |255.255.255.0| N/A|Connexion au switch RACK A-SW-MTL
|          |Tunnel 1   |172.16.25.1   |255.255.255.252| N/A|Connexion Tunnel au RACK-A-R2-Ottawa
|RACK-A-R2-Ottawa |G0/0/1   |10.0.0.10   |255.255.255.252| N/A|Connexion a ISP
|          |G0/0/0|172.16.20.1|255.255.255.0  | N/A|Connexion au switch RACK A-SW-Ottawa
|          |Tunnel 1   |172.16.25.2   |255.255.255.252| N/A|Connexion Tunnel au RACK-A-R1-MTL
|RACK-A-PC1|Fa0      |172.16.10.100       |255.255.255.0  | 172.16.10.1   |    |
|RACK-A-PC2|Fa0      |172.16.20.100       |255.255.255.0  | 172.16.20.1   |    |

Note: utiliser le serveur 192.168.10.200 pour DNS

# Étape 1 – Configuration des paramètres de base
a. Configurez les noms d’hôte (hostname)

# Étape 2 – Configuration des adresses IP
a. À l’aide du tableau d’adresses IP, configurez les adresses IP.

# Étape 3 – Configuration du routage statique
a. Sur ISP, configurez une route par défaut route entièrement spécifiée pointant vers SW-Internet.

b. Sur RACK-A-R1-MTL, configurez une route par défaut route entièrement spécifiée pointant vers ISP.

c. Sur RACK-A-R2-Ottawa, configurez une route par défaut route entièrement spécifiée pointant vers ISP.

# Étape 4 – Configuration du tunnel GRE
a. Configurer le tunnel GRE entre les routeurs RACK-A-R1-MTL et RACK-A-R2-Ottawa

# Étape 5 – Configuration du routage dynamique 
a. Configurez le routage OSPF sur tous les routeurs RACK-A-R1-MTL et RACK-A-R2-Ottawa.

•   Utilisez le numéro de processus ID 1 et la zone 0.

•   Annoncez dans OSPF uniquement les réseaux connectés, sauf les réseaux qui mène vers ISP.

•   Configurez les interfaces passives aux endroits appropriés.

# Étape 6 – Configuration du NAT sur RACK-A-R1-MTL et RACK-A-R2-Ottawa
a.	Créer une liste d’accès standard nommée NAT sur RACK-A-R1-MTL pour permettre le réseau
172.16.10.0/24 et interdire tout autres réseaux.

b.	Configurer le NAT avec PAT sur l'interface de sortie de RACK-A-R1-MTL.

a.	Créer une liste d’accès standard nommée NAT sur RACK-A-R2-Ottawa pour permettre le réseau
172.16.20.0/24 et interdire tout autres réseaux.

b.	Configurer le NAT avec PAT sur l'interface de sortie de RACK-A-R2-Ottawa.

d.	Tester le NAT avant de continuer.

# Captures à remettre dans le pigeonnier

a. Vous devez effectuer un traceroute entre le PC RACK-A-PC1 et le PC RACK-A-PC2. Le trafic doit passer à travers le tunnel.

b. Vous devez effectuer un traceroute entre le PC RACK-A-PC1 et google.com. Le trafic ne doit pas passer dans le tunnel.

c. Vous devez effectuer un traceroute entre le PC RACK-A-PC2 et google.com. Le trafic ne doit pas passer dans le tunnel.