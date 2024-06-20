# Contexte

Pour être agile, les entreprises s'orientent vers le concept de DevOps voire DevSecOps pour raccourcir le cycle de déploiement, de mise à jour des applications/services en mettant en place des outils adaptés comme CI/CD (Continuous Integration/Continuous Deploiement), IaC (Infrastructure as Code)...  

La mise en place d'une «Usine DevSecOps » ( DevSecOps Factory) permet aux entreprises de migrer des applications traditionnelles vers des applications conteneurisées pour optimiser les ressources et préparer la migration vers les micro-services. 

Le projet consiste à :

- Réaliser rapidement une étude sur le principe de fonctionnement du concept DevSecOps et les outils associés, 
- Étudier, préparer et déployer une usine de production DevSecOps, 
- Industrialiser le déploiement des usines DevSecOps à l’aide des outils IaC. 

# Ansible

Ansible est un moteur d'automatisation IT open source qui automatise le provisionnement, la gestion de la configuration, le déploiement d'applications, l'orchestration et de nombreux autres processus IT. Il est gratuit et le projet bénéficie de l'expérience et de l'intelligence de ses milliers de contributeurs. 

# Docker 

Docker est une plateforme open-source qui permet aux développeurs de créer, déployer, exécuter, mettre à jour et gérer des conteneurs. Les conteneurs sont des paquets logiciels standardisés qui regroupent le code d'une application, ses dépendances et les bibliothèques système nécessaires pour son exécution, garantissant ainsi qu'elle s'exécutera de manière cohérente quel que soit l'environnement.

# Fedora 

Fedora est une distribution Linux libre et open-source, développée par une communauté de passionnés et sponsorisée par Red Hat. Elle est connue pour son approche à la pointe de la technologie, intégrant souvent de nouvelles fonctionnalités et des logiciels innovants avant les autres distributions.

Notre environemment :

- Serveur Proxmox :
    - VM Fedora CoreOs : 192.168.10.209
    - VM Debian : 192.168.10.207

# Installation

Création de la VM Fedora CoreOS:


•	Installation et configuration initial : Fedora CoreOS nécessite une approche différente dans sa mise en place, par rapport à un système d’exploitation plus populaire (Debian, Windows, Kali...)

•	Il faut tout d’abord télécharger l’image de l’OS : https://fedoraproject.org/fr/coreos/download?stream=stable

•	Une fois l’image montée et démarrée il faut configurer un fichier de configuration initial appeler un fichier d’ignition sur un poste différent, comme suit :

•	Pour pouvoir récupérer le fichier sur le serveur Fedora CoreOs un des moyens le plus simple est d’utiliser un serveur Python3 sur la machine qui contient le ficher (Il faut donc avoir Python3 installé sur cette dernière) :
python3 -m http.server (Cette commande doit être utilisée une fois dans le repertoire ou se trouve le fichier que l’on souhaite partager)
•	Une fois le fichier créer il faudra le récupérer sur le serveur Fedora CoreOs via une requête Curl :
curl -O adresseipdelamachine:8000/chemin/fichier_d_ignition.ign

•	Une fois le fichier récupéré il ne reste qu’a installer ce fichier de configuration sur le serveur Fedora CoreOS :
sudo coreos-installer install /dev/sda --ignition-file fichier_d_ignition.ign

•	Une fois l’installation terminé on éteint la machine :
poweroff

•	Avant de relancer la machine il faut bien penser à démonter l’image depuis le contrôleur de virtualisation sinon la VM se lancera automatiquement dessus au lieu de charger la nouvelle configuration. Une fois cela fait on peut relancer la machine.

Sur le Fedora CoreOs :

- docker
- ssh


Sur le Debian :

```bash
sudo apt-add-repository ppa:ansible/ansible
sudo apt update
sudo apt install ansible
```

Pour cloner le repertoire 

```bash
sudo apt install git
git clone https://github.com/NicoSeth77/DevSecOps
```

Le fichier __hosts.ini__ spécifie les hôtes cibles ainsi que les ports pour le déploiement :

__192.168.10.207 ansible_user=utec ansible_ssh_private_key_file=/home/utec/.ssh/id_rsa__

- IP de la machine cible
- ansible_user correspond à l'utilisateur du Debian
- ansible_ssh_private_key_file correspond à la clé privée sur le Fedora CoreOs

Le fichier __deploy-docker.yml__ contient des tâches telles que la sélection d'images Docker, les noms de conteneurs, les ports, etc.
Dans ce fichier nous avons mis plusieurs conteneurs :
- Wireshark sur le port 3000 --> 192.168.10.207:3000
- Grafana sur le port 4000 --> 192.168.10.207:4000 
- MariaDB sur le port 5000 --> 192.168.10.207:5000
- Jenkins sur le port 8000 --> 192.168.10.207:8000

Execution du Ansible playbook pour deployer le conteneur Docker :

```bash
ansible-playbook -i hosts.ini deploy-docker.yml
```

Sur Fedora, vérification si le conteneur est bien créé :

```bash
docker ps
```


