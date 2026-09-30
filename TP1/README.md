# TP 1

## Étape 1
1. Expliquez, avec vos propres mots, ce qu’est une machine virtuelle.

Il s'agit d'une machine émulée par un hyperviseur qui a ses propres ressources virtuelles (CPU, RAM, stockage et réseau) et qui a son propre système d'exploitation. Elle est isolée du système hôte et des autres machines virtuelles.

2. Citez deux avantages de la virtualisation dans un environnement professionnel.

- La scalabilité. il est possible d'allouer plus ou moins de ressources à une machine virtuelle selon les besoins des applications et le nombre d'utilisateurs.
- L'isolation. L'utilisation de machines virtuelles permet d'isoler les applications entre elles et avec l'OS hôte. Ainsi, chaque application a son propre environnement et n'interfère pas avec les autres applications. Cela permet également d'avoir une sécurité accrue, car si une application est compromise, les autres applications ne sont pas affectées.

3. Quelle différence existe-t-il entre travailler directement sur votre ordinateur et travailler dans une machine virtuelle ?

Travailler dans une machine virtuelle permet d'avoir un environnement contrôlé, ce qui permet de recréer un environnement identique pour tous les développeurs, peu importe leur machine. Cela ajoute cependant un overhead en termes de performance qui peut poser problème dans certains cas. 

## Étape 2
1. Expliquez, avec vos propres mots, ce qu’est un conteneur Docker.

Un conteneur Docker est un environnement standardisé et isolé qui permet de rouler des applications de manière portable. Il est fait pour être facile à créer, à partager et déployer. Il utilise les ressources du système hôte sans avoir besoin d'un système d'exploitation complet, contrairement à une machine virtuelle. 

2. Quelle différence fondamentale existe entre une machine virtuelle et un conteneur ?

Une machine virtuelle est un environnement complet qui contient son propre système d'exploitation et ses propres ressources virtuelles, contrairement à un conteneur qui utilise le système d'exploitation et les ressources de l'hôte. Un conteneur est également fait pour être créé et détruit rapidement, tandis qu'une machine virtuelle est plus lourde et prend plus de temps à démarrer.

3. Pourquoi les conteneurs sont-ils particulièrement adaptés au déploiement d’applications dans le Cloud ?

Étant donné que les conteneurs sont définis par du code, leur automatisation est plus facile et rapide. Ils sont également conçus pour être rapides à créer et déployer, ce qui est idéal pour les environnements qui nécessitent une scalabilité. Leur légèreté permet également de partager les ressources efficacement entre applications. L'écosystème de registre de conteneurs comme le Docker Hub permet de facilement partager et mettre à jour les images ainsi que de les déployer dans le Cloud. 

## Étape 3
1. Pourquoi un Dockerfile est-il préférable à la configuration manuelle d’un conteneur ?

L'utilisation d'un Dockerfile permet d'éviter les erreurs humaines dans la configuration d'un conteneur en le définissant clairement dans un fichier et en recréant le conteneur de manière identique à chaque fois. Cela permet également de versionner la configuration et de la partager facilement avec d'autres développeurs. Finalement, le Dockerfile permet l'automatisation de le gestion des containeurs en permettant de créer et détruire des images en utilisant du code.

2. Quelle différence existe entre une image Docker et un conteneur Docker ?

Une image Docker est un peu comme un modèle utilisé pour créer des conteneurs, tandis que le conteneur est une instance exécutable de l'image. Le Dockerfile permet de décrire une image en définissant les instructions à suivre, et en "buildant" le Dockerfile, nous obtenons l'image Docker, qui contient toutes les ressources et dépendances nécessaires à notre application. 

## Étape 4
1. Pourquoi Docker Compose est-il préférable au lancement manuel de plusieurs conteneurs ?

Docker compose permet de lancer et gérer les relations entre plusieurs conteneurs avec un seul fichier. Cela permet donc de simplifier et d'accélerer le processus de développement et déploiement d'applications complexes qui nécessitent plusieurs conteneurs. Par exemple, une application avec des centaines de microservices peut être lancée avec une seule commande, ce qui va créer les conteneurs pour chaque microservices ainsi que la configuration réseau et volumes nécessaires. 

2. Quel est le rôle du fichier "docker-compose.yml" ?

Il est un peu comme le Dockerfile, dans le sens ou il sert de modèle pour décrire où trouver nos images, comment les build, comment les connecter et toute les autres informations necessaire au fonctionnement de nos services. Il necessite soit une image construite dans un repository ou le chemin vers un Dockerfile afin de pouvoir construire les images. Les informations de réseau et des volumes sont également présentes dans ce fichier.

3. Dans quels cas Docker Compose pourrait-il atteindre ses limites ?

Dans le cas ou une orchestration est necessaire afin de créer et détruire des conteneurs dynamiquement sur différentes machines. Docker compose permet de facilement lancer un ou plusieurs services sur une machine, mais il ne permet pas de gérer des conteneurs a travers plusieurs machines, selon leur usage individuel. Dans ce cas, un service d'orchestration comme Kubernetes est un meilleur choix. En d'autres mots, Docker compose est simple et efficace pour le développement, les tests et les déploiements à petite échelle, mais est plus limité en environnement de production à grande échelle.