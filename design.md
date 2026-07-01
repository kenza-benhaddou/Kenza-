<!-- design.md — Spécification de design pour l'application Kenza -->
# Guide de Design

Ce document présente la direction de design pour l'application : personnalité de la marque, palette de couleurs, typographie, composants, navigation, vues principales (Dashboard, Liste de courses, Planificateur hebdomadaire, Découverte de recettes), principes UX et accessibilité.

---

## 1. Personnalité de la marque

- Ton: Chaleureux, pratique, fiable.
- Valeurs: simplicité, gain de temps, santé et clarté.
- Voix: conversationnelle mais concise — guides et microcopies orientées action.
- Promesse: Aider l'utilisateur à planifier ses repas et courses rapidement, réduire le gaspillage et stimuler la créativité culinaire.

---

## 2. Palette de couleurs

Palette principale (tokens):

- Primary: #0F72FF (Bleu vif) — actions principales, CTA.
- Primary-600: #0C5EDB
- Secondary: #FF8A00 (Orange chaleureux) — accents, états actifs.
- Neutral-900: #0B1220 — texte principal.
- Neutral-700: #2A3A4A — texte secondaire.
- Neutral-200: #E6EEF8 — surfaces légères, backgrounds.
- Surface: #FFFFFF — cartes et surfaces principales.
- Success: #16A34A (vert) — confirmations.
- Danger: #E11D48 (rouge) — erreurs.

Usage:

- CTA primaire: `Primary` sur fond `Surface` ou `Neutral-900` selon contraste.
- Accent et badges: `Secondary`.
- Cartes et surfaces: `Surface` avec `Neutral-200` pour séparateurs.

Contraste: viser un ratio de contraste d'au moins 4.5:1 pour le texte normal et 3:1 pour les textes larges ou les icônes.

---

## 3. Typographie

- Famille principale: Inter (sans-serif) — disponible en variable font.
- Hiérarchie recommandée:
  - H1: 32px / 40px — 700
  - H2: 24px / 32px — 600
  - H3: 20px / 28px — 600
  - Body (p): 16px / 24px — 400
  - Small: 14px / 20px — 400
- Kerning et lisibilité: line-height généreuse, surtout pour listes et descriptions d'ingrédients.

Accents typographiques:

- Boutons: 16px / 20px — 600
- Étiquettes de petite taille: 12px — 600 (caps si nécessaire)

---

## 4. Composants

Chaque composant doit être atomique, accessible et documenté (propriétés, variantes, état, exemples d'usage).

- Bouton (`Button`)
  - Variantes: `primary`, `secondary`, `ghost`, `danger`.
  - États: `default`, `hover`, `active`, `disabled`, `loading`.
  - Règles: largeur adaptative, min-height 40px, focus visible (anneau de 3px, `Primary-600` avec outline), icône à gauche optionnelle.

- Champ (`Input`)
  - Types: text, number, search, textarea.
  - États: `default`, `focus`, `error`, `disabled`.
  - Labels persistants et aides (`helper text`).

- Carte (`Card`)
  - Utilisée pour recettes, items de liste, aperçus de planification.
  - Élévation légère, padding 16px, coin 8px.

- Liste (`List`) & Item
  - Items remixables: drag & drop pour réorganiser la liste de courses.

- Badge & Tag
  - Pour états rapides (ex: `Vegan`, `Favori`, `Rapide`).

- Modal / Drawer
  - Utiliser Drawer pour interactions progressives (ex: ajouter un ingrédient), Modal pour confirmations bloquantes.

- Toast & Snackbar
  - Notifications brèves, accessibles, dismissible.

Composants spécifiques produit:

- `RecipeCard`: image, titre, temps, portions, badges, bouton `Ajouter au plan`.
- `GroceryItem`: case à cocher, quantité editable, catégories, remove.
- `WeekPlannerGrid`: jours en colonnes, repas en lignes, drag/drop de `RecipeCard`.

---

## 5. Navigation

- Structure principale:
  - Barre inférieure (mobile) ou latérale (desktop) avec 4-5 items: `Dashboard`, `Planner`, `Liste de courses`, `Découvrir`, `Profil`.
  - Breadcrumbs légers dans les vues profondes (ex: dossier de recettes).

- Comportement:
  - Persistante et visible sur  >=768px en vertical, responsive en bottom nav pour mobile.
  - Indicateur d'état actif: underline + icône coloré.

---

## 6. Dashboard

But: Synthétiser les actions clés et l'état actuel (prochain repas, liste de courses, suggestions rapides).

Blocs recommandés:

- Vue « Aujourd'hui »: repas planifiés, temps total de préparation.
- Raccourcis: Ajouter recette, Générer liste de courses, Planifier semaine.
- Statistiques rapides: ingrédients à proximité de la péremption, économies estimées.

Interactions:

- CTA clair pour `Ajouter au plan` et `Générer la liste`.
- Cartes cliquables menant à la vue détaillée.

---

## 7. Liste de courses

Objectif: Faire des courses rapides et organisées.

Fonctionnalités clés:

- Catégorisation automatique par rayon (fruits, légumes, produits laitiers).
- Options d'édition inline (quantité, unité).
- Cases à cocher persistantes; possibilité de créer une nouvelle liste.
- Mode magasin: afficher uniquement les items non cochés et grouper par rayon.
- Synchronisation & partage: partager la liste par lien ou export CSV.

UX:

- Prioriser l'usage one-tap pour cocher/décocher.
- Confirmation simple pour suppression d'items multiples.

---

## 8. Planificateur hebdomadaire

Objectif: Planifier les repas de la semaine rapidement.

Structure:

- Grid: 7 colonnes (jours) x 3-4 lignes (petit déjeuner, déjeuner, dîner, snacks).
- Drag & drop: placer une `RecipeCard` sur une cellule.
- Vue de résumé journalier et hebdomadaire (calories approximatives, temps total).

Fonctionnalités:

- Suggestions intelligentes: proposer recettes basées sur le contenu du frigo / préférences.
- Générer automatiquement la liste de courses depuis le planificateur.

---

## 9. Découverte de recettes

Objectif: Inspirer et aider la conversion en plan ou liste de courses.

Parcours:

- Carte recette: image 16:9, titre, temps, difficulté, badges (Vegan, Rapide).
- Filtres persistants: ingrédients disponibles, temps max, régime, difficulté.
- Moteur de recherche: recherche par ingrédient (ex: "poulet + brocoli").

Actions principales:

- `Voir recette` (détail) — `Ajouter au plan` — `Ajouter à la liste` — `Favori`.

---

## 10. Principes UX

- Clarté: toute vue doit répondre à "Qu'est-ce que je peux faire ici ?" en <3 secondes.
- Minimalisme fonctionnel: masquer les options avancées derrière des interactions secondaires.
- Réversibilité: actions destructrices demandent confirmation mais restent réversibles quand possible.
- Prévention des erreurs: validations inline, suggestions intelligentes.
- Progressive disclosure: montrer l'essentiel, afficher le reste à la demande.

---

## 11. Accessibilité

- Contrastes: respecter WCAG AA (4.5:1 pour texte normal). Tester `Primary` et `Secondary` sur `Surface`.
- Navigation clavier: toutes les interactions (planifier, cocher, drag & drop) doivent fonctionner au clavier; fournir alternatives pour DnD (menu contextuel "Déplacer vers...").
- Focus visible: styles de focus nets et cohérents; ne pas se fier uniquement à la couleur.
- ARIA: rôles clairs pour listes, boutons, modals; labels explicites pour champs et contrôles personnalisés.
- Lecteurs d'écran: tests pour flux clés (ajouter au plan, générer liste, cocher item).
- Taille cible: minimum 40x40px pour éléments interactifs tactiles.

Checklist rapide d'accessibilité:

- [ ] Ratio de contraste vérifié
- [ ] Navigation clavier complète
- [ ] Tests de lecteur d'écran pour parcours critiques
- [ ] Balises ARIA et labels présents

---

## Annexes — Exemples rapides

- Token CSS (ex.):

```css
:root {
  --color-primary: #0F72FF;
  --color-secondary: #FF8A00;
  --text-900: #0B1220;
  --surface: #FFFFFF;
}
```

- Exemple de bouton primaire:

```html
<button class="btn btn-primary">Ajouter au plan</button>
```

---

Pour toute question ou adaptation (ton, couleurs alternatives, ou exigences d'accessibilité plus strictes), je peux générer des variantes et des tokens supplémentaires.
