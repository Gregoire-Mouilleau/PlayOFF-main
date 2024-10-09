# PlayOFF

Voici notre projet Transversal de l'élaboration d'une application qui permet à n'importe qui de créer des tournois entre amis dans n'importe quelle discipline (sport, activité, jeux, etc...)

## Requirements

- PHP >= 8.2
- Composer
- Symfony CLI (optionnel mais conseillé)
- NodeJS

## Installation

### Cloner le répertoire

```bash
git clone git@github.com:Sam-rst/PlayOFF.git
cd PlayOFF
```

### Installer les dépendances Composer et NodeJS

```bash
composer install
npm install
```

### Se connecter à la base de données

1. Copier le fichier [.env](.env) dans un nouveau fichier [.env.local](.env.local)
```bash
cp .env .env.local
```

2. Ouvrir le fichier [.env.local](.env.local) puis commenter la ligne 29, et décommentez la ligne 27 et y mettre les identifiants de connection à la database en localhost :
```txt
DATABASE_URL="mysql://user:password@localhost:3306/play_off?serverVersion=8.0.32&charset=utf8mb4"
```

3. Création de la base de données (SI vous ne l'avez pas créée de base):
```bash
symfony console doctrine:database:create
```

4. Création des migrations :
```bash
symfony console doctrine:migrations:migrate
```

### Activer l'extension intl de php
Pour pouvoir utiliser et manier les DateTimes de php dans un projet symfony, on a besoin d'activer l'extension intl
dans le fichier php.ini de la machine

Pour cela, veuillez :
1. Ouvrir ce fichier qui peut demander les accès admin
2. Rechercher la ligne ;extension=intl en faisant CTRL + F
3. Enlevez le ; et sauvegardez
4. Relancer le serveur php (symfony serve:start)

### Créer des fixtures
Dans un projet qui nécessite des données une quantité de données dans l'environnement de développement, pour éviter de devoir les générer à la main ces données, un très bon composant php nous d'en générer : fakerphp/faker
Avec le composant orm-fixtures, on peut automatiser la génération de ces données.
Après avoir installé les nouveaux packages (composer install), veuillez suivre les étapes suivantes :

1. Pour réinitialiser la database (supprimer les migrations si il y en a):
```bash
symfony console doctrine:database:drop --force
symfony console d:d:c
symfony console make:migration
symfony console d:m:m
```

2. Création des données venant du dossier [src/DataFixtures/AppFixtures](src/DataFixtures/AppFixtures) déjà configuré :
```bash
symfony console doctrine:fixtures:load --no-interaction
```

