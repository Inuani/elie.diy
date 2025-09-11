<script lang="ts">
	import { onMount } from 'svelte';
	import { fade } from 'svelte/transition';

	let currentSlide = $state(0);
	let isCarouselPlaying = $state(true);
	let isMobile = $state(false);

	const castleImages = [

		'/valfin/valfin_2.webp',
        '/valfin/valfin_8.webp',
		'/valfin/valfin_3.webp',
		'/valfin/valfin_5.webp',
		'/valfin/valfin_6.webp',
		// '/valfin/valfin_7.webp',
		'/valfin/valfin_9.webp',
		'/valfin/valfin_10.webp',
		'/valfin/valfin_11.webp',
		'/valfin/valfin_12.webp',
		'/valfin/valfin_13.webp',
        '/valfin/valfin_14.webp',
        '/valfin/valfin_1.webp',
        '/valfin/valfin_4.webp',
	];

	let maxSlides = $derived(isMobile ? castleImages.length - 1 : castleImages.length - 3);

	onMount(() => {
		// Check if mobile on mount and on resize
		const checkMobile = () => {
			isMobile = window.innerWidth <= 768;
		};

		checkMobile();
		window.addEventListener('resize', checkMobile);

		const interval = setInterval(() => {
			if (isCarouselPlaying) {
				currentSlide = (currentSlide + 1) % (maxSlides + 1);
			}
		}, 4000);

		return () => {
			clearInterval(interval);
			window.removeEventListener('resize', checkMobile);
		};
	});

	function goToSlide(index: number) {
		currentSlide = index;
		isCarouselPlaying = false;
		setTimeout(() => {
			isCarouselPlaying = true;
		}, 5000);
	}
</script>

<svelte:head>
	<title>Séjour méditation au gîte Valfin</title>
	<meta name="description" content="Séjour méditation du jeudi 13 au dimanche 16 novembre 2025" />
</svelte:head>

<div class="container">
	<!-- Hero Section -->
	<section class="hero" in:fade={{ duration: 800 }}>
		<div class="hero-content">
			<h1>Qui d'autre nous rejoins pour une rencontre méditation au gîte du château de Valfin?</h1>
			<p class="hero-subtitle">Une rencontre amicale du jeudi 13 au dimanche 16 novembre 2025</p>
			<div class="hero-dates">
				<span class="weekend-option">(Possibilité de venir uniquement pour le weekend)</span>
			</div>
		</div>
	</section>

	<!-- Castle Images Carousel -->
	<section class="castle-gallery section">
		<div class="gallery-header">
			<h3>Photos du gîte, château, cuisine, salon, chambres, nature aux alentours etc.</h3>
		</div>
		<div class="carousel-container">
			<button
				class="carousel-nav carousel-prev"
				onclick={() => goToSlide(Math.max(0, currentSlide - 1))}
				aria-label="Previous images"
			>
				<svg viewBox="0 0 24 24" fill="currentColor">
					<path d="M15.41 7.41L14 6l-6 6 6 6 1.41-1.41L10.83 12z" />
				</svg>
			</button>

			<div class="carousel-wrapper">
				<div
					class="carousel-track"
					style="transform: translateX(-{currentSlide * (isMobile ? 100 : 33.33)}%)"
				>
					{#each castleImages as image, index}
						<div class="carousel-slide">
							<img
								src={image}
								alt="Château d'Argy - Image {index + 1}"
								class="carousel-image"
								loading="lazy"
							/>
							<div class="image-overlay"></div>
						</div>
					{/each}
				</div>
			</div>

			<button
				class="carousel-nav carousel-next"
				onclick={() => goToSlide(Math.min(maxSlides, currentSlide + 1))}
				aria-label="Next images"
			>
				<svg viewBox="0 0 24 24" fill="currentColor">
					<path d="M8.59 16.59L10 18l6-6-6-6-1.41 1.41L13.17 12z" />
				</svg>
			</button>

			<div class="carousel-indicators">
				{#each Array(maxSlides + 1) as _, index}
					<button
						class="indicator"
						class:active={currentSlide === index}
						onclick={() => goToSlide(index)}
						aria-label="Slide {index + 1}"
					></button>
				{/each}
			</div>
		</div>
	</section>

	<!-- Program Section -->
	<section class="section program-section" in:fade={{ duration: 800 }}>
		<div class="section-content">
			<h2>Programme de la rencontre</h2>

			<div class="meditation-highlight">
				<h3>
					Je vous propose comme base pour cette rencontre deux méditations/jour (au minimum) 🧘🏼‍♀️🪷🧘‍♂️
				</h3>
			</div>
			<div class="program-flow">
				<p>
					Avec cette base, cette rencontre pourra se tisser organiquement selon vos inspirations et
					vos élans ...
				</p>
				<p>
					🎨 Activités créatives/artistique • 💃 Mouvements & Corps • 🗣️ Partages & Cercles • 🌿
					Connexion nature ...
				</p>
				<p>
					Que vous ayez des élans co-création ou pas vous êtes chaleureusement invité pour cette
					rencontre!
				</p>
			</div>
		</div>
	</section>

	<!-- Practical Info Section -->
	<section class="section practical-info-section" in:fade={{ duration: 800 }}>
		<div class="section-content">
			<h2>Infos pratiques</h2>

			<div class="info-grid">
				<div class="info-card">
					<div class="info-icon">🕐</div>
					<h3>Horaires</h3>
					<div class="schedule-item">
						<strong>Arrivée souhaitée:</strong>
						<span>Jeudi 13 novembre aux alentours de 15h</span>
					</div>
					<div class="schedule-item">
						<strong>Départ:</strong>
						<span>Dimanche 16 novembre aux alentours de 18h</span>
					</div>
					<div class="schedule-note">Pour ceux qui viennent le weekend: arrivée samedi matin idéalement avant 11h</div>
				</div>

                <div class="info-card">
					<div class="info-icon">📍</div>
					<h3>Lieu</h3>
					<p>Château de Valfin</p>
					<p>Rue du Château</p>
					<p>39240 Vosbles-Valfin, France</p>
					<!-- <a
						href="https://maps.google.com/maps?q=Château+d'Argy,+2+place+du+Château,+36500+Argy,+France"
						target="_blank"
						class="map-link"
					>
						Voir sur Google Maps →
					</a> -->
                    <h3>Accès</h3>
					<div class="access-item">
						<strong>En voiture:</strong>
						<span>1h30 depuis Genève ou Lyon, parking gratuit sur place</span>
					</div>
					<!-- <div class="access-item">
						<strong>En train:</strong>
						<span>Gare de Châteauroux (25 km) puis navette possible</span>
					</div> -->
					<div class="access-item">
						<strong>Covoiturage:</strong>
						<span>Organisation via le groupe WhatsApp</span>
					</div>
				</div>

				<!-- <div class="info-card">
					<div class="info-icon">🚗</div>
					<h3>Accès</h3>
					<div class="access-item">
						<strong>En voiture:</strong>
						<span>2h30 depuis Paris, parking gratuit sur place</span>
					</div>
					<div class="access-item">
						<strong>En train:</strong>
						<span>Gare de Châteauroux (25 km) puis navette possible</span>
					</div>
					<div class="access-item">
						<strong>Covoiturage:</strong>
						<span>Organisation via le groupe WhatsApp</span>
					</div>
				</div> -->

				<!-- <div class="info-card">
					<div class="info-icon">🎒</div>
					<h3>À prévoir</h3>
					<ul class="bring-list">
						<li>Coussin ou zafu de méditation (quelques-uns disponibles sur place)</li>
						<li>Tapis de yoga pour les pratiques corporelles</li>
						<li>Vêtements confortables</li>
						<li>Chaussures pour marche en nature</li>
						<li>Carnet de notes personnel</li>
						<li>Draps et serviettes (literie fournie)</li>
					</ul>
				</div> -->
			</div>

			<div class="map-container">
				<iframe
					src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d2752.994355129017!2d5.517478!3d46.369499999999995!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x478cb9002849db09%3A0xa70f348521ecfbb!2sCh%C3%A2teau%20de%20Valfin!5e0!3m2!1sfr!2sch!4v1756904695754!5m2!1sfr!2sch"
					width="100%"
					height="400"
					style="border:0;"
					allowfullscreen={true}
					loading="lazy"
					referrerpolicy="no-referrer-when-downgrade"
					title="Carte du Château d'Argy"
				>
				</iframe>
			</div>
		</div>
	</section>

	<!-- Pricing Section -->
	<section class="section pricing-section section-alt" in:fade={{ duration: 800 }}>
		<div class="section-content">
			<h2>Estimation du coût de la rencontre</h2>
			<h3>Pour contribuer à l'esprit d'une rencontre amicale, les coûts se veulent doux.</h3>

			<div class="pricing-cards">
				<div class="pricing-card">
					<h3>Séjour complet (4 jours et 3 nuits)</h3>
					<div class="price-breakdown">
						<div class="price-item">
							<span
								>Location salle méditation, cuisine, salon, salle à manger & chambre pour 3 nuits</span
							>
							<span>130€</span>
						</div>
						<div class="price-item">
							<span>Organisation du séjour</span>
							<span>60€</span>
						</div>
						<div class="price-item">
							<span>Repas (33€/jour)</span>
							<span>100€</span>
						</div>
						<div class="price-item donation">
							<span>Donation pour le service spirituel (suggestion)</span>
							<span>100€</span>
						</div>
						<div class="price-total">
							<span>Total</span>
							<span>~390€</span>
						</div>
					</div>
				</div>

				<div class="pricing-card">
					<h3>Weekend seulement (2 jours et 2 nuits)</h3>
					<div class="price-breakdown">
						<div class="price-item">
							<span
								>Location salle méditation, cuisine, salon, salle à manger & chambre pour 2 nuits</span>
							<span>100€</span>
						</div>
						<div class="price-item">
							<span>Organisation du séjour</span>
							<span>60€</span>
						</div>
						<div class="price-item">
							<span>Repas (33€/jour)</span>
							<span>66€</span>
						</div>
						<div class="price-item donation">
							<span>Donation pour le service spirituel (suggestion)</span>
							<span>80€</span>
						</div>
						<div class="price-total">
							<span>Total</span>
							<span>~310€</span>
						</div>
					</div>
				</div>
			</div>
			<div class="pricing-disclaimer">
				<p>
					<em
						>Ces estimations sont données à titre indicatif et peuvent varier suivant vos moyens,
						vos élans de soutien, du pays dans lequel vous travaillez, etc. bref on essa</em
					>
				</p>
			</div>
		</div>
	</section>

	<!-- Contact/Booking -->
	<section class="section contact-section" in:fade={{ duration: 800 }}>
		<div class="section-content">
			<h2>Nous sommes pour l'instant 7 participant.e.s,</h2>
			<h3>pour vous inscrire ou en savoir plus</h3>
			<div class="contact-info">
				<h3>📞 Contacter Élie au +41 76 385 07 26</h3>

				<a
					href="https://chat.whatsapp.com/FKowTmkOY2HGgAlkJTd46k"
					target="_blank"
					class="contact-btn"
				>
					Cliquez ici pour rejoindre le groupe whatsapp de la rencontre
				</a>
			</div>
		</div>
	</section>
</div>

<style>
	.section p,
	.price-item,
	.pricing-disclaimer p,
	.program-flow p,
	.hero-subtitle,
	.weekend-option {
		font-family: 'Inter', sans-serif;
		font-weight: 300;
	}

	.container {
		width: 100%;
		overflow-x: hidden;
	}

	.hero {
		min-height: 60vh;
		display: flex;
		align-items: center;
		justify-content: center;
		position: relative;
		color: var(--ocean-depths);
		text-align: center;
		padding: 4rem 1rem 4rem;
		overflow: visible;
		z-index: 1;
	}

	.hero::before {
		content: '';
		position: absolute;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		background:
			linear-gradient(rgba(255, 255, 255, 0.3), rgba(255, 255, 255, 0.6)),
			url('/argy/me_gibli_backgrd_right.png');
		background-position: 75% center;
		background-size: cover;
		background-repeat: no-repeat;
		z-index: -2;
	}

	.hero-content h1 {
		font-family: 'Syne Mono', monospace;
		font-size: clamp(2rem, 6vw, 3rem);
		margin-bottom: 1rem;
		color: var(--ocean-depths);
		text-shadow:
			2px 2px 0 #ffffff,
			-2px 2px 0 #ffffff,
			2px -2px 0 #ffffff,
			-2px -2px 0 #ffffff,
			0 0 8px #ffffff;
	}

	.hero-subtitle {
		font-size: clamp(1.2rem, 3vw, 1.8rem);
		margin-bottom: 2rem;
		opacity: 0.9;
		text-shadow:
			2px 2px 0 #ffffff,
			-2px 2px 0 #ffffff,
			2px -2px 0 #ffffff,
			-2px -2px 0 #ffffff,
			0 0 8px #ffffff;
	}

	.hero-dates {
		display: flex;
		flex-direction: column;
		gap: 0.5rem;
		font-family: 'JetBrains Mono', monospace;
		text-shadow:
			2px 2px 0 #ffffff,
			-2px 2px 0 #ffffff,
			2px -2px 0 #ffffff,
			-2px -2px 0 #ffffff,
			0 0 8px #ffffff;
	}

	.weekend-option {
		font-size: clamp(1.1rem, 2vw, 1.4rem);
		font-style: italic;
		font-family: 'JetBrains Mono', monospace;
	}

	/* Carousel Styles */

	.gallery-header {
		text-align: center;
		margin-bottom: 3rem;
	}

	.gallery-header h3 {
		font-family: 'Syne Mono', monospace;
		font-size: clamp(1.5rem, 3vw, 2rem);
		color: var(--ocean-depths);
		margin: 0;
	}

	.castle-gallery {
		padding: 4rem 0;
	}

	.carousel-container {
		position: relative;
		max-width: 1200px;
		margin: 0 auto;
		height: 450px;
		border-radius: 20px;
		overflow: hidden;
	}

	.carousel-nav {
		position: absolute;
		top: 50%;
		transform: translateY(-50%);
		z-index: 10;
		background: rgba(255, 255, 255, 0.9);
		backdrop-filter: blur(10px);
		border: none;
		width: 50px;
		height: 50px;
		border-radius: 50%;
		display: flex;
		align-items: center;
		justify-content: center;
		cursor: pointer;
		transition: all 0.3s ease;
		color: var(--ocean-depths);
		box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
	}

	.carousel-nav:hover {
		background: rgba(255, 255, 255, 1);
		transform: translateY(-50%) scale(1.1);
		box-shadow: 0 6px 20px rgba(0, 0, 0, 0.15);
	}

	.carousel-prev {
		left: 20px;
	}

	.carousel-next {
		right: 20px;
	}

	.carousel-nav svg {
		width: 24px;
		height: 24px;
	}

	.carousel-wrapper {
		position: relative;
		width: 100%;
		height: 100%;
		overflow: hidden;
	}

	.carousel-slide {
		width: calc(100% / 3);
		height: 100%;
		position: relative;
		flex-shrink: 0;
		padding: 0 8px;
		box-sizing: border-box;
	}

	.carousel-track {
		display: flex;
		height: 100%;
		transition: transform 0.8s cubic-bezier(0.4, 0, 0.2, 1);
	}

	.carousel-image {
		width: 100%;
		height: 100%;
		object-fit: cover;
		border-radius: 12px;
		transition: all 0.3s ease;
	}

	.carousel-slide:hover .carousel-image {
		transform: scale(1.05);
	}

	.image-overlay {
		position: absolute;
		top: 0;
		left: 8px;
		right: 8px;
		bottom: 0;
		background: linear-gradient(
			to bottom,
			transparent 0%,
			transparent 70%,
			rgba(0, 0, 0, 0.3) 100%
		);
		border-radius: 12px;
		opacity: 0;
		transition: opacity 0.3s ease;
		pointer-events: none;
	}

	.carousel-slide:hover .image-overlay {
		opacity: 1;
	}

	.carousel-indicators {
		position: absolute;
		bottom: 25px;
		left: 50%;
		transform: translateX(-50%);
		display: flex;
		gap: 12px;
		background: rgba(255, 255, 255, 0.2);
		backdrop-filter: blur(10px);
		padding: 10px 20px;
		border-radius: 25px;
	}

	.indicator {
		width: 10px;
		height: 10px;
		border-radius: 50%;
		border: none;
		background: rgba(255, 255, 255, 0.5);
		cursor: pointer;
		transition: all 0.3s ease;
		position: relative;
	}

	.indicator.active {
		background: var(--golden-sand);
		transform: scale(1.3);
		box-shadow: 0 0 10px rgba(212, 175, 122, 0.5);
	}

	.indicator:hover:not(.active) {
		background: rgba(255, 255, 255, 0.8);
		transform: scale(1.1);
	}

	/* Section Styles */
	.section {
		padding: 6rem 1rem;
	}

	.section-alt {
		background: linear-gradient(135deg, rgba(74, 111, 165, 0.1), rgba(30, 58, 95, 0.1));
	}

	.section-content {
		max-width: 48rem;
		margin: 0 auto;
	}

	.section h2 {
		font-family: 'Syne Mono', monospace;
		font-size: clamp(2rem, 4vw, 2.5rem);
		color: var(--ocean-depths);
		margin-bottom: 2rem;
		text-align: center;
	}

	.section h3 {
		font-family: 'Syne Mono', monospace;
		font-size: clamp(1.2rem, 3vw, 1.5rem);
		color: var(--twilight-blue);
		margin-bottom: 1rem;
	}

	.section p {
		font-size: clamp(1rem, 2vw, 1.125rem);
		color: var(--ocean-depths);
		line-height: 1.7;
		margin-bottom: 1.5rem;
	}

	/* Program Section */
	.meditation-highlight {
		background: rgba(212, 175, 122, 0.1);
		padding: 2rem;
		border-radius: 8px;
		margin-bottom: 3rem;
		border-left: 4px solid var(--golden-sand);
	}

	.program-flow {
		margin-top: 2rem;
		padding: 1.5rem;
		background: rgba(255, 255, 255, 0.5);
		border-radius: 8px;
		border-left: 4px solid var(--twilight-blue);
	}

	/* Practical Info Section */
	.practical-info-section {
		background: linear-gradient(135deg, rgba(255, 255, 255, 0.95), rgba(127, 179, 211, 0.1));
	}

	.info-grid {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
		gap: 2rem;
		margin: 3rem 0;
	}

	.info-card {
		background: white;
		border-radius: 12px;
		padding: 2rem;
		box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
		transition: all 0.3s ease;
		border-top: 3px solid var(--golden-sand);
	}

	.info-card:hover {
		transform: translateY(-4px);
		box-shadow: 0 8px 20px rgba(0, 0, 0, 0.12);
	}

	.info-icon {
		font-size: 2.5rem;
		margin-bottom: 1rem;
		text-align: center;
	}

	.info-card h3 {
		text-align: center;
		margin-bottom: 1.5rem;
		color: var(--ocean-depths);
		font-size: 1.3rem;
	}

	.info-card p {
		text-align: center;
		margin: 0.5rem 0;
		color: var(--ocean-depths);
		font-size: 1rem;
	}

	.map-link {
		display: inline-block;
		margin-top: 1rem;
		color: var(--twilight-blue);
		text-decoration: none;
		font-weight: 500;
		transition: color 0.3s ease;
		text-align: center;
		width: 100%;
	}

	.map-link:hover {
		color: var(--golden-sand);
	}

	.schedule-item,
	.access-item {
		display: flex;
		flex-direction: column;
		gap: 0.5rem;
		margin-bottom: 1rem;
		padding-bottom: 0.8rem;
		border-bottom: 1px solid rgba(30, 58, 95, 0.1);
	}

	.schedule-item:last-child,
	.access-item:last-child {
		border-bottom: none;
	}

	.schedule-item strong,
	.access-item strong {
		color: var(--twilight-blue);
		font-size: 0.9rem;
		text-transform: uppercase;
		letter-spacing: 0.5px;
	}

	.schedule-item span,
	.access-item span {
		color: var(--ocean-depths);
		font-size: 1rem;
	}

	.schedule-note {
		margin-top: 1rem;
		padding: 0.8rem;
		background: rgba(212, 175, 122, 0.15);
		border-radius: 6px;
		font-size: 0.95rem;
		font-style: italic;
		text-align: center;
		color: var(--twilight-blue);
	}

	.bring-list {
		list-style: none;
		padding: 0;
		margin: 0;
	}

	.bring-list li {
		position: relative;
		padding-left: 1.5rem;
		margin-bottom: 0.8rem;
		color: var(--ocean-depths);
		font-size: 0.95rem;
		line-height: 1.5;
	}

	.bring-list li::before {
		content: '✓';
		position: absolute;
		left: 0;
		color: var(--golden-sand);
		font-weight: bold;
	}

	.map-container {
		margin-top: 3rem;
		border-radius: 12px;
		overflow: hidden;
		box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
	}

	.map-container iframe {
		border-radius: 12px;
	}

	/* Pricing Section */
	.pricing-cards {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
		gap: 2rem;
		margin-top: 3rem;
	}

	.pricing-card {
		background: white;
		border-radius: 8px;
		padding: 2rem;
		box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
		border: 2px solid var(--golden-sand);
	}

	.pricing-card h3 {
		text-align: center;
		margin-bottom: 2rem;
		color: var(--ocean-depths);
	}

	.price-breakdown {
		display: flex;
		flex-direction: column;
		gap: 1rem;
	}

	.price-item {
		display: flex;
		justify-content: space-between;
		align-items: flex-start;
		padding: 0.5rem 0;
		border-bottom: 1px solid rgba(30, 58, 95, 0.2);
		color: var(--ocean-depths);
	}

	.price-item.donation {
		font-style: italic;
		color: var(--twilight-blue);
	}

	.price-total {
		display: flex;
		justify-content: space-between;
		font-weight: bold;
		font-size: 1.2rem;
		color: var(--ocean-depths);
		padding: 1rem 0 0;
		border-top: 2px solid var(--golden-sand);
		margin-top: 1rem;
		font-family: 'Inter', sans-serif;
	}

	.pricing-disclaimer p {
		margin: 1rem;
		color: var(--twilight-blue);
		font-size: 0.95rem;
	}

	/* Contact Section */
	.contact-section {
		background: var(--ocean-depths);
		color: white;
	}

	.contact-section h2 {
		color: var(--golden-sand);
	}

	.contact-section h3 {
		color: var(--golden-sand);
		display: flex;
		justify-content: center;
		font-size: 1.5rem;
		font-family: 'Inter', sans-serif;
	}

	.contact-info {
		display: flex;
		justify-content: center;
		gap: 2rem;
		flex-wrap: wrap;
	}

	.contact-btn {
		display: inline-block;
		font-family: 'Syne Mono', monospace;
		font-size: 1.1rem;
		color: var(--ocean-depths);
		background: var(--golden-sand);
		padding: 1rem 2rem;
		text-decoration: none;
		border-radius: 4px;
		transition: all 0.3s ease;
		font-weight: bold;
	}

	.contact-btn:hover {
		background: white;
		transform: translateY(-2px);
		box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
	}

	/* Responsive adjustments */
	@media (max-width: 768px) {
		.carousel-container {
			height: 300px;
		}

		.pricing-cards {
			grid-template-columns: 1fr;
		}

		.contact-info {
			flex-direction: column;
			align-items: center;
		}

		.carousel-slide {
			width: calc(100%);
			height: 100%;
			position: relative;
			flex-shrink: 0;
			padding: 0;
			box-sizing: border-box;
		}

		.info-grid {
			grid-template-columns: 1fr;
			gap: 1.5rem;
		}

		.info-card {
			padding: 1.5rem;
		}

		.map-container {
			margin-top: 2rem;
		}

		.map-container iframe {
			height: 300px;
		}
	}
</style>
