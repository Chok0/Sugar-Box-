# 🍬 Sugar Box — Rhythm Idle Sequencer

Prototype minimal de la boucle centrale décrite dans la [note de cadrage](note-cadrage-rhythm-idle.pdf) (section 7) : **1 Sugar Box, 1 son (clap synthétisé), grille 8 steps, 1 looper**.

## Jouer

Ouvrir `index.html` dans un navigateur (aucun build, aucune dépendance — Web Audio API uniquement), ou servir le dossier :

```
python3 -m http.server 8000
# → http://localhost:8000
```

## La boucle (v0.2)

1. **Frapper** (touches 1-4, espace ou les pads) quand la tête de lecture traverse un pas actif — la précision (PARFAIT / BIEN / OK / RATÉ) détermine le gain en sucres.
2. **Bind** : après 8 frappes, geler la qualité en looper — il joue tout seul et génère du passif : `qualité_du_bind × pas_actifs × BPM`.
3. **Règle clé** : refrapper sur une box **détruit son loop** — pas de superposition qui perturbe la synchro ; à toi de choisir quand reprendre la main (le passif s'arrête jusqu'au re-bind). Changer de séquence perd aussi le loop.
4. **Acheter** dans la boutique, puis retour à la frappe.

## Contenu achetable

- **Sugar Box supplémentaires** (jusqu'à 4), chacune avec son propre son (clap, pok, kick, hi-hat), sa grille et son looper indépendant — jouer l'une pendant que les autres tournent
- **Séquences** de complexité croissante : noires seules → noires + croches → syncopes → off-beat → roulement
- **Extension de grille 16 pas** (2 mesures) qui débloque les séquences longues
- **Nappe de fond (drone)** : ambiance + revenus ×1.25, activable/désactivable
- **BPM** : 60 → 180, +10 par achat (coût ×1.6) — plus de débit, précision plus dure

## Réglages actuels (à ajuster au feel)

| Paramètre | Valeur |
|---|---|
| Fenêtres de précision | ±45 ms (parfait ×3), ±90 ms (bien ×2), ±160 ms (ok ×1) |
| Gain par frappe | 5 🍬 × multiplicateur × (BPM/60) × drone |
| Rendement looper | 60 % d'une frappe équivalente, pondéré par la qualité du bind |
| Tempo de départ | 60 BPM |
| Résolution | 1 pas = 1 croche ; 8 pas = 1 mesure |
| Métronome | activable/désactivable dans les réglages |
| Sauvegarde | automatique (localStorage), bouton reset dans les réglages |

## Hors périmètre du proto (volontairement)

Univers/prestige, multi-pistes par machine, effets (filtre/delay/swing), dégradation du looper dans le temps (question ouverte n°3 de la note).

## Limites connues

- La latence clavier/audio n'est pas calibrée ; les fenêtres de précision sont volontairement larges pour compenser.
- Timing basé sur l'horloge audio avec planification anticipée (lookahead 25 ms / 200 ms) — précis, mais non testé sur mobile bas de gamme.
