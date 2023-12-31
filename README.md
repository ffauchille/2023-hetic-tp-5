# TP#5: Images docker et docker compose

**Ojbectifs**: 

- créer les images pour les différents processus d'hetic tac toe:
  - **frontend**: la partie du code écrite en ReactJS
  - **backend**: la partie du code écrite en Python
- utiliser le plugin [**docker compose**](https://docs.docker.com/compose/) pour lancer les manipuler les conteneurs

## Étape 1: Les commandes principales des images Docker

Un conteneur Docker est **toujours** run (lancé) à partir d'une **image**. 

> Note: Si l'on fait un parallèle avec la programmation orienté objet, l'**image** est la `class` et le conteneur est une 
> **instance** de cette `class`

Vous pouvez lister les images présentent sur votre hôte Docker via la commande:

```sh
docker image ls
```

Vous pouvez utiliser des images Docker qui sont hébergées sur une *registry* Docker publique: [Docker hub](https://hub.docker.com/).
Docker hub fournit une solution simple qui permet de partager gratuitement des images docker **publiques**.
Si vous souhaitez utiliser des images docker privées (non ouverte à tous), vous pouvez créer un compte sur docker hub ou utiliser d'autre
*registry* docker.

> Note: Github fournit une *registry* Docker: [ghcr pour **G**it**H**ub **C**ontainer **R**egistry](https://docs.github.com/fr/packages/working-with-a-github-packages-registry/working-with-the-container-registry)

Les commandes `docker image pull` et `docker image push` vous permette de respectivement récupérer et envoyer des images docker depuis
votre poste de travail vers une *registry* Docker.

Par défaut, votre hôte Docker est configuré pour récupérer des images sur Docker hub.

Vous pouvez récupérer une image ubuntu via la commande:

```sh
docker image pull ubuntu:latest
```

Cette commande va récupérer la dernière image d'ubuntu qui a été `push` (envoyée) sur Docker hub.
Vous pouvez trouver les détails de cette image sur [la page de l'image ubuntu sur Docker hub](https://hub.docker.com/_/ubuntu).

Le mot `latest` est une convention qui permet de récupérer l'image ubuntu avec le `tag` le plus récent.

Sur la page [la page de l'image ubuntu sur Docker hub](https://hub.docker.com/_/ubuntu), vous pouvez naviger sur l'onglet `Tags` et 
récupérer une version spécific d'ubuntu pour votre application.

Par exemple, la commande suivant va récupérer l'image `ubuntu` taggée `24.04`:

```sh
docker image pull ubuntu:24.04
```

Vous pouvez supprimer l'image de votre poste de travail en tapant la commande:

```sh
docker image rm ubuntu:24.04
```

L'avantage de supprimer une image est d'économiser de l'espace de disque sur votre hôte Docker.

## Étape 2: Créer les images pour hetic tac toe

Docker vous offre deux options pour créer vos images:

1. via la commande `docker container commit`
1. via la commande `docker image build` et un fichier `Dockerfile`

La première option n'est pas recommandée et n'est utiliser que dans des cas très spécifiques.

Nous allons uniquement nous intéresser à la seconde option en écrivant nos fichier `Dockerfile` puis en utilisant la commande `docker image build`.

C'est l'option recommandée pour créer les images Docker pour vos applications.

### Dockerfile

