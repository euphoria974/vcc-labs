# TP 2

## Étape 1

1. Quel est le rôle d’un réseau privé dans une infrastructure Cloud ? D’un routeur externe ?

Le réseau privé permet aux machines du réseau de communiquer entre elles sans nécessairement les exposer au réseau externe (par exemple, internet). Le routeur externe permet de connecter le réseau privé au réseau externe avec les règles d'accès désirées selon le cas.

2. Pourquoi un fournisseur Cloud propose-t-il autant de catégories de ressources différentes ?

Dans un modèle IaaS comme OpenStack, le fournisseur donne au client accès à plusieurs ressources pour lui donner plus de liberté. Ainsi, chaque client peut choisir le compute, le stockage ou le réseau qui correspond à son application, ce qui permet d'utiliser une même plateforme IaaS pour toutes sortes d'utilisations.

3. En observant la topologie générée par OpenStack, expliquez le chemin emprunté par un paquet réseau envoyé depuis l’extérieur vers une machine virtuelle sur net-discovery.

Le paquet de l'extérieur entre par l'interface externe du routeur (`192.168.34.1`) qui redirige le paquet vers l'interface interne (`192.168.10.1`) qui se situe dans le réseau `net-discovery`. Le paquet peut ensuite atteindre la machine virtuelle.

## Étape 2

1. Quelles sont les étapes nécessaires pour pouvoir se connecter en SSH à une nouvelle machine virtuelle OpenStack depuis la machine hôte ?

    i. Créer une paire de clés SSH sur la machine virtuelle et télécharger la clé privée.
    ii. Ajouter une règle `CIDR 0.0.0.0/0` sur le protocole SSH pour permettre le trafic SSH entrant de n'importe quelle adresse.
    iii. Ajouter une adresse IP flottante pour rendre la VM accessible de l'extérieur du réseau privé.
    iv. Lancer la commande `ssh -i vm-discovery-key.pem ubuntu@<IP_FLOTTANTE>` avec la clé privé et l'IP flottante de la VM.

2. Quel est le rôle de l’adresse IP privée, de l’adresse IP flottante et des Groupes de Sécurité dans cette connexion ?

L'adresse IP privée permet de communiquer avec la VM sur le réseau privé. L'adresse IP flottante permet de communiquer avec la VM à partir du réseau externe (internet). Finalement, les Groupes de Sécurité permettent d'établir des règles sur différents protocoles (par exemple, ICMP ou SSH) et de les appliquer à un groupe de VMs.

3. Pourquoi OpenStack distingue-t-il une adresse IP privée d’une IP flottante publique, plutôt que d’attribuer directement une adresse publique à chaque machine virtuelle ?

Cette distinction permet d'abord de renforcer la sécurité du réseau interne en masquant celui-ci de l'internet par défaut. De plus, les adresses IPv4 publiques sont limitées sur les réseaux publics et les plages d'adresses publiques peuvent coûter assez cher, donc c'est une bonne pratique de limiter les adresses publiques utilisées au strict nécessaire. 

## Étape 3

1. Pourquoi les Security Groups sont-ils indispensables même lorsqu’une machine virtuelle possède une adresse IP publique ?

Les security groups sont indispensables pour assurer la sécurité du réseau privé et des machines. En effet, garder tous les ports et protocoles ouverts à tout l'internet expose la machine à plus d'attaques. Les security groups permettent de restreindre l'accès par défaut et d'autoriser seulement le nécessaire.

2. Décrivez le chemin parcouru par une requête HTTP envoyée depuis votre ordinateur jusqu’à l’application hello-api exécutée sur votre machine virtuelle.

    i. La requête HTTP quitte notre ordinateur vers le routeur passerelle de notre réseau local.
    ii. Le routeur achemine la requête (en passant par d'autres routeurs et d'autres réseaux) jusqu'au routeur externe de OpenStack.
    iii. Le routeur de OpenStack achemine la requête à la VM.

## Étape 4

1. Quelles différences existe-il entre une image officielle et un snapshot ?

L'image est un modèle contenant un système d'exploitation et optionnellement des logiciels et des données dans le but de créer rapidement des instances de machines virtuelles avec une configuration spécifique. Le snapshot est une capture instantanée de l'état complet d'une VM qui permet de créer une copie de la VM ou de restaurer un état dans le temps. Avec certains hyperviseurs comme VMWare vSphere, les snapshots sauvegardent aussi la mémoire virtuelle incluant les processus en cours d'exécution.

2. Quels avantages apporte le redimensionnement d’une machine virtuelle dans un environnement Cloud ?

Le redimensionnement d'une machine virtuelle permet d'assurer l'élasticité des services facilement. Par exemple, si le nombre d'utilisateurs d'un service web augmente, on peut redimensionner la VM pour augmenter les capacités du service. À un niveau plus avancé, ce redimensionnement peut se faire automatiquement selon le trafic web ou les ressources en demande.

3. Dans quels contextes un administrateur système préférera-t-il créer une nouvelle machine à partir d’un snapshot plutôt que de repartir d’une image vierge ?


