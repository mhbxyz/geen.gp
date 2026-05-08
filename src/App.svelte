<script>
  import Globe from './lib/Globe.svelte';

  const links = [
    { label: 'Le réseau', href: '#reseau' },
    { label: 'Membres', href: '#membres' },
    { label: 'Actualités', href: '#actus' },
    { label: 'Événements', href: '#agenda' }
  ];

  const stats = [
    { value: '355', label: 'membres visibles dans l’annuaire' },
    { value: '2', label: 'niveaux d’engagement simples' },
    { value: '98', label: 'rue de Sèvres, ancrage à Paris' }
  ];

  const benefits = [
    {
      title: 'Faire circuler les parcours',
      text: 'GeeN met en lumière les réussites, les projets et les récits de celles et ceux qui portent la Guadeloupe dans leur cœur.'
    },
    {
      title: 'Créer des passerelles concrètes',
      text: 'La plateforme relie diaspora, territoire, institutions, associations, entreprises et talents autour d’opportunités lisibles.'
    },
    {
      title: 'Garder un réseau vivant',
      text: 'Actualités, événements, groupes et annuaire donnent au réseau GeeN une présence continue, ouverte et évolutive.'
    }
  ];

  const features = [
    'Profil membre',
    'Annuaire',
    'Groupes',
    'Événements',
    'Actualités',
    'Petites annonces'
  ];

  const profiles = [
    {
      name: 'Chantal Loïal',
      field: 'Art / Danse',
      image: 'https://geen.gp/wp-content/uploads/2025/09/chantal-loial-1.jpg',
      text: 'Danseuse et chorégraphe, elle transmet la richesse des cultures caribéennes avec la Compagnie Difé Kako et le festival Mois Kréyol.'
    },
    {
      name: 'Garry Déféri',
      field: 'Art / Galerie',
      image: 'https://geen.gp/wp-content/uploads/2025/09/deferi.jpg',
      text: 'Fondateur de la Galerie Wawi à Paris, il défend un espace de rencontre entre artistes, événementiel et public.'
    },
    {
      name: 'Jean-Rony Leriche',
      field: 'Culinaire',
      image: 'https://geen.gp/wp-content/uploads/2025/10/Portrait-Leriche.png',
      text: 'Chef installé à Paris, il valorise les produits de Guadeloupe dans une gastronomie caribéenne contemporaine.'
    },
    {
      name: 'Jaky Sainsily',
      field: 'Mode',
      image: 'https://geen.gp/wp-content/uploads/2025/10/Portrait-wip.png',
      text: 'Créatrice de WI-PARIS SWIMWEAR, elle fait dialoguer héritage créole, savoir-faire et collaborations internationales.'
    }
  ];

  const news = [
    {
      tag: 'Football',
      title: 'Marcus Thuram champion d’Italie avec l’Inter Milan',
      image: 'https://geen.gp/wp-content/uploads/2026/01/GEN_IMG-1-1-1024x538.png'
    },
    {
      tag: 'Judo',
      title: 'Teddy Riner de retour à Lausanne en août',
      image: 'https://geen.gp/wp-content/uploads/2025/12/202512_IMG_GEEN_GEN-Arts-martiaux-1024x538.png'
    },
    {
      tag: 'Route du Rhum',
      title: '118 skippers au départ de Saint-Malo vers la Guadeloupe',
      image: 'https://geen.gp/wp-content/uploads/2026/04/202602_IMG_-57-1024x538.png'
    }
  ];

  const events = [
    {
      date: '18 fév. 2026',
      title: 'Joseph Decange en tournée avec Les Misérables',
      place: 'L’Amphithéâtre 3000, Lyon'
    },
    {
      date: '28 avr. 2026',
      title: 'Dominique Arron au Salon International du Livre d’Abidjan',
      place: 'Institut français de Côte d’Ivoire'
    },
    {
      date: '17 mai 2026',
      title: 'Kreyol Day, édition Food',
      place: 'Paris'
    }
  ];

  const levels = [
    {
      title: 'Membre',
      text: 'Suivre l’actualité, découvrir les initiatives et entrer en contact avec d’autres Guadeloupéen·nes dans le monde.'
    },
    {
      title: 'Ambassadeur·rice',
      text: 'Contribuer activement à la visibilité du réseau et devenir un relais GeeN dans son territoire ou son domaine.'
    }
  ];
</script>

<svelte:head>
  <title>reseau GeeN - La Guadeloupe est en nous</title>
  <meta
    name="description"
    content="GeeN est le réseau des Guadeloupéen·nes et de celles et ceux qui aiment la Guadeloupe, pour relier les parcours, les talents et les opportunités dans le monde."
  />
</svelte:head>

<div class="site-shell">
  <header class="site-header">
    <a class="brand-mark" href="#top" aria-label="Accueil reseau GeeN">
      <img src="https://geen.gp/wp-content/uploads/2025/09/GeeN-logo.png" alt="GeeN - La Guadeloupe est en Nous" />
    </a>

    <nav class="main-nav" aria-label="Navigation principale">
      {#each links as link}
        <a href={link.href}>{link.label}</a>
      {/each}
    </nav>

    <a class="header-cta" href="https://geen.gp/nous-rejoindre/">S’inscrire</a>
  </header>

  <main id="top">
    <section class="hero-section">
      <video class="hero-video" autoplay muted loop playsinline preload="metadata" poster="https://geen.gp/wp-content/uploads/2025/09/GeeN-logo.png">
        <source src="https://geen.gp/wp-content/uploads/2026/04/GEEN-HD_1.mp4" type="video/mp4" />
      </video>
      <div class="hero-overlay"></div>
      <Globe />

      <div class="hero-content">
        <p class="kicker hero-kicker">La Guadeloupe est en nous</p>
        <h1>
          <span>Le réseau des</span>
          <span>guadeloupéen·nes</span>
          <span>à travers le monde.</span>
        </h1>
        <p class="hero-copy">
          GeeN fait circuler les idées, les parcours, les opportunités et les projets pour créer des passerelles concrètes avec la Guadeloupe.
        </p>
        <div class="hero-actions">
          <a class="button button-primary" href="https://geen.gp/nous-rejoindre/">Rejoins GeeN</a>
          <a class="button button-secondary" href="#reseau">Explorer le réseau</a>
        </div>
      </div>

      <div class="hero-stats" aria-label="Chiffres clés">
        {#each stats as stat}
          <div>
            <strong>{stat.value}</strong>
            <span>{stat.label}</span>
          </div>
        {/each}
      </div>
    </section>

    <section id="reseau" class="intro-section">
      <div class="section-inner intro-grid">
        <div>
          <p class="kicker">Dé mo kat pawòl</p>
          <h2>GeeN relie les Guadeloupéen·nes d’ici et d’ailleurs.</h2>
        </div>
        <div class="intro-copy">
          <p>
            Pensé comme un réseau vivant, culturel et ouvert sur le monde, GeeN met en lumière les initiatives de la diaspora et crée des passerelles concrètes avec la Guadeloupe.
          </p>
          <p>
            Entreprises, associations, talents, événements, actualités et rencontres: la plateforme donne à voir une Guadeloupe qui rayonne bien au-delà de ses frontières.
          </p>
        </div>
      </div>
    </section>

    <section class="benefits-section">
      <div class="section-inner">
        <div class="section-heading">
          <p class="kicker">Pourquoi GeeN</p>
          <h2>Un lieu de rencontre et de reconnaissance.</h2>
        </div>
        <div class="benefit-grid">
          {#each benefits as benefit}
            <article class="benefit-card">
              <h3>{benefit.title}</h3>
              <p>{benefit.text}</p>
            </article>
          {/each}
        </div>
      </div>
    </section>

    <section class="tools-section">
      <div class="section-inner tools-grid">
        <div>
          <p class="kicker">Plateforme</p>
          <h2>Des outils publics pour rendre le réseau lisible.</h2>
        </div>
        <div class="feature-list" aria-label="Fonctionnalités GeeN">
          {#each features as feature}
            <span>{feature}</span>
          {/each}
        </div>
      </div>
    </section>

    <section id="membres" class="members-section">
      <div class="section-inner">
        <div class="section-heading split-heading">
          <div>
            <p class="kicker">Communauté</p>
            <h2>Ils nous ont rejoints.</h2>
          </div>
          <p>
            Des parcours variés: artistes, entrepreneur·es, professionnel·les, passionné·es de culture et amoureux·ses de la Guadeloupe.
          </p>
        </div>
        <div class="profile-grid">
          {#each profiles as profile}
            <article class="profile-card">
              <img src={profile.image} alt={`Portrait de ${profile.name}`} loading="lazy" />
              <div>
                <span>{profile.field}</span>
                <h3>{profile.name}</h3>
                <p>{profile.text}</p>
              </div>
            </article>
          {/each}
        </div>
      </div>
    </section>

    <section id="actus" class="news-section">
      <div class="section-inner">
        <div class="section-heading">
          <p class="kicker">Actus</p>
          <h2>Ce qui fait vibrer le réseau.</h2>
        </div>
        <div class="news-grid">
          {#each news as item}
            <article class="news-card">
              <img src={item.image} alt="" loading="lazy" />
              <div>
                <span>{item.tag}</span>
                <h3>{item.title}</h3>
              </div>
            </article>
          {/each}
        </div>
      </div>
    </section>

    <section id="agenda" class="agenda-section">
      <div class="section-inner agenda-grid">
        <div>
          <p class="kicker">Agenda</p>
          <h2>Des rendez-vous pour relier les territoires.</h2>
          <p class="section-copy">
            GeeN rassemble les événements culturels, économiques, sportifs et associatifs qui donnent corps au réseau.
          </p>
        </div>
        <div class="event-list">
          {#each events as event}
            <article>
              <time>{event.date}</time>
              <h3>{event.title}</h3>
              <p>{event.place}</p>
            </article>
          {/each}
        </div>
      </div>
    </section>

    <section class="levels-section">
      <div class="section-inner levels-grid">
        <div class="levels-copy">
          <p class="kicker">Engagement</p>
          <h2>Rejoindre GeeN, c’est simple.</h2>
          <p>
            Le réseau se construit pas à pas, au rythme de ses membres. Chacun·e peut suivre, partager, suggérer et contribuer à faire grandir les usages.
          </p>
        </div>
        <div class="level-cards">
          {#each levels as level}
            <article>
              <h3>{level.title}</h3>
              <p>{level.text}</p>
            </article>
          {/each}
        </div>
      </div>
    </section>

    <section class="final-cta">
      <div class="section-inner final-grid">
        <div>
          <p class="kicker">Maison de la Guadeloupe</p>
          <h2>Un ancrage à Paris, un réseau partout dans le monde.</h2>
          <p>
            GeeN prolonge le lien porté par la Maison de la Guadeloupe: accueillir, informer, fédérer et donner à chacun la possibilité de garder un lien vivant avec l’archipel.
          </p>
        </div>
        <address>
          <strong>98 rue de Sèvres</strong>
          <span>75007 Paris</span>
          <a class="button button-primary" href="https://geen.gp/nous-rejoindre/">Rejoins GeeN</a>
        </address>
      </div>
    </section>
  </main>
</div>
