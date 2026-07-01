<!-- RULES.md — Standards et règles pour le projet Smart Meal Prep Planner -->
# Règles du projet — Smart Meal Prep Planner

Ce document rassemble les règles et bonnes pratiques à respecter pour le projet : qualité de code, cohérence UI, accessibilité, sécurité, organisation des fichiers, workflow Git, usage d'IA, tests et documentation.

---

## 1. Qualité du code

- Style et linting : configurer et appliquer des outils de linting et formattage (ESLint, Prettier, SwiftLint, ktlint, etc.).
  - Les PR doivent passer le linting et la CI avant revue.
- Revue de code : chaque PR a au moins 1 relecteur indépendant.
  - Relectures ciblent lisibilité, tests, sécurité et conformité aux API.
- Commits : messages clairs, impératifs et préfixés (feat:, fix:, chore:, docs:, refactor:, test:).
- Tests : tout nouveau code critique doit être couvert par tests unitaires ou d'intégration.
- Dépendances : mettre à jour régulièrement, utiliser `dependabot` ou équivalent, valider les breaking changes.

Checks automatiques recommandés : lint, typecheck, tests unitaires, scanning de vulnérabilités.

---

## 2. Cohérence UI

- Design system : centraliser tokens (couleurs, typographies, espacements) et composants réutilisables.
- Composants : documentés (props, variants, states) et testés visuellement (storybook ou équivalent).
- Variantes et états : prévoir `default`, `hover`, `active`, `disabled`, `loading`, `focus`.
- Spacing et grid : suivre la grille définie dans `design.md` pour alignement et rythme visuel.
- Images et icônes : format WebP/AVIF optimisés, sprites ou icons system (SVG symbol).

Contrôles de qualité UI : review visuelle, tests de régression visuelle (Percy, Chromatic).

---

## 3. Accessibilité

- Objectifs : respecter WCAG AA au minimum pour les surfaces utilisateur.
- Contraste : ratio >= 4.5:1 pour texte normal, >= 3:1 pour texte large.
- Navigation clavier : toutes les fonctionnalités accessibles au clavier (tab order, actions alternatives pour DnD).
- Focus visible : styles de focus cohérents et non uniquement basés sur la couleur.
- ARIA & labels : ajouter des rôles et `aria-*` pour composants non natifs.
- Tests : utiliser axe-core, Lighthouse et tests manuels avec lecteurs d'écran pour les parcours critiques.

---

## 4. Sécurité

- Secrets : ne jamais stocker de clés ou secrets en clair dans le repo. Utiliser vaults / secrets manager.
- Communication : TLS obligatoire (HTTPS) pour toutes les communications réseau.
- Auth & permissions : principe du moindre privilège, token expirables, scopes limités.
- Validation : valider toute entrée externe côté serveur et côté client.
- Dépendances : scanner vulnérabilités (Snyk, `npm audit`, `dependabot`) et corriger rapidement.
- Stockage des données sensibles : chiffrer au repos et en transit.

Incident response : documenter le processus de signalement et mitigation (qui contacter, étapes initiales).

---

## 5. Organisation des fichiers

- Racine claire : séparer `src/`, `assets/`, `packages/`, `docs/`, `tests/`.
- Nommage : utiliser `kebab-case` pour fichiers publics et `PascalCase` pour composants React/Native.
- Modules : structure par feature (feature-first) plutôt que par type quand pertinent.
- Assets : centraliser images et icônes dans `assets/` et les référencer via tokens ou imports.
- Configs : stocker configs partagées (`.eslintrc`, `prettierrc`, `tsconfig`) à la racine.

---

## 6. Workflow Git

- Branching : utiliser `main` (production), branches de fonctionnalité `feat/<desc>` ou `fix/<desc>`.
- PRs : petites, atomiques, avec description, screenshots et checklist de tests.
- Rebase ou merge : privilégier merge via PR (squash commits selon politique équipe).
- Releases : tagger les releases et maintenir un `CHANGELOG.md` (manuel ou généré).
- Politique de protection : activer protections de branche (requérir revues, CI verte, checks passés).

Template PR minimal : résumé, issue liée, tests ajoutés, instructions de QA, captures d'écran.

---

## 7. Usage d'IA

- Transparence : documenter quand et où l'IA est utilisée (génération de copie, suggestions nutritionnelles, codegen).
- Données sensibles : ne pas envoyer d'informations personnelles identifiables (PII/PHI) à des services externes sans consentement et contrôle.
- Human-in-the-loop : pour sorties à risque (conseils nutritionnels personnalisés, diagnostics), valider par un expert humain.
- Prompts : stocker les prompts et versions, journaliser les résultats critiques pour traçabilité.
- Vérification : outputs d'IA doivent être vérifiés par les agents humains ou automatisés (tests, validation de sécurité).

Politique d'expérimentation : lab feature flags pour tester modèles et rollbacks rapides.

---

## 8. Tests

- Couverture : viser couverture raisonnable selon la criticité (unitaires pour logique, E2E pour parcours clés).
- Types de tests : unitaires, intégration, E2E, tests d'accessibilité, tests de performance occasionnels.
- CI : exécuter tests automatiquement sur chaque PR; bloquer merge si tests critiques échouent.
- Tests mobiles : inclure tests sur émulateurs/real devices pour interactions tactiles et DnD.
- Test data : anonymiser données réelles, utiliser fixtures et factories.

---

## 9. Documentation

- README : page d'accueil claire (setup, run, tests, conventions de commit).
- Docs techniques : API, architecture, diagrammes, design system, et endpoints critiques.
- Guides : démarrage rapide pour contributeurs, guide de style de code, guide d'accessibilité.
- CHANGELOG : tenir un journal clair des changements pour chaque release.
- Issues & RFCs : documenter décisions d'architecture via RFCs et lier aux tickets.

---

## Contrôles et conformité

- Relectures régulières : audits mensuels de sécurité, accessibilité et dette technique.
- Checklists PR : inclure items obligatoires (tests, docs, lint ok, sécurité scan).

---

Si vous souhaitez, je peux :

- Générer une checklist PR automatique (`.github/PULL_REQUEST_TEMPLATE.md`).
- Ajouter des workflows CI basiques (lint/test/security) via GitHub Actions.
- Créer des templates de tickets (issue templates) pour sécurité, incidents, et demandes de design.
