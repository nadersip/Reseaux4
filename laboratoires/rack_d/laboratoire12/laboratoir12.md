# Laboratoire 12 - Automatisation
# Topologie

![Topo](../../../topo/rack-d/topo12.png)

# Table d’adressage :

|Equipments|Interface     | IP Address     | Subnet Mask     | Default Gateway | Description
|----------|--------------|---------------|----------------|------------------|------------------|
|ISP |G1/0/1   |10.10.10.26       |255.255.255.248         | N/A|Connexion a internet 
|          |G1/0/2   |10.0.0.29   |255.255.255.252| N/A|Connexion a RACK-D-R1-MTL
|          |G1/0/3   |10.0.0.33   |255.255.255.252| N/A|Connexion a RACK-D-R2-Ottawa
|RACK-D-R1-MTL |G0/0/1   |10.0.0.30       |255.255.255.252           | N/A|Connexion a ISP
|          |G0/0/0   |172.16.70.1   |255.255.255.0| N/A|Connexion au switch RACK D-SW-MTL
|          |Tunnel 1   |172.16.85.1   |255.255.255.252| N/A|Connexion Tunnel au RACK-D-R2-Ottawa
|RACK-D-R2-Ottawa |G0/0/1   |10.0.0.34   |255.255.255.252| N/A|Connexion a ISP
|          |G0/0/0|172.16.80.1|255.255.255.0  | N/A|Connexion au switch RACK D-SW-Ottawa
|          |Tunnel 1   |172.16.85.2   |255.255.255.252| N/A|Connexion Tunnel au RACK-D-R1-MTL
|RACK-D-PC1|Fa0      |172.16.70.100       |255.255.255.0  | 172.16.70.1   |    |
|RACK-D-PC2|Fa0      |172.16.80.100       |255.255.255.0  | 172.16.80.1   |    |

Note: utiliser le serveur 192.168.40.200 pour DNS

# Étape 1 – Configuration des paramètres de base
a. Configurez les noms d’hôte (hostname)

b. Configurez le mot de passe « class » pour le mode privilégié.

# Étape 2 – Configuration des adresses IP
a. À l’aide du tableau d’adresses IP, configurez les adresses IP de ISP.

b. À l’aide du tableau d’adresses IP, configurez uniquement les adresses IP sur l’interface G0/0/1 des routeurs RACK-D-R1-MTL et RACK-D-R2-Ottawa.

# Étape 3 – Configuration du routage statique
a. Sur ISP, configurez une route par défaut route entièrement spécifiée pointant vers SW-Internet.

b. Sur RACK-D-R1-MTL, configurez une route par défaut route entièrement spécifiée pointant vers ISP.

c. Sur RACK-D-R2-Ottawa, configurez une route par défaut route entièrement spécifiée pointant vers ISP.

# Étape 4 – Configurez SSH sur le routeur RACK-D-R1-MTL et RACK-D-R2-Ottawa.

a. Définissez le nom de domaine à rack-d.local

b. Créez un utilisateur « user » avec le mot de passe « cisco1234 ».

c. Créez une clé RSA 2048 bits.

d. Version 2

e. Paramétrez toutes les lignes vty 0 4 pour utiliser SSH et un login local

# Étape 5 – Automatisation des tâches

a. À l’aide du RACK-D-PC3, connectez-vous au serveur 192.168.40.200 en SSH en utilisant le nom d’utilisateur « user » et le mot de passe « cisco1234 ».

🔴 Avant de lancer les scripts, essayez de vous connecter en SSH depuis le serveur vers les routeurs.

b. Exécutez la commande suivante pour télécharger le dépôt GitHub sur le serveur.

git clone https://github.com/nadersip/Reseaux4.git

c. Déplacez-vous dans le répertoire Reseaux4/laboratoires/rack_d/laboratoire12.

d. Exécutez la commande suivante pour configurer le routeur RACK-D-R1-MTL.

ansible-playbook config_rack_d_r1_mtl.yaml -i inventory.ini

e. Exécutez la commande suivante pour configurer le routeur RACK-D-R2-Ottawa.

ansible-playbook config_rack_d_r2_ottawa.yaml -i inventory.ini

🔴 Exécutez la commande show run pour vous assurer que les configurations sont bien présentes sur les routeurs.

# Étape 6 – Configuration SNMP
a. Configurer le serveur Zabbix pour se connecter aux routeurs RACK-D-R1-MTL et RACK-D-R2-Ottawa. Suivre la documentation [SNMP](../../documentation/snmp_client.md).

# Étape 7 – Sauvegarde des configurations sur le serveur TFTP

a. Effectuer la sauvegarde des configurations des routeurs vers le serveur TFTP (192.168.40.200).

# Captures à remettre dans le pigeonnier

a. Vous devez effectuer un traceroute entre le PC RACK-D-PC1 et le PC RACK-D-PC2. Le trafic doit passer à travers le tunnel.

b. Vous devez effectuer un traceroute entre le PC RACK-D-PC1 et www.rack-d.local. Le trafic ne doit pas passer dans le tunnel.

c. Vous devez effectuer un traceroute entre le PC RACK-D-PC2 et www.rack-d.local. Le trafic ne doit pas passer dans le tunnel.

d. Ouvrir www.google.com dans le navigateur web sur RACK-D-PC1. Vous devez être capable d’ouvrir cette page.

e. Ouvrir www.google.com dans le navigateur web sur RACK-D-PC2. Vous devez être capable d’ouvrir cette page.

f. Ouvrir hackme.computcenter.ca dans le navigateur web sur RACK-D-PC1. Vous ne devez pas être capable d’ouvrir cette page.

g. Ouvrir hackme.computcenter.ca dans le navigateur web sur RACK-D-PC2. Vous ne devez pas être capable d’ouvrir cette page.

h. Prenez une capture d’écran de la page web de Zabbix montrant vos appareils qui ont été ajoutés.

i. Connectez-vous au serveur 192.168.40.200 en SSH, puis déplacez-vous dans le dossier « /backup ». Exécutez la commande « ls » pour voir les configurations de chaque routeur et switch. Exécutez ensuite un « cat » sur un des fichiers afin de vérifier les configurations.

    Utilisez les identifiants suivants :
    
    • Nom d’utilisateur : user

    • Mot de passe : cisco1234

j. Exécuter la commande "show ip access-lists" sur les routeurs RACK-D-R1-MTL et RACK-D-R2-Ottawa. Vous devez voir des correspondances (matches) sur toutes les lignes.

