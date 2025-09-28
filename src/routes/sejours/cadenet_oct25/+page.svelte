<script lang="ts">
	import { onMount } from 'svelte';
	import { fade } from 'svelte/transition';

	let currentSlide = $state(0);
	let isCarouselPlaying = $state(true);
	let isMobile = $state(false);
	let selectedRoomPrice = $state(100);
	let selectedRoomPrice3Nights = $state(75);
	let selectedRoomPriceWeekend = $state(50);

	const castleImages = [
		'/cadenet/argy_castle_1.webp',
		'/cadenet/argy_group_1.webp',
		'/cadenet/argy_group_3.webp',
		'/cadenet/argy_castle_3.webp',
		'/cadenet/argy_group_2.webp',
		'/cadenet/argy_castle_4.webp',
		'/cadenet/argy_castle_5.webp',
		'/cadenet/argy_castle_6.webp',
		'/cadenet/argy_castle_8.webp',
		'/cadenet/argy_castle_9.webp',
		'/cadenet/argy_castle_2.webp',
		'/cadenet/argy_castle_10.webp',
		'/cadenet/argy_castle_7.webp'
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
	<title>Échos des petits princes d'Alleret</title>
	<meta name="description" content="Séjour du vendredi 10 au lundi 13 octobre 2025" />
	<link rel="preconnect" href="https://fonts.googleapis.com" />
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
	<link
		href="https://fonts.googleapis.com/css2?family=Crimson+Text:ital,wght@0,400;0,600;1,400&family=Source+Serif+Pro:ital,wght@0,300;0,400;0,500;0,600;1,300;1,400&display=swap"
		rel="stylesheet"
	/>
</svelte:head>

<div class="container">
	<!-- Hero Section -->
	<section class="hero" in:fade={{ duration: 800 }}>
		<div class="hero-content">
			<h1>
				Oui l'été se poursuit ... <br />
				la vibration du coeur aussi....
			</h1>
			<p class="hero-subtitle">
				Comme un écho aux séjours du Château d’Alleret, retrouvons-nous à la Fontaine de l’Aube pour
				partager la joie d'être ensemble du jeudi 23 au dimanche 26 octobre 2025
			</p>
			<div class="hero-dates">
				<span class="weekend-option">(Possibilité d'arriver le jour qui vous convient)</span>
			</div>
		</div>
	</section>

	<!-- Castle Images Carousel -->
	<section class="castle-gallery section">
		<div class="gallery-header">
			<h3>Photos de la fontaine de l'aube, alentours, cuisine, salon, chambres etc.</h3>
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
					La conscience en éveil, l'intelligence collective, le corps en mouvement, la voix, la
					méditation feront le terreau de ce moment auxquels pourront s’ajouter vos élans de
					contribution. 🧘🏼‍♀️🪷🧘‍♂️
				</h3>
			</div>
			<div class="program-flow">
				<p>
					Plus précisément nous pourrons retrouver : Pour les adultes La méditation avec Elie La
					joie en mouvement avec Stéphane L’échange ouvert et en conscience avec Sergio La voix du
					coeur avec Lydwine Les cercles de paroles Pour les familles Le dessin collectif : imaginer
					les racines de chaque élément avec Lydwine La danse libre avec Caroline 🎨 Activités
					créatives/artistique • 💃 Mouvements & Corps • 🗣️ Partages & Cercles • 🌿 Connexion nature
					...
				</p>
				<p>
					Avec cette base, cette rencontre pourra se tisser organiquement selon vos inspirations et
					vos élans ...
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
						<strong>Début de la rencontre:</strong>

						<span>jeudi 23 octobre 2025 à 19h</span>
						<span
							>Possibilité d’arriver la veille le mercredi 22 à partir de 17h pour profiter de la
							journée libre du jeudi</span
						>
						<div class="schedule-note">
							Pour ceux qui arrive le jeudi: arrivée avant 18h idéalement
						</div>
						<div class="schedule-note">
							Pour ceux qui viennent le weekend: arrivée vendredi soir idéalement
						</div>
					</div>

					<div class="schedule-item">
						<strong>Départ:</strong>
						<span>Dimanche 26 octobre à 16h au plus tard</span>
					</div>
				</div>

				<div class="info-card">
					<div class="info-icon">📍</div>
					<h3>Lieu</h3>
					<p>Fontaine de l'Aube</p>
					<p>11 Chem. de Lauris</p>
					<p>84160 Cadenet, France</p>
					<!-- <a
						href="https://maps.app.goo.gl/SNZb5xuArke3VNqaA"
						target="_blank"
						class="map-link"
					>
						Voir sur Google Maps →
					</a> -->
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

				<div class="info-card">
					<div class="info-icon">ℹ️</div>
					<h3>Infos supplémentaires</h3>
					<div class="access-item">
						<strong>Repas:</strong>
						<span>
							Les repas végétariens orchestrés par Caroline Cornelia sont prévus du jeudi soir au
							dimanche midi (Auto gestion pour le mercredi soir, jeudi matin et midi)
						</span>
					</div>
					<div class="access-item">
						<strong>Enfants - ados:</strong>
						<span>
							L’espace d’accueil étant réduit, la présence des enfants sera limitée à un enfant par
							adulte.
						</span>
					</div>

					<!-- <ul class="bring-list">
						<li>Coussin ou zafu de méditation (quelques-uns disponibles sur place)</li>
						<li>Tapis de yoga pour les pratiques corporelles</li>
						<li>Vêtements confortables</li>
						<li>Chaussures pour marche en nature</li>
						<li>Carnet de notes personnel</li>
						<li>Draps et serviettes (literie fournie)</li>
					</ul> -->
				</div>
			</div>

			<div class="map-container">
				<iframe
					src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d360.34918125013075!2d5.366863490833555!3d43.735617530911746!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x12ca1f31373325ad%3A0x8ce0102a6d357ad7!2sLa%20Fontaine%20de%20l&#39;Aube!5e0!3m2!1sfr!2sch!4v1758990782429!5m2!1sfr!2sch"
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
					<h3>Séjour à partir de mercredi (4 nuits)</h3>
					<div class="price-breakdown">
						<div class="price-item">
							<span>Location salles de la fontaine de l'Aube (10€/jour)</span>
							<span>40€ </span>
						</div>
						<div class="room-pricing-section">
							<div class="room-selector">
								<h4>Type d'hébergement :</h4>
								<div class="room-options">
									<div class="room-option">
										<input
											type="radio"
											id="room-3-4"
											name="room-type"
											value={100}
											checked
											bind:group={selectedRoomPrice}
										/>
										<label for="room-3-4">
											<div class="room-details">
												<span class="room-name">Chambre 3-4 personnes</span>
												<span class="room-price">25€/jour × 4 nuits</span>
											</div>
											<span class="total-price">100€</span>
										</label>
									</div>
									<div class="room-option">
										<input
											type="radio"
											id="room-2"
											name="room-type"
											value={120}
											bind:group={selectedRoomPrice}
										/>
										<label for="room-2">
											<div class="room-details">
												<span class="room-name">Chambre 2 personnes</span>
												<span class="room-price">30€/jour × 4 nuits</span>
											</div>
											<span class="total-price">120€</span>
										</label>
									</div>
									<div class="room-option">
										<input
											type="radio"
											id="camping"
											name="room-type"
											value={48}
											bind:group={selectedRoomPrice}
										/>
										<label for="camping">
											<div class="room-details">
												<span class="room-name">Camping</span>
												<span class="room-price">12€/jour × 4 nuits</span>
											</div>
											<span class="total-price">48€</span>
										</label>
									</div>
								</div>
							</div>
						</div>
						<div class="price-item">
							<span>Repas (25€/jour)</span>
							<span>100€</span>
						</div>
						<div class="price-item donation">
							<span>Donation en conscience pour l'organisation et le service (suggestion)</span>
							<span>100€</span>
						</div>
						<div class="price-total">
							<span>Total</span>
							<span>{240 + Number(selectedRoomPrice)}€</span>
						</div>
					</div>
				</div>

				<div class="pricing-card">
					<h3>Séjour à partir de jeudi (3 nuits)</h3>
					<div class="price-breakdown">
						<div class="price-item">
							<span>Location salles de la fontaine de l'Aube (10€/jour)</span>
							<span>30€</span>
						</div>
						<div class="room-pricing-section">
							<div class="room-selector">
								<h4>Type d'hébergement :</h4>
								<div class="room-options">
									<div class="room-option">
										<input
											type="radio"
											id="room-3-4-3nights"
											name="room-type-3nights"
											value={75}
											checked
											bind:group={selectedRoomPrice3Nights}
										/>
										<label for="room-3-4-3nights">
											<div class="room-details">
												<span class="room-name">Chambre 3-4 personnes</span>
												<span class="room-price">25€/jour × 3 nuits</span>
											</div>
											<span class="total-price">75€</span>
										</label>
									</div>
									<div class="room-option">
										<input
											type="radio"
											id="room-2-3nights"
											name="room-type-3nights"
											value={90}
											bind:group={selectedRoomPrice3Nights}
										/>
										<label for="room-2-3nights">
											<div class="room-details">
												<span class="room-name">Chambre 2 personnes</span>
												<span class="room-price">30€/jour × 3 nuits</span>
											</div>
											<span class="total-price">90€</span>
										</label>
									</div>
									<div class="room-option">
										<input
											type="radio"
											id="camping-3nights"
											name="room-type-3nights"
											value={36}
											bind:group={selectedRoomPrice3Nights}
										/>
										<label for="camping-3nights">
											<div class="room-details">
												<span class="room-name">Camping</span>
												<span class="room-price">12€/jour × 3 nuits</span>
											</div>
											<span class="total-price">36€</span>
										</label>
									</div>
								</div>
							</div>
						</div>
						<div class="price-item">
							<span>Repas (25€/jour)</span>
							<span>75€</span>
						</div>
						<div class="price-item donation">
							<span>Donation en conscience pour l'organisation et le service (suggestion)</span>
							<span>100€</span>
						</div>
						<div class="price-total">
							<span>Total</span>
							<span>{205 + Number(selectedRoomPrice3Nights)}€</span>
						</div>
					</div>
				</div>

				<div class="pricing-card">
					<h3>Weekend seulement (2 nuits)</h3>
					<div class="price-breakdown">
						<div class="price-item">
							<span>Location salles de la fontaine de l'Aube (10€/jour)</span>
							<span>20€</span>
						</div>
						<div class="room-pricing-section">
							<div class="room-selector">
								<h4>Type d'hébergement :</h4>
								<div class="room-options">
									<div class="room-option">
										<input
											type="radio"
											id="room-3-4-weekend"
											name="room-type-weekend"
											value={50}
											checked
											bind:group={selectedRoomPriceWeekend}
										/>
										<label for="room-3-4-weekend">
											<div class="room-details">
												<span class="room-name">Chambre 3-4 personnes</span>
												<span class="room-price">25€/jour × 2 nuits</span>
											</div>
											<span class="total-price">50€</span>
										</label>
									</div>
									<div class="room-option">
										<input
											type="radio"
											id="room-2-weekend"
											name="room-type-weekend"
											value={60}
											bind:group={selectedRoomPriceWeekend}
										/>
										<label for="room-2-weekend">
											<div class="room-details">
												<span class="room-name">Chambre 2 personnes</span>
												<span class="room-price">30€/jour × 2 nuits</span>
											</div>
											<span class="total-price">60€</span>
										</label>
									</div>
									<div class="room-option">
										<input
											type="radio"
											id="camping-weekend"
											name="room-type-weekend"
											value={24}
											bind:group={selectedRoomPriceWeekend}
										/>
										<label for="camping-weekend">
											<div class="room-details">
												<span class="room-name">Camping</span>
												<span class="room-price">12€/jour × 2 nuits</span>
											</div>
											<span class="total-price">24€</span>
										</label>
									</div>
								</div>
							</div>
						</div>
						<div class="price-item">
							<span>Repas (25€/jour)</span>
							<span>50€</span>
						</div>
						<div class="price-item donation">
							<span>Donation en conscience pour l'organisation et le service (suggestion)</span>
							<span>80€</span>
						</div>
						<div class="price-total">
							<span>Total</span>
							<span>{150 + Number(selectedRoomPriceWeekend)}€</span>
						</div>
					</div>
				</div>
			</div>
			<div class="pricing-disclaimer">
				<p>
					<em
						>Ces estimations sont données à titre indicatif et peuvent varier suivant vos moyens,
						vos élans de soutien, du pays dans lequel vous travailler, etc.</em
					>
				</p>
			</div>
		</div>
	</section>

	<!-- Contact/Booking -->
	<section class="section contact-section" in:fade={{ duration: 800 }}>
		<div class="section-content">
			<h2>Nous sommes pour l'instant 5 participant.e.s,</h2>
			<h3>pour vous inscrire ou en savoir plus</h3>
			<div class="contact-info">
				<h3>📞 Contacter Élie au +41 76 385 07 26</h3>

				<a
					href="https://chat.whatsapp.com/LQFz6HRhCV94ZH5PtmNpDT"
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
		font-family: 'Source Serif Pro', 'Georgia', serif;
		font-weight: 300;
		letter-spacing: 0.3px;
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
		color: var(--color-primary);
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
			linear-gradient(rgba(255, 255, 255, 0.45), rgba(255, 255, 255, 1)), url('/equipe_lpp.png');
		background-position: 55% center;
		background-size: cover;
		background-repeat: no-repeat;
		z-index: -2;
	}

	.hero-content h1 {
		font-family: 'Crimson Text', 'Times New Roman', serif;
		font-size: clamp(2rem, 6vw, 3rem);
		margin-bottom: 1rem;
		color: var(--color-primary);
		font-weight: 600;
		letter-spacing: 0.5px;
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
		font-family: 'Source Serif Pro', 'Georgia', serif;
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
		font-family: 'Source Serif Pro', 'Georgia', serif;
	}

	/* Carousel Styles */

	.gallery-header {
		text-align: center;
		margin-bottom: 3rem;
	}

	.gallery-header h3 {
		font-family: 'Crimson Text', 'Times New Roman', serif;
		font-size: clamp(1.5rem, 3vw, 2rem);
		color: var(--color-primary);
		margin: 0;
		font-weight: 500;
		letter-spacing: 0.3px;
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
		color: var(--color-primary);
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
		background: var(--color-accent);
		transform: scale(1.3);
		box-shadow: 0 0 10px rgba(12, 242, 93, 0.5);
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
		background: linear-gradient(135deg, rgba(2, 115, 94, 0.1), rgba(3, 65, 89, 0.1));
	}

	.section-content {
		max-width: 48rem;
		margin: 0 auto;
	}

	.section h2 {
		font-family: 'Crimson Text', 'Times New Roman', serif;
		font-size: clamp(2rem, 4vw, 2.5rem);
		color: var(--color-primary);
		margin-bottom: 2rem;
		text-align: center;
		font-weight: 600;
		letter-spacing: 0.5px;
	}

	.section h3 {
		font-family: 'Crimson Text', 'Times New Roman', serif;
		font-size: clamp(1.2rem, 3vw, 1.5rem);
		color: var(--color-secondary);
		margin-bottom: 1rem;
		font-weight: 500;
		letter-spacing: 0.3px;
	}

	.section p {
		font-size: clamp(1rem, 2vw, 1.125rem);
		color: var(--color-primary);
		line-height: 1.8;
		margin-bottom: 1.5rem;
		letter-spacing: 0.2px;
	}

	/* Program Section */
	.meditation-highlight {
		background: rgba(12, 242, 93, 0.1);
		padding: 2rem;
		border-radius: 8px;
		margin-bottom: 3rem;
		border-left: 4px solid var(--color-accent);
	}

	.program-flow {
		margin-top: 2rem;
		padding: 1.5rem;
		background: rgba(255, 255, 255, 0.5);
		border-radius: 8px;
		border-left: 4px solid var(--color-secondary);
	}

	/* Practical Info Section */
	.practical-info-section {
		background: linear-gradient(135deg, rgba(255, 255, 255, 0.95), rgba(12, 242, 93, 0.05));
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
		border-top: 3px solid var(--color-accent);
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
		color: var(--color-primary);
		font-size: 1.3rem;
	}

	.info-card p {
		text-align: center;
		margin: 0.5rem 0;
		color: var(--color-primary);
		font-size: 1rem;
	}

	.map-link {
		display: inline-block;
		margin-top: 1rem;
		color: var(--color-secondary);
		text-decoration: none;
		font-weight: 500;
		transition: color 0.3s ease;
		text-align: center;
		width: 100%;
	}

	.map-link:hover {
		color: var(--color-accent);
	}

	.schedule-item,
	.access-item {
		display: flex;
		flex-direction: column;
		gap: 0.5rem;
		margin-bottom: 1rem;
		padding-bottom: 0.8rem;
		border-bottom: 1px solid rgba(3, 65, 89, 0.1);
	}

	.schedule-item:last-child,
	.access-item:last-child {
		border-bottom: none;
	}

	.schedule-item strong,
	.access-item strong {
		color: var(--color-secondary);
		font-size: 0.9rem;
		text-transform: uppercase;
		letter-spacing: 0.5px;
	}

	.schedule-item span,
	.access-item span {
		color: var(--color-primary);
		font-size: 1rem;
	}

	.schedule-note {
		margin-top: 1rem;
		padding: 0.8rem;
		background: rgba(12, 242, 93, 0.1);
		border-radius: 6px;
		font-size: 0.95rem;
		font-style: italic;
		text-align: center;
		color: var(--color-secondary);
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
		color: var(--color-primary);
		font-size: 0.95rem;
		line-height: 1.5;
	}

	.bring-list li::before {
		content: '✓';
		position: absolute;
		left: 0;
		color: var(--color-accent);
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
		grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
		gap: 2rem;
		margin-top: 3rem;
	}

	.pricing-card {
		background: white;
		border-radius: 8px;
		padding: 2rem;
		box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
		border: 2px solid var(--color-accent);
	}

	.pricing-card h3 {
		text-align: center;
		margin-bottom: 2rem;
		color: var(--color-primary);
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
		border-bottom: 1px solid rgba(3, 65, 89, 0.2);
		color: var(--color-primary);
	}

	.room-pricing-section {
		padding: 0.5rem 0;
		border-bottom: 1px solid rgba(3, 65, 89, 0.2);
	}

	.room-selector h4 {
		margin: 0 0 1rem 0;
		color: var(--color-primary);
		font-size: 1rem;
		font-weight: 600;
	}

	.room-options {
		display: flex;
		flex-direction: column;
		gap: 0.75rem;
	}

	.room-option {
		position: relative;
	}

	.room-option input[type='radio'] {
		display: none;
	}

	.room-option label {
		display: flex;
		justify-content: space-between;
		align-items: center;
		padding: 1rem;
		border: 2px solid rgba(3, 65, 89, 0.2);
		border-radius: 8px;
		cursor: pointer;
		transition: all 0.3s ease;
		background: rgba(255, 255, 255, 0.5);
	}

	.room-option input[type='radio']:checked + label {
		border-color: var(--color-accent);
		background: rgba(255, 193, 7, 0.1);
		box-shadow: 0 2px 8px rgba(255, 193, 7, 0.3);
	}

	.room-option label:hover {
		border-color: var(--color-accent);
		background: rgba(255, 193, 7, 0.05);
	}

	.room-details {
		display: flex;
		flex-direction: column;
		gap: 0.25rem;
	}

	.room-name {
		font-weight: 600;
		color: var(--color-primary);
		font-size: 1rem;
	}

	.room-price {
		font-size: 0.875rem;
		color: var(--color-secondary);
	}

	.total-price {
		font-weight: bold;
		color: var(--color-primary);
		font-size: 1.125rem;
	}

	.room-option input[type='radio']:checked + label .total-price {
		color: var(--color-accent);
	}

	.price-item.donation {
		font-style: italic;
		color: var(--color-secondary);
	}

	.price-total {
		display: flex;
		justify-content: space-between;
		font-weight: bold;
		font-size: 1.2rem;
		color: var(--color-primary);
		padding: 1rem 0 0;
		border-top: 2px solid var(--color-accent);
		margin-top: 1rem;
		font-family: 'Source Serif Pro', 'Georgia', serif;
		letter-spacing: 0.2px;
	}

	.pricing-disclaimer p {
		margin: 1rem;
		color: var(--color-secondary);
		font-size: 0.95rem;
	}

	/* Contact Section */
	.contact-section {
		background: var(--color-primary);
		color: white;
	}

	.contact-section h2 {
		color: var(--color-accent);
	}

	.contact-section h3 {
		color: var(--color-accent);
		display: flex;
		justify-content: center;
		font-size: 1.5rem;
		font-family: 'Source Serif Pro', 'Georgia', serif;
		font-weight: 500;
		letter-spacing: 0.3px;
	}

	.contact-info {
		display: flex;
		justify-content: center;
		gap: 2rem;
		flex-wrap: wrap;
	}

	.contact-btn {
		display: inline-block;
		font-family: 'Source Serif Pro', 'Georgia', serif;
		font-size: 1.1rem;
		color: var(--color-primary);
		background: var(--color-accent);
		padding: 1rem 2rem;
		text-decoration: none;
		border-radius: 4px;
		transition: all 0.3s ease;
		font-weight: 600;
		letter-spacing: 0.3px;
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

		.room-option label {
			padding: 0.75rem;
			flex-direction: column;
			align-items: flex-start;
			gap: 0.5rem;
		}

		.room-details {
			width: 100%;
		}

		.total-price {
			align-self: flex-end;
			font-size: 1.25rem;
		}

		.room-selector h4 {
			font-size: 0.95rem;
		}

		.room-name {
			font-size: 0.95rem;
		}

		.room-price {
			font-size: 0.8rem;
		}
	}
</style>
