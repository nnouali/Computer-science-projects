# Pokemon Rescue Saga

Projet de Programmation Orientée Objet (Java / Swing) — HUANG & NOUALI

Un jeu de réflexion inspiré des jeux de type « SameGame » : sauvez les Pokémon
des mains de la Team Rocket en faisant disparaître les blocs de couleur qui les
retiennent, jusqu'à ce qu'ils atteignent le sol.

![Aperçu du jeu](jeu.jpg)

## Règles du jeu

- Le plateau est composé de cases colorées, de Pokémon et parfois de cases
  fixes (cailloux) qui ne bougent jamais.
- Cliquez sur une case de couleur : si elle est contiguë (horizontalement ou
  verticalement) à au moins une autre case de la même couleur, tout le groupe
  disparaît.
- Les cases situées au-dessus tombent pour combler le vide et les colonnes
  vides sont supprimées.
- Un Pokémon qui atteint la dernière ligne du plateau est sauvé.
- **Gagné** : tous les Pokémon sont sauvés.
- **Perdu** : il reste des Pokémon mais plus aucun groupe de cases ne peut être
  supprimé.

### Score

Chaque coup rapporte `(nombre de cases supprimées)² × 10` points. Le bouton
**Undo** annule le dernier coup (et retire les points correspondants).

## Fonctionnalités

- **3 niveaux** de difficulté croissante (plateaux différents, nouveaux Pokémon
  à sauver — Pikachu, Aquali, Mentali — et cases fixes au niveau 3).
- **Mode Robot** : le jeu se joue tout seul, en cliquant chaque seconde sur
  une case valide choisie au hasard.
- **Help me** : met en évidence (fleurs) un groupe de cases jouable.
- **Undo / Restart / Next Level / Exit** disponibles depuis chaque niveau.
- **Version console** (`PlateauText`) : le niveau 1 jouable au clavier en
  saisissant des coordonnées de la forme `B6`.

## Lancement

Prérequis : un JDK (Java 8 ou plus récent).

```bash
# depuis le dossier du projet
javac *.java

# version graphique (fenêtre d'accueil : choix du niveau, robot, aide)
java Lanceur

# version console (niveau 1)
java PlateauText
```

> **Remarque (Linux/macOS)** : les images sont chargées avec des chemins
> relatifs, il faut donc lancer le programme depuis le dossier du projet. Sur
> un système sensible à la casse, veillez à ce que les noms de fichiers
> d'images correspondent à ceux utilisés dans le code (`pikachu.png`,
> `jeu.JPG`, …).

## Architecture

Le projet suit une organisation proche du modèle MVC :

| Fichier | Rôle |
|---|---|
| `Lanceur.java` | Point d'entrée : crée le modèle et la fenêtre d'accueil. |
| `Modele.java` | Logique de fin de partie (gagné/perdu) et mémorisation de l'état pour l'Undo. |
| `Plateau.java` | Classe mère des plateaux : affichage Swing, suppression des groupes de cases adjacentes, réarrangement du plateau, score, aide. |
| `PlateauMain.java` | Fenêtre d'accueil : choix du niveau, mode robot, règles, quitter. |
| `PlateauNiveau1/2/3.java` | Les trois niveaux (grille propre à chacun). |
| `PlateauRobot.java` | Mode automatique : un `Timer` joue un coup aléatoire valide chaque seconde. |
| `PlateauText.java` | Version console du jeu (utilise `Modele`). |
| `ModelText.java` | Variante de `Modele` prévue pour la version console, non utilisée actuellement. |
| `Joueur.java` | Pseudo et score du joueur, saisie clavier pour la version console. |
| `Serialisable.java` | Interface marqueur. |

### Codage des cases

Le plateau est représenté par une matrice d'entiers `color[i][j]` :

| Valeur | Signification |
|---|---|
| 0 | case vide |
| 1 | Pikachu |
| 2 – 6 | cases de couleur (vert, violet, jaune, rouge, bleu) |
| 7 | case fixe (caillou) |
| 8 | Aquali |
| 9 | Mentali |

## Auteurs

Projet réalisé par **HUANG** et **NOUALI** dans le cadre du cours de
Programmation Orientée Objet.
