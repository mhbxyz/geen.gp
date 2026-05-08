# Standard de design web GeeN

## Objectif
Transposer la charte graphique GeeN en un systeme de design web exploitable pour un site developpe avec Svelte + Tailwind, avec un rendu premium, epure, peu de mouvements, et un globe anime comme element signature.

---

## 1) Direction creative

### Positionnement visuel
- Atmosphere institutionnelle mais chaleureuse.
- Interface claire, lisible, orientee conversion.
- Moins de mouvement global, plus de precision dans les details.
- Equilibre entre ambition (reseau international) et accessibilite (proximite humaine).

### References cibles (mail de Manuella)
- Reference 1 (juste milieu): `https://fiasco.design/work/bayswater/?utm_source=Pinterest&utm_medium=organic`
  - Points a retenir: direction premium, structure editoriale maitrisee, composition hero forte.
- Reference 2 (moins de mouvements, plus epure): `https://www.salesgosses.re/`
  - Points a retenir: sobriete, respirations visuelles, hierarchie de contenu nette.

### Contraintes non negociables
- Presence du globe en mouvement.
- Respect strict de la charte couleur et du logotype GeeN.
- Respect de la denomination: toujours `reseau GeeN` (N majuscule).

---

## 2) Fondations de marque

### Palette officielle

#### Couleurs principales
- `forest-deep`: `#012b1b`
- `eucalyptus-dark`: `#20524c`
- `veronese`: `#14a45c`
- `water-light`: `#eaf8ec`
- `noir`: `#131313`

#### Couleurs secondaires
- `ocre-gold`: `#ffba20`
- `mint-celadon`: `#7ac49e`
- `yellow-bright`: `#ffec3d`
- `white-soft`: `#fdfff5`

#### Couleur accent
- `orange-vibrant`: `#ff5500`

### Typographies
- Titre / display: `Unbounded`
- Texte editorial / long: `Libre Baskerville`
- Texte interface (labels, boutons, formulaires): `DM Sans`

### Interdits (a appliquer sur le web)
- Ne pas inventer de couleurs hors palette.
- Ne pas deformer ou styliser le logo (rotation, ombre, contour, effets).
- Ne pas utiliser le logo blanc sur fond clair.
- Ne pas utiliser le logo sur image trop contrastee sans plaque de protection.
- Ne pas deformer les typographies (stretch, faux contour, faux bold).

---

## 3) Systeme de design (Svelte + Tailwind)

### 3.1 Tokens (CSS variables)
Definir les tokens dans `:root` et les exposer dans Tailwind.

```css
:root {
  --geen-forest-deep: #012b1b;
  --geen-eucalyptus-dark: #20524c;
  --geen-veronese: #14a45c;
  --geen-water-light: #eaf8ec;
  --geen-black: #131313;

  --geen-ocre-gold: #ffba20;
  --geen-mint-celadon: #7ac49e;
  --geen-yellow-bright: #ffec3d;
  --geen-white-soft: #fdfff5;

  --geen-orange-vibrant: #ff5500;

  --radius-sm: 0.5rem;
  --radius-md: 0.875rem;
  --radius-lg: 1.25rem;
  --radius-xl: 1.75rem;

  --shadow-soft: 0 8px 30px rgba(1, 43, 27, 0.08);
}
```

### 3.2 Configuration Tailwind (extrait)
```ts
// tailwind.config.ts
export default {
  theme: {
    extend: {
      colors: {
        geen: {
          forest: '#012b1b',
          eucalyptus: '#20524c',
          veronese: '#14a45c',
          water: '#eaf8ec',
          black: '#131313',
          ocre: '#ffba20',
          mint: '#7ac49e',
          yellow: '#ffec3d',
          white: '#fdfff5',
          orange: '#ff5500'
        }
      },
      fontFamily: {
        display: ['Unbounded', 'sans-serif'],
        serif: ['Libre Baskerville', 'serif'],
        sans: ['DM Sans', 'sans-serif']
      },
      boxShadow: {
        soft: '0 8px 30px rgba(1,43,27,.08)'
      }
    }
  }
}
```

### 3.3 Echelle typographique recommandee
- `display-xl`: 56/62 (desktop), 40/46 (mobile)
- `display-lg`: 44/50, 32/38
- `h1`: 36/42, 30/36
- `h2`: 28/34, 24/30
- `h3`: 22/28, 20/26
- `body-lg`: 20/32
- `body`: 18/30
- `body-sm`: 16/26
- `caption`: 14/22

Regles:
- Titres en `Unbounded`, textes de narration en `Libre Baskerville`, UI en `DM Sans`.
- Longs paragraphes limites a 70-80 caracteres par ligne.

### 3.4 Grille et spacing
- Container max: `1280px`.
- Gouttieres: `24px` desktop, `16px` mobile.
- Sections verticales: `py-24` desktop, `py-16` tablette, `py-12` mobile.
- Grille contenu: 12 colonnes desktop, 6 tablette, 4 mobile.

### 3.5 Composants de base
- Bouton primaire: fond `geen-forest`, texte `geen-white`, hover `geen-eucalyptus`.
- Bouton secondaire: fond transparent, bord `geen-forest`, texte `geen-forest`.
- Badge/macaron: variantes `opro`, `newsletter`, `participation` avec couleurs charte.
- Card preuve sociale: photo + role + localisation + metrique cle.
- Bloc citation: fond `geen-water`, accent `geen-ocre`.

### 3.6 Motion (sobre)
- Duree standard: `180ms` a `280ms`.
- Easing: `cubic-bezier(0.22, 1, 0.36, 1)`.
- Animations autorisees:
  - fade + translate Y leger (8-12px)
  - reveal stagger tres court
  - micro hover sur cartes (scale 1.01 max)
- Animations a eviter:
  - parallax agressif
  - rotations decoratives gratuites
  - loops visuelles parasites

### 3.7 Globe anime (pre-requis)
- Position: hero, visible above the fold.
- Role: symboliser connexions mondiales + fuseaux.
- Vitesse: lente et continue (ne jamais voler le focus du CTA).
- Interaction: survol optionnel (ralentir/mettre en evidence un reseau), aucun effet bruyant.
- Fallback mobile: version simplifiee (canvas leger / svg anime), max performance.

### 3.8 Accessibilite
- Contraste minimum WCAG AA sur textes et CTA.
- Etats focus visibles sur tous les elements interactifs.
- Respect `prefers-reduced-motion` pour minimiser l'animation.
- Alt texts descriptifs pour visuels editoriaux.
- Liens explicites (pas de "cliquez ici").

---

## 4) Architecture de landing recommandee

1. Hero (promesse + globe + CTA principal)
2. Pourquoi GeeN (3 benefices: visibilite, connexions, opportunites)
3. Pour qui (segments: etudiants, pros, assos, institutions, artistes, entrepreneurs)
4. Ce que permet la plateforme (profil, annuaire, groupes, evenements, actus)
5. Preuves sociales (membres, chiffres, temoignages)
6. Actualites/evenements (selection courte)
7. FAQ courte (5 questions)
8. CTA final (rejoindre / proposer son organisation / devenir partenaire)

Regle cle: un CTA principal dominant et repete, sans concurrence.

---

## 5) Iconographie et photographie

### Ligne editoriale visuelle
- Diversite de profils metiers et trajectoires.
- Scenes professionnelles concretes (bureau, tournage, conference, echange).
- Equilibre regards camera / scenes d'action.
- Traitement chaleureux (esprit filtre type Fresco 45% comme reference visuelle).

### Motifs graphiques derives de la charte
- Triangles lateraux de dynamisation (usage parcimonieux).
- Lignes de fond evoquant reseaux/fuseaux horaires.
- Textes surlignes pour appels de messages forts.

---

## 6) Fonds et textures web

Traduire les fonds de charte en versions web performantes:
- Fonds vert profond texture fine.
- Fonds jaune texture fine.
- Fonds vert/blanc degrade doux.

Implementation:
- preferer CSS gradients + grain leger optimise (webp/avif ou overlay svg tres compresse).
- eviter les images de fond lourdes pleine page non optimisees.

---

## 7) Conventions UX et contenu

- Voix: claire, directe, federatrice.
- Promesse orientee usage concret (pas uniquement institutionnelle).
- Sections courtes, scannables, avec preuves rapides.
- Aucun element BuddyBoss technique visible sur pages publiques.
- FR homogene, sans melange systeme FR/EN.

---

## 8) Checklist implementation Svelte + Tailwind

### Setup technique
- Installer polices via `@fontsource` ou chargement optimise.
- Declarer tokens dans `app.css`.
- Etendre `tailwind.config.ts` (colors, fonts, shadows, radius).
- Creer composants atomiques: `Button`, `Section`, `Badge`, `Stat`, `TestimonialCard`.

### Performance
- Budget hero media strict (images next-gen, lazy hors viewport).
- Globe charge de maniere progressive.
- Reduction du JS client sur pages marketing.

### QA
- Tests visuels desktop/mobile.
- Verification contrastes et focus states.
- Audit Lighthouse accessibilite + best practices.
- Validation `prefers-reduced-motion`.

---

## 9) Exemple de mapping pages -> style

- Home publique: premium epure, narrative, globe hero.
- Annuaire public: lisibilite + filtres clairs + cartes propres.
- Actualites: grille editoriale simple, accent couleur ponctuel.
- Pages membres (phase 2): style coherent mais plus utilitaire.

---

## 10) Definition of done (phase landing)

- Globe anime integre et stable sur desktop/mobile.
- Hero explicite en moins de 5 secondes de lecture.
- CTA principal unique, visible et repete.
- Direction visuelle alignee charte GeeN + references Manuella.
- Accessibilite et performance conformes aux standards modernes.

---

Ce document sert de base de production pour prototyper puis integrer la nouvelle landing GeeN sous Svelte + Tailwind, avec un niveau de finition presentable client sans ambiguite sur la direction graphique.
