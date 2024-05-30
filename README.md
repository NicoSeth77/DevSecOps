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

Sur le Fedora CoreOs :




Sur le Debian :

```bash
sudo apt-add-repository ppa:ansible/ansible
sudo apt update
sudo apt install ansible
```

Pour cloner la repertoire 

```bash
git clone https://github.com/NicoSeth77/DevSecOps
```



