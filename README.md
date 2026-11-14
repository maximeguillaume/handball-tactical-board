# Planche tactique handball

Une planche tactique pour entraîneur de handball, dans une seule page web. On y place les joueurs, on trace les courses, les passes et les tirs, et on anime un enchaînement étape par étape.

La page s'utilise à la souris, au doigt ou au stylet. Elle ne demande ni installation ni compte.

## Utilisation

Ouvrez `index.html` dans un navigateur. La page s'ouvre sur un exemple : attaque en 3-3 contre défense 6-0 sur demi-terrain.

### Terrain

- Demi-terrain (but en haut) ou terrain entier de 40 × 20 m.
- Tracés réglementaires : zone à 6 m, ligne de jet franc à 9 m, ligne des 7 m, ligne des 4 m du gardien, zones de changement.

### Joueurs et matériel

- Attaquants, défenseurs, gardiens, ballon et plots se déplacent par glisser-déposer.
- Touchez un joueur pour changer son étiquette (3 caractères au plus : `ALG`, `DC`, `PIV`, un numéro…) ou le supprimer.
- Le panneau « Ajouter » crée de nouveaux joueurs, ballons ou plots.

### Outils de tracé

| Outil | Trait | Signification |
| --- | --- | --- |
| Course | plein, avec flèche | déplacement d'un joueur sans ballon |
| Passe | pointillé, avec flèche | trajectoire du ballon |
| Dribble | ondulé, avec flèche | déplacement en dribble |
| Tir | double, avec flèche | tir au but |
| Écran | plein, terminé par une barre | écran ou bloc |
| Crayon | libre, sans flèche | annotation |
| Zone | ellipse translucide | espace à surligner |
| Gomme | — | efface le tracé touché |

Les tracés à main levée sont simplifiés et lissés automatiquement. Quatre couleurs sont disponibles. Avec l'outil « Déplacer », un tracé peut être sélectionné, déplacé, recoloré ou supprimé.

### Placements

- Attaque : 3-3 ou 2-4 (deux pivots).
- Défense : 6-0, 5-1, 3-2-1, 4-2 ou 3-3.

Un placement repositionne les joueurs existants de l'équipe et crée ceux qui manquent.

### Étapes et lecture

1. Placez les joueurs et tracez les intentions de jeu.
2. « + Étape » copie les positions dans une nouvelle étape, sans les tracés.
3. Déplacez les joueurs vers leur position suivante.
4. « Lecture » anime le passage d'une étape à l'autre.

### Enregistrement

- La planche en cours est sauvegardée automatiquement.
- « Mes schémas » enregistre des planches sous un nom, pour les rouvrir plus tard.

Tout est stocké dans le navigateur (`localStorage`). Les schémas restent donc sur l'appareil et le navigateur où ils ont été créés, et disparaissent si les données du site sont effacées. Il n'y a pas d'export en image ou en PDF.

### Raccourcis clavier

| Touche | Action |
| --- | --- |
| `Ctrl` / `Cmd` + `Z` | annuler |
| `Ctrl` / `Cmd` + `Maj` + `Z` | rétablir |
| `Suppr` ou `Retour arrière` | supprimer la sélection |
| `Échap` | désélectionner |

## Sur mobile

La mise en page s'adapte aux petits écrans. La tablette reste le format le plus confortable.

- Le terrain occupe toute la largeur de l'écran, l'en-tête est réduit et les outils tiennent sur une seule ligne qui défile horizontalement.
- En portrait, le terrain entier s'affiche en hauteur, but du haut à attaquer.
- Le panneau de réglages passe sous le terrain.
- Un doigt posé sur le terrain trace ou déplace ; pour faire défiler la page, partez des barres ou des panneaux.
- Le bouton ⛶ agrandit la planche. Quand le navigateur n'autorise pas le vrai plein écran (iPhone), la planche remplit la page à la place : les barres du navigateur restent visibles.

### Ajouter à l'écran d'accueil

Depuis la version en ligne, la page s'installe comme une application, avec son icône :

- **iPhone et iPad** : dans Safari, bouton Partager puis « Sur l'écran d'accueil ».
- **Android** : dans Chrome, menu puis « Ajouter à l'écran d'accueil » ou « Installer l'application ».

Lancée depuis l'écran d'accueil, la planche s'ouvre sans les barres du navigateur. Sur iOS, elle garde alors ses propres schémas, séparés de ceux enregistrés dans Safari.

## Technique

Toute la page tient dans `index.html`, sans dépendance ni étape de build. Les autres fichiers servent à l'icône : `icon.svg` (le dessin d'origine), ses exports `icon-192.png`, `icon-512.png` et `apple-touch-icon.png`, et `manifest.webmanifest`.

- **SVG** pour le terrain, les joueurs et les tracés. Le repère est en décimètres : `x` de 0 à 400 dans la longueur, `y` de 0 à 200 dans la largeur. Le demi-terrain est le même dessin, retourné par une transformation.
- **JavaScript** sans framework : Pointer Events pour la souris et le tactile, `requestAnimationFrame` pour l'animation.
- **CSS** avec variables, thème clair ou sombre selon le système.
- **Police** Barlow, chargée depuis Google Fonts. Hors connexion, la page utilise une police système.

### Modifier la page

Les données se trouvent au début du script de `index.html` :

- `ATT` et `DEF` : coordonnées des placements d'attaque et de défense.
- `TOOLS` : liste des outils, avec leur icône et leur texte d'aide.
- `COLORS` : couleurs de tracé.

Les couleurs du terrain et de l'interface sont des variables CSS, déclarées dans `:root` en haut de la feuille de style.

Pour travailler en local, ouvrez le fichier directement ou servez le dossier :

```sh
python3 -m http.server 8000
```

puis ouvrez <http://localhost:8000>.

## État du projet

La page n'a pas encore fait l'objet d'une campagne de tests sur navigateurs et appareils tactiles. Les retours et corrections sont bienvenus.
