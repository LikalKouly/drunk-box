# Drunk Box — prototype de contrôle

Prototype web qui valide une seule chose : déplacer un personnage ivre **uniquement en inclinant la tablette**, dans une salle qui réagit en 3D au mouvement.

Une seule page (`index.html`), sans étape de compilation. Three.js est chargé depuis un CDN.

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
