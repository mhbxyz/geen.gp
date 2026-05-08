# Dossier de refonte GeeN - Implémentation du plan

## Livrable 1 - Audit fusionné (complet)

### Résumé exécutif

Le projet GeeN a une vraie valeur de fond (mission claire, matière éditoriale, membres, annuaire, actualités), mais l’exécution actuelle est en décalage avec l’ambition institutionnelle.

Le problème principal n’est pas uniquement visuel. Il est structurel :
- proposition de valeur trop générique et trop tardive,
- landing page surchargée (marketing + média + communauté + technique),
- mélange non maîtrisé entre vitrine publique et mécanique BuddyBoss,
- parcours d’inscription peu convaincant,
- qualité de finition inégale,
- dette front visible (chargements, erreurs, composants parasites).

Conclusion stratégique :
- **refaire la landing page est indispensable**,
- **puis engager une refonte progressive du reste**,
- avec séparation claire entre **site public d’acquisition** et **plateforme membre**.

---

## 1) Ce qui ne va pas (constats consolidés)

### 1.1 Positionnement / message

- Hero actuel compréhensible mais trop abstrait (intention > bénéfice).
- Promesse peu orientée usage concret.
- Valeur utilisateur insuffisamment exprimée en 5-10 secondes.
- Peu de preuve sociale mise en scène dès le haut de page.

Conséquence : faible conversion visiteur froid -> inscription.

### 1.2 Landing page trop chargée

- La home mélange : manifeste, actus, profils, widgets de groupes, newsletter, éléments communautaires, scripts globe/chat, etc.
- Aucun rôle dominant clair (conversion, média, portail, institutionnel).
- Progression narrative faible.

Conséquence : charge cognitive forte, sensation de fouillis, dilution du CTA.

### 1.3 CTA et conversion

- Multiples CTA concurrents (`Se connecter`, `S’inscrire`, `Newsletter`, `Actualités`, etc.).
- Pas de CTA principal dominant et répétable.

Conséquence : décision retardée, intention d’inscription affaiblie.

### 1.4 Navigation / architecture

- Navigation trop portail, peu orientée parcours.
- Fonctions internes communautaires exposées trop tôt.

Conséquence : compréhension lente des priorités du produit.

### 1.5 Mélange marketing vs plateforme communautaire

- Widgets/éléments BuddyBoss visibles publiquement.
- Composants `Report`, `Block Member?`, etc. visibles dans les pages publiques.
- Connexion via `wp-login.php`.
- Sur la page membres : liens `http://messages/` et `http://notifications/` remontés.

Conséquence : impression “WordPress brut”, baisse de crédibilité.

### 1.6 Inscription / onboarding

- Formulaire long exposé tôt (email, mot de passe, type, alias, centres d’intérêt…).
- Inscription pensée comme collecte, pas comme conversion progressive.
- Éléments parasites visibles dans le rendu analysable.

Conséquence : friction au moment clé.

### 1.7 Contenu / éditorial

- Beaucoup de matière mais hiérarchie faible.
- Discours institutionnel parfois trop déclaratif.
- Qualité textuelle inégale (typos/formulations, mélange FR/EN dans des composants).

Conséquence : perception de produit inachevé.

### 1.8 Annuaire / qualité de données

- Longues listes brutes.
- Nombreux avatars par défaut.
- Doublons ou quasi-doublons visibles.
- Normalisation insuffisante des fiches.

Conséquence : perte de confiance dans la valeur de l’annuaire.

### 1.9 Crédibilité institutionnelle

- Rattachement à la Maison de la Guadeloupe => attente élevée.
- Exécution web perçue en dessous du standard attendu.

Conséquence : décalage ambition / perception.

### 1.10 SEO (stratégique)

- Base indexable correcte, mais home trop générique sémantiquement.
- Potentiel SEO réel sous-exploité (intentions qualifiées diaspora/annuaire/acteurs).

Conséquence : acquisition organique non optimisée business.

### 1.11 Accessibilité et qualité front

- Lighthouse observé : Accessibilité 93 / Best Practices 96 / SEO 100.
- Problèmes réels malgré tout : contrastes footer, noms de liens, alt incohérents, bruit DOM.

Conséquence : le score technique ne compense pas les défauts UX/produit.

### 1.12 Surcharge technique visible

- ~225 requêtes observées sur la home au chargement inspecté.
- Multiples plugins/SDK/frontends chargés simultanément.
- Erreur 400 AJAX MEC, warnings Three.js (duplication/deprecation), logs globe répétés.

Conséquence : page lourde, maintenance fragile, signal de dette technique.

### 1.13 Cohérence de domaine

- Page `GeeN Connect` avec CTA vers `geen.fr` alors que plateforme auditée sur `geen.gp`.

Conséquence : confusion potentielle d’écosystème de marque.

---

## 2) Ce qu’il faut faire maintenant (implémentation du plan)

## Phase 1 - Refonte landing page (priorité absolue)

Objectif : clarifier la proposition de valeur et augmenter les inscriptions.

### 2.1 Structure cible de la nouvelle home

1. **Hero clair**
- Titre orienté promesse
- Sous-titre orienté bénéfice
- CTA principal : `Rejoindre le réseau gratuitement`
- CTA secondaire : `Explorer l’annuaire`
- Preuves immédiates : membres, profils, activité

2. **Pourquoi GeeN ?**
- Visibilité
- Connexions
- Opportunités

3. **Pour qui ?**
- Particuliers, pros, assos, institutions, étudiants, artistes, entrepreneurs

4. **Ce que permet la plateforme**
- Profil, annuaire, groupes, événements, actus, contribution

5. **Preuves sociales**
- Membres mis en avant
- Chiffres clés
- Témoignages

6. **Actualités/événements (courts)**
- 3 actus max
- 2-3 événements max

7. **FAQ courte**
- 5 questions essentielles

8. **CTA final**
- Rejoindre / proposer son organisation / devenir partenaire

### 2.2 Ce qu’on retire de la home

- Widgets communautaires non stratégiques en footer
- Composants BuddyBoss visibles
- Sections vides/erreurs
- Surcharge d’actus
- Éléments techniques parasites

---

## Phase 2 - Nettoyage UX plateforme

Objectif : supprimer l’effet “WordPress brut”.

- Login custom
- Inscription custom/progressive
- Traduction complète des messages systèmes visibles
- Nettoyage modales/report/block exposées publiquement
- Cohérence navigation publique vs membre

---

## Phase 3 - Refonte progressive produit

Objectif : fiabiliser la valeur communautaire.

- Dédoublonnage et normalisation annuaire
- Gouvernance des fiches (validation, qualité)
- Recherche/filtres mieux orientés usage
- Amélioration parcours membre
- Gouvernance éditoriale des actus/événements

---

## 3) Backlog priorisé (actionnable)

### Sprint 0 (1-2 semaines)

- Cadrage proposition de valeur
- Audit contenu + inventaire CTA
- Schéma IA public vs membre
- Spécification de la nouvelle home

### Sprint 1 (2-3 semaines)

- Wireframe + copy de la landing
- UI responsive
- Intégration home
- Nettoyage footer public
- QA conversion mobile/desktop

### Sprint 2 (2-3 semaines)

- Refonte inscription/connexion
- Onboarding progressif
- Nettoyage composants communautaires exposés

### Sprint 3 (3-5 semaines)

- Normalisation annuaire
- Réduction surcharge scripts sur pages marketing
- Corrections erreurs JS/AJAX visibles
- Optimisation performance ciblée home/pages publiques

---

## 4) Proposition commerciale prête à l’emploi

## Option A - Mission d’entrée (landing page)

Objectif : vitrine claire, crédible, orientée inscription.

Inclus :
- audit UX rapide,
- réécriture message,
- nouvelle structure de page,
- design responsive,
- intégration,
- SEO de base,
- CTA et preuves sociales optimisées.

## Option B - Mission stratégique (refonte progressive)

Objectif : transformation complète et maîtrisée de l’écosystème GeeN.

Inclus :
- refonte landing page,
- refonte inscription/connexion,
- harmonisation UI/UX,
- nettoyage BuddyBoss visible,
- refonte annuaire et qualité data,
- stratégie SEO éditoriale,
- documentation et gouvernance.

---

## 5) Angle de communication recommandé

À éviter :
- “votre site est nul”
- “on va juste faire plus joli”

À dire :

> Vous avez déjà le fond, la mission et la matière. Ce qui manque aujourd’hui, c’est une couche produit/UX à la hauteur pour rendre cette valeur immédiatement lisible et crédible. On commence par une landing page performante, puis on structure la refonte progressive de la plateforme.

---

## Verdict final

- Oui, la home doit être refaite immédiatement.
- Oui, l’opportunité commerciale est forte.
- Oui, la meilleure trajectoire est : **landing page d’abord, refonte progressive ensuite**.

Le projet GeeN ne manque pas d’idée ni de contenu. Il manque d’exécution structurée, de hiérarchie produit et de crédibilité perçue. C’est exactement là où la refonte apporte de la valeur rapidement.
