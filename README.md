# Drunk Box — prototype de contrôle

Prototype web qui valide une seule chose : déplacer un personnage ivre **uniquement en inclinant la tablette**, dans une salle qui réagit en 3D au mouvement.

Une seule page (`index.html`), sans étape de compilation. Three.js est chargé depuis un CDN. Le personnage est un modèle 3D articulé au rendu illustré.

L'écran reste figé dans l'orientation du départ, même quand on retourne la tablette. Le verrou natif est utilisé quand il existe (Android, en plein écran). Sinon, la page contre-tourne l'image.

## Salles du prototype

Les salles s'enchaînent : la sortie de l'une ouvre la suivante. Un écran de fin s'affiche après la dernière. Dans ⚙, le bouton **Salle suivante** permet de passer directement à la salle d'après.

| Salle | Ce qu'on y teste | Solution |
| --- | --- | --- |
| Salle de test | Marche, profondeur, boules qui roulent | Atteindre l'ouverture noire à droite |
| Scène 8 — L'évasion | Retourner la salle | Tourner lentement jusqu'au plafond, puis prendre la trappe. Retourner d'un coup est mortel |
| Scène 9 — La ventilation | Profondeur, élan, plongeon | Contourner le puits par l'avant, puis pencher fort pour plonger sous le conduit bas |
| Scène 10 — Le ventilateur | Agir sur un objet sans le toucher | S'abriter derrière le pilier (au fond), retourner la salle à environ 110° pour faire passer le bidon par-dessus le rebord, puis revenir : il bloque le ventilateur |
| Scène 11 — Le toit | Doser la vitesse | Rejoindre la gouttière en marchant. En courant, on passe par-dessus et on tombe dans la rue |
| Scène 14 — Le mur | Objet lourd qui bascule | Se tenir à l'écart, ramener le haut de la tablette vers soi pour faire tomber la tôle, puis entrer dans la cave |

## Tester sur tablette

Les capteurs de mouvement ne fonctionnent qu'en **HTTPS**.

1. Activez GitHub Pages sur ce dépôt : Settings → Pages → Branch `main`, dossier `/ (root)`.
2. Ouvrez `https://<votre-compte>.github.io/<nom-du-depot>/` sur la tablette.
3. Tenez la tablette en paysage, comme pour jouer, puis touchez **Commencer**. Cette position devient la position neutre. Sur iOS, acceptez l'accès aux capteurs de mouvement.

## Tester sur PC

```bash
python -m http.server 8765
```

Ouvrez ensuite `http://localhost:8765`. Les flèches ou un glisser de la souris inclinent la salle, Espace revient au neutre et R recalibre.

## Contrôles

| Geste | Effet |
| --- | --- |
| Pencher à gauche ou à droite | Le personnage marche dans ce sens. Au-delà de 25°, la pente l'emporte : il court de plus en plus vite sans pouvoir s'arrêter |
| Basculer le haut vers l'arrière ou vers soi | Il marche vers le fond ou vers l'avant |
| Pencher fort (plus de 55°) | Il tombe sur le mur |
| Retourner | Il tombe au plafond. Une chute trop rapide (plus de 8 m/s) le tue |
| ⟲ Recalibrer | La position actuelle redevient la position neutre |

## Réglages en jeu (⚙)

Les réglages couvrent la vue (face, plongée, trois-quarts, contre-plongée), la vitre avant (mur ou vide) et la taille du personnage. On peut aussi régler la zone morte, les angles d'emportement et de chute, la course max, la vitesse, la gravité, les seuils de mort, l'ivresse, le lissage du capteur, la force de l'effet 3D et l'amplification latérale. Enfin, des cases permettent d'inverser les axes (si un appareil donne ses axes à l'envers), d'activer la vibration et d'afficher le débogage. Tous ces réglages sont gardés sur l'appareil.
