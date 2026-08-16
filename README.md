# 🍬 Sugar Box — Rhythm Idle Sequencer

Prototype minimal de la boucle centrale décrite dans la [note de cadrage](note-cadrage-rhythm-idle.pdf) (section 7) : **1 Sugar Box, 1 son (clap synthétisé), grille 8 steps, 1 looper**.

## Jouer

Ouvrir `index.html` dans un navigateur (aucun build, aucune dépendance — Web Audio API uniquement), ou servir le dossier :

```
python3 -m http.server 8000
# → http://localhost:8000
```

## La boucle testée

1. **Composer** : activer des pas sur la grille 8 steps (les points marquent les temps).
2. **Frapper** (espace ou le pad) quand la tête de lecture traverse un pas actif — la précision (PARFAIT / BIEN / OK / RATÉ) détermine le gain en sucres.
3. **Bind** : après 8 frappes, transformer le pattern en looper. La **qualité du moment du bind est gelée** et fixe le revenu passif : `qualité_du_bind × pas_actifs × BPM`.
4. **Acheter du BPM** : plus de revenu, mais fenêtres de précision plus dures à tenir.
5. **Re-bind** à tout moment pour améliorer la qualité gelée — c'est le twist anti-clicker : rejouer manuellement reste utile même quand le looper tourne.

## Réglages actuels (à ajuster au feel)

| Paramètre | Valeur |
|---|---|
| Fenêtres de précision | ±45 ms (parfait ×3), ±90 ms (bien ×2), ±160 ms (ok ×1) |
| Gain par frappe | 5 🍬 × multiplicateur × (BPM/90) |
| Rendement looper | 60 % d'une frappe équivalente, pondéré par la qualité du bind |
| BPM | 90 → 180, +10 par achat, coût 200 🍬 ×1.6 |
| Résolution | 8 pas = 1 mesure en croches |

## Hors périmètre du proto (volontairement)

Univers/prestige, sampler, multi-pistes, effets, extension de grille, sauvegarde, dégradation du looper dans le temps (question ouverte n°3 de la note).

## Limites connues

- La latence clavier/audio n'est pas calibrée ; les fenêtres de précision sont volontairement larges pour compenser.
- Timing basé sur l'horloge audio avec planification anticipée (lookahead 25 ms / 200 ms) — précis, mais non testé sur mobile bas de gamme.
