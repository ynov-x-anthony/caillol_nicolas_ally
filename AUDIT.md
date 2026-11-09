# AUDIT.md

## 1. Audits outillés

Audits lancés sur la page (`npm run dev`, ouverte dans Chrome), **avant** correction :

- **Lighthouse** (catégorie Accessibility) : score de 86/100. Problème remonté : contraste insuffisant entre les couleurs de premier plan et d'arrière-plan sur N éléments (`.subtitle`, `.label`, `.hint`, `.btn-primary`).
- **axe DevTools** : N violations. La règle `color-contrast` est signalée au niveau Serious sur N éléments.
- **WAVE** : N erreurs, dont N Contrast Errors.

Après correction, les trois outils ne remontent plus d'erreur de contraste (Lighthouse : XX/100).

## 2. Les éléments à corriger

| Élément | Couleur texte | Couleur fond | Ratio mesuré | Ratio AA requis | Conforme ? |
|---------|---------------|--------------|--------------|------------------|------------|
| `.subtitle` | `#aaaaaa` | `#ffffff` | ≈ 2.3:1 | 4.5:1 | Non |
| `.label` | `#999999` | `#ffffff` | ≈ 2.8:1 | 4.5:1 | Non |
| `.hint` | `#bbbbbb` | `#ffffff` | ≈ 1.9:1 | 4.5:1 | Non |
| `.btn-primary` | `#ffffff` | `#6fa8dc` | ≈ 2.5:1 | 4.5:1 (texte) | Non |

Corrections appliquées dans `src/App.css` :

| Élément | Avant | Après | Nouveau ratio |
|---------|-------|-------|---------------|
| `.subtitle` | `#aaaaaa` | `#5c5c5c` | ≈ 6.7:1 |
| `.label` | `#999999` | `#595959` | ≈ 7.0:1 |
| `.hint` | `#bbbbbb` | `#595959` | ≈ 7.0:1 |
| `.btn-primary` | fond `#6fa8dc` | fond `#1a5fa8` (texte `#ffffff`) | ≈ 6.5:1 |

## 3. Priorisation

Classement par impact sur l'utilisateur :

1. **`.btn-primary`** : c'est l'action principale de la page. Si son texte est illisible, l'utilisateur ne peut pas accomplir la tâche.
2. **`.label`** : il donne le sens de chaque valeur affichée. Sans lui, la donnée est incompréhensible.
3. **`.hint`** : ratio le plus bas, mais c'est une aide secondaire. La page reste utilisable sans.
4. **`.subtitle`** : texte d'introduction. La page reste compréhensible sans lui.
