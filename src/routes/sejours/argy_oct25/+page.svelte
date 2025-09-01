<script lang="ts">
	import { onMount } from 'svelte';
	import { fade } from 'svelte/transition';

	let currentSlide = $state(0);
	let isCarouselPlaying = $state(true);

	const castleImages = [
		'/argy/argy_castle_1.webp',
		'/argy/argy_castle_2.webp', 
		'/argy/argy_castle_3.webp',
		'/argy/argy_castle_4.webp'
	];

	const maxSlides = castleImages.length - 2; // Show 3 images at once

	onMount(() => {
		const interval = setInterval(() => {
			if (isCarouselPlaying) {
				currentSlide = (currentSlide + 1) % (maxSlides + 1);
			}
		}, 4000);

		return () => clearInterval(interval);
	});

	function goToSlide(index: number) {
		currentSlide = index;
		isCarouselPlaying = false;
		setTimeout(() => { isCarouselPlaying = true; }, 5000);
	}
</script>

<svelte:head>
	<title>Séjour méditation au Château d'Argy</title>
	<meta name="description" content="du vendredi 10 au lundi 13 octobre 2025" />
</svelte:head>

<div class="container">
	<!-- Hero Section -->
	<section class="hero" in:fade={{ duration: 800 }}>
		<div class="hero-content">
			<h1>Séjour méditation au Château d'Argy </h1>
			<p class="hero-subtitle">du vendredi 10 au lundi 13 octobre 2025</p>
			<div class="hero-dates">
				<!-- <span class="main-dates">du vendredi 10 au lundi 13 octobre 2025</span> -->
				<span class="weekend-option">(Possibilité de venir uniquement pour le weekend)</span>
			</div>
		</div>
	</section>

	<!-- Castle Images Carousel -->
	<section class="castle-gallery section">
		<div class="carousel-container">
			<button class="carousel-nav carousel-prev" onclick={() => goToSlide(Math.max(0, currentSlide - 1))} aria-label="Previous images">
				<svg viewBox="0 0 24 24" fill="currentColor">
					<path d="M15.41 7.41L14 6l-6 6 6 6 1.41-1.41L10.83 12z"/>
				</svg>
			</button>
			
			<div class="carousel-wrapper">
				<div class="carousel-track" style="transform: translateX(-{currentSlide * 33.33}%)">
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
			
			<button class="carousel-nav carousel-next" onclick={() => goToSlide(Math.min(maxSlides, currentSlide + 1))} aria-label="Next images">
				<svg viewBox="0 0 24 24" fill="currentColor">
					<path d="M8.59 16.59L10 18l6-6-6-6-1.41 1.41L13.17 12z"/>
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
			<h2>Programme</h2>
			
			<div class="meditation-highlight">
				<h3>Au moins 2 méditations par jour</h3>
				<p>Le matin et en fin d'après-midi.</p>
				<p>Lors des séjours les méditations sont le socle, le pilier qui permettent aux ateliers de prendre grâce.</p>
			</div>

			<div class="meditation-method">
				<h3>La méditation à induction (MI) comme instrument d'exploration</h3>
				<p>Une méditation simple, douce, naturelle et transparente. Sans mantras, symboles, rituels, imagerie, respirations et sans technique.</p>
				<p>La méditation à induction permet d'aller progressivement au-delà des états temporaires de relaxation intérieure et du bien-être psychophysique pour accéder aux aspects plus profonds et subtils de la conscience.</p>
				<p>Elle favorise les mécanismes de l'évolution et de la guérison à tous les niveaux. Durant la méditation, l'induction à des états de conscience différents se fait par les médiateurs expérimentés qui agissent comme des émetteurs sur les méditants-récepteurs en canalisant des fréquences subtiles et élevées.</p>
			</div>

			<div class="creative-workshops">
				<h3>Ateliers créatifs et artistiques</h3>
				<p>Autres ateliers selon les élans et les participants... selon la volonté de chacun.e</p>
			</div>
		</div>
	</section>

	<!-- Pricing Section -->
	<section class="section pricing-section section-alt" in:fade={{ duration: 800 }}>
		<div class="section-content">
			<h2>Tarifs</h2>
			
			<div class="pricing-cards">
				<div class="pricing-card">
					<h3>Séjour complet (4 jours)</h3>
					<div class="price-breakdown">
						<div class="price-item">
							<span>Location du gîte, salle méditation, chambre</span>
							<span>130€</span>
						</div>
						<div class="price-item">
							<span>Organisation du séjour et ateliers</span>
							<span>80€</span>
						</div>
						<div class="price-item">
							<span>Repas (30€/jour)</span>
							<span>120€</span>
						</div>
						<div class="price-item donation">
							<span>Donation pour le service spirituel (suggestion)</span>
							<span>120€</span>
						</div>
						<div class="price-total">
							<span>Total</span>
							<span>450€</span>
						</div>
					</div>
				</div>

				<div class="pricing-card">
					<h3>Weekend seulement (2 jours)</h3>
					<div class="price-breakdown">
						<div class="price-item">
							<span>Location du gîte, salle méditation, chambre</span>
							<span>130€</span>
						</div>
						<div class="price-item">
							<span>Organisation du séjour et ateliers</span>
							<span>80€</span>
						</div>
						<div class="price-item">
							<span>Repas</span>
							<span>80€</span>
						</div>
						<div class="price-item donation">
							<span>Donation pour le service spirituel (suggestion)</span>
							<span>80€</span>
						</div>
						<div class="price-total">
							<span>Total</span>
							<span>370€</span>
						</div>
					</div>
				</div>
			</div>
		</div>
	</section>

	<!-- Organizer Section -->
	<section class="section organizer-section" in:fade={{ duration: 800 }}>
		<div class="section-content">
			<h2>Organisateur et guide de méditation</h2>
			<p class="organizer-name">Elie Gauthey</p>
		</div>
	</section>

	<!-- Contact/Booking -->
	<section class="section contact-section" in:fade={{ duration: 800 }}>
		<div class="section-content">
			<h2>Réservation et contact</h2>
			<div class="contact-info">
				<a href="https://t.me/elie_lx" target="_blank" class="contact-btn">
					Réserver sur Telegram
				</a>
				<a href="https://instagram.com/elie.diy" target="_blank" class="contact-btn">
					Contact Instagram
				</a>
			</div>
		</div>
	</section>
</div>

<style>
	.container {
		width: 100%;
		overflow-x: hidden;
	}

	.hero {
		min-height: 60vh;
		display: flex;
		align-items: center;
		justify-content: center;
		background: linear-gradient(135deg, var(--color-secondary) 0%, var(--color-tertiary) 100%);
		color: white;
		text-align: center;
		padding: 8rem 1rem 4rem;
	}

	.hero-content h1 {
		font-family: 'Syne Mono', monospace;
		font-size: clamp(2.5rem, 6vw, 4rem);
		margin-bottom: 1rem;
		color: var(--color-primary);
	}

	.hero-subtitle {
		font-size: clamp(1.2rem, 3vw, 1.8rem);
		margin-bottom: 2rem;
		opacity: 0.9;
	}

	.hero-dates {
		display: flex;
		flex-direction: column;
		gap: 0.5rem;
	}

	/* .main-dates {
		font-size: clamp(1.1rem, 2.5vw, 1.4rem);
		font-weight: bold;
		color: var(--color-accent);
	} */

	.weekend-option {
		font-size: clamp(0.9rem, 2vw, 1.1rem);
		font-style: italic;
		opacity: 0.8;
	}

	/* Carousel Styles */
	.castle-gallery {
		padding: 4rem 0;
		background: linear-gradient(135deg, #f8f9fa 0%, #e9ecef 100%);
	}

	.carousel-container {
		position: relative;
		max-width: 1200px;
		margin: 0 auto;
		height: 450px;
		border-radius: 20px;
		overflow: hidden;
		/* box-shadow: 0 20px 40px rgba(0, 0, 0, 0.15); */
		background: linear-gradient(135deg, #f8f9fa 0%, #e9ecef 100%);

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

	.carousel-track {
		display: flex;
		width: 133.33%; /* 4 images × 33.33% = 133.33% */
		height: 100%;
		transition: transform 0.8s cubic-bezier(0.4, 0, 0.2, 1);
	}

	.carousel-slide {
		width: 33.33%;
		height: 100%;
		position: relative;
		flex-shrink: 0;
		padding: 0 8px;
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
		font-family: 'Syne Mono', monospace;
		font-size: clamp(2rem, 4vw, 2.5rem);
		color: var(--color-primary);
		margin-bottom: 2rem;
		text-align: center;
	}

	.section h3 {
		font-family: 'Syne Mono', monospace;
		font-size: clamp(1.2rem, 3vw, 1.5rem);
		color: var(--color-secondary);
		margin-bottom: 1rem;
	}

	.section p {
		font-size: clamp(1rem, 2vw, 1.125rem);
		color: var(--color-primary);
		line-height: 1.7;
		margin-bottom: 1.5rem;
	}

	/* Program Section */
	.meditation-highlight {
		background: rgba(12, 242, 93, 0.1);
		padding: 2rem;
		border-radius: 8px;
		margin-bottom: 3rem;
		border-left: 4px solid var(--color-accent);
	}

	.meditation-method,
	.creative-workshops {
		margin-bottom: 2rem;
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
	}

	/* Organizer Section */
	.organizer-section {
		text-align: center;
	}

	.organizer-name {
		font-family: 'Syne Mono', monospace;
		font-size: clamp(1.5rem, 3vw, 2rem);
		color: var(--color-accent);
		font-weight: bold;
	}

	/* Contact Section */
	.contact-section {
		background: var(--color-primary);
		color: white;
	}

	.contact-section h2 {
		color: var(--color-accent);
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
		color: var(--color-primary);
		background: var(--color-accent);
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
	}
</style>