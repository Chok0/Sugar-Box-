# 🍬 Sugar Box — Rhythm Idle Sequencer

Prototype minimal de la boucle centrale décrite dans la [note de cadrage](note-cadrage-rhythm-idle.pdf) (section 7) : **1 Sugar Box, 1 son (clap synthétisé), grille 8 steps, 1 looper**.

## Jouer

Ouvrir `index.html` dans un navigateur (aucun build, aucune dépendance — Web Audio API uniquement), ou servir le dossier :

```
python3 -m http.server 8000
# → http://localhost:8000
```

## La boucle (v0.3)

1. **Cliquer rapporte toujours** : un clic hors rythme donne +1 🍬 (ça reste un clicker), mais il casse le combo.
2. **Frapper en rythme** (touches 1-4, espace ou les pads) rapporte bien plus : `5 🍬 × précision (×1/×2/×3) × combo (jusqu'à ×4) × BPM`. Le combo monte sur les frappes PARFAIT/BIEN consécutives — c'est ce qui rend le jeu propre plus rentable que le spam.
3. **Rythmes cumulatifs** : acheter un rythme le rend actif par défaut, mais tous les rythmes possédés continuent de rapporter si on les frappe (cases fantômes sur la grille), sans avoir à les activer.
4. **Bind** : après 8 frappes, geler la qualité en looper — passif = `qualité_du_bind × frappes_du_rythme × BPM`. On peut cliquer par-dessus le looper sans le perdre ; re-bind remplace la qualité. Le droit de bind s'achète **par rythme** (achat « Loop », le rythme de départ l'inclut).

## Contenu achetable

- **Sugar Box supplémentaires** (jusqu'à 4), chacune avec son propre son (clap, pok, kick, hi-hat), sa grille et son looper indépendant — jouer l'une pendant que les autres tournent
- **Rythmes** de complexité croissante : noires seules → noires + croches → syncopes → off-beat → roulement
- **Loops** : le droit de bind chaque rythme en looper (achat séparé par rythme)
- **Extension de grille 16 pas** (2 mesures) qui débloque les rythmes longs
- **Nappe de fond (drone)** : ambiance + revenus ×1.25, activable/désactivable
- **BPM** : 60 → 180, +10 par achat (coût ×1.6) — plus de débit, précision plus dure

## Réglages actuels (à ajuster au feel)

| Paramètre | Valeur |
|---|---|
| Clic hors rythme | +1 🍬 fixe, remet le combo à zéro |
| Fenêtres de précision | ±45 ms (parfait ×3), ±90 ms (bien ×2), ±160 ms (ok ×1, maintient le combo) |
| Combo | +0.5 par frappe PARFAIT/BIEN, plafonné à ×4 |
| Gain par frappe en rythme | 5 🍬 × précision × combo × (BPM/60) × drone |
| Rendement looper | 60 % d'une frappe équivalente (sans combo), pondéré par la qualité du bind |
| Tempo de départ | 60 BPM |
| Résolution | 1 pas = 1 croche ; 8 pas = 1 mesure |
| Métronome | activable/désactivable dans les réglages |
| Sauvegarde | automatique (localStorage), bouton reset dans les réglages |

## Hors périmètre du proto (volontairement)

Univers/prestige, multi-pistes par machine, effets (filtre/delay/swing), dégradation du looper dans le temps (question ouverte n°3 de la note).

## Limites connues

- La latence clavier/audio n'est pas calibrée ; les fenêtres de précision sont volontairement larges pour compenser.
- Timing basé sur l'horloge audio avec planification anticipée (lookahead 25 ms / 200 ms) — précis, mais non testé sur mobile bas de gamme.
