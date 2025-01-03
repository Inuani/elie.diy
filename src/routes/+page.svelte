<script lang="ts">
	import { onMount } from 'svelte';
	import { fade } from 'svelte/transition';

	onMount(() => {
		const observer = new IntersectionObserver(
			(entries) => {
				entries.forEach((entry) => {
					if (entry.isIntersecting) {
						entry.target.classList.add('fade-in');
					}
				});
			},
			{ threshold: 0.1 }
		);

		document.querySelectorAll('.section').forEach((section) => {
			observer.observe(section);
		});

		return () => observer.disconnect();
	});
</script>

<div class="container">
	<!-- Hero Section -->
	<section class="hero">
		<div class="hero-overlay"></div>
		<div class="hero-content" in:fade={{ duration: 800, delay: 200 }}>
			<h1>Creative fashion explorer</h1>
			<p>
				blending the tactile worlds of upcycling & DIY art with blockchain technology pushing new
				boundaries of creativity.
			</p>
		</div>
	</section>

	<!-- About Section -->
	<section id="about" class="section">
		<div class="about-overlay"></div>
		<div class="section-content" in:fade={{ duration: 800, delay: 200 }}>
			<h2>About</h2>
			<p>
				My journey weaves together DIY fashion pieces, blockchain, 
				and community culture to create something entirely new. Each project is designed
				to explore, experiment, and push boundaries.
			</p>
			<p>
				This isn't just about crafting wearable art pieces authenticated on the blockchain – 
				I am opening new pathways for connection, ownership, value sharing, and community belonging 
				by associating a decentralised app with each physical creations.
				The deeper question driving my work is how to empower communities to fully shape 
				and own their identities and the collective value created.
			</p>
			<p>
				In these projects I feel guided and supported by forces beyond this dimension, progressively
				shaping the different aspects towards one direction. There's a sense of purpose in blending art, DIY
				practices, community engagement, and technology in creative ways, 
				a feeling that we're tapping into potential that will be transformative.
			</p>
		</div>
	</section>

	<!-- Creations Section -->
	<section id="creations" class="section">
		<div class="section-content-creations">
			<h2>Creations</h2>

			<!-- Collection Item -->
			<div class="collection">
				<h3>Spaceboot beta collection</h3>
				<div class="collection-images">
					<img src="/ocean_boots.webp" alt="Velcro Vision piece 2" loading="lazy" />
					<img src="/savana_boots.webp" alt="Velcro Vision piece 2" loading="lazy" />
					<img src="/bitpanda.webp" alt="Velcro Vision piece 3" loading="lazy" />
					<img src="/transpride.webp" alt="Velcro Vision piece 3" loading="lazy" />
					<img src="/kyle.webp" alt="Velcro Vision piece 3" loading="lazy" />
					<img src="/kofl.webp" alt="Velcro Vision piece 3" loading="lazy" />
				</div>
			</div>

			<!-- Collection Item -->
			<div class="collection">
				<h3>Collective canvas spectrum collection</h3>
				<div class="collection-images">
					<img src="/velcro_boots.webp" alt="Velcro Vision piece 3" loading="lazy" />
					<img src="/Got24.webp" alt="Velcro Vision piece 3" loading="lazy" />
					<img src="/kids.webp" alt="Velcro Vision piece 3" loading="lazy" />
				</div>
			</div>

			<!-- Collection Item -->
			<div class="collection">
				<h3>R3boot Outfit to come ...</h3>
				<div class="collection-images"></div>
			</div>
		</div>
	</section>

	<!-- RAVE Section -->
	<section id="rave" class="section section-alt" in:fade={{ duration: 800 }}>
		<div class="rave-overlay"></div>
		<div class="section-content">
			<h2>RAVE (real assets virtually extended)</h2>
			<p>
				RAVE assets bridge physical and digital worlds through NFC technology. Each creation carries
				one or several embedded NFC tags, forging a bond between the real asset to its digital
				counterpart on the blockchain.
			</p>
			<p>
				RAVE creations aren't simply authenticated items or static digital twins on the blockchain. 
				Every RAVE asset is coupled with a full-stack decentralized app, 
				creating dynamic ecosystems that function like miniature computers within each piece. 
				Through these digital extensions, physical creations become dynamic touchpoints that evolve, 
				enabling new forms of collective interaction, organization, and value creation.
			</p>
			<a href="https://raygen.diy" target="_blank" rel="noopener noreferrer" class="custom-btn">
				Discover RAVE project
			</a>
		</div>
	</section>

	<!-- Raygen Section -->
	<section id="raygen" class="section" in:fade={{ duration: 800 }}>
		<div class="section-content">
			<h2>Raygen</h2>
			<p>
				Raygen is a social project based in Switzerland that organizes DIY workshops and 
				events to create spaces for creativity, knowledge sharing 
				and connection through upcycling practices.
				We build environments where everyone becomes a creator,
				transforming upcycled materials into unique piece.
				From these creative gatherings emerge collaborative 
				artworks, where individual expressions blend into collective pieces or collections.
			</p>
			<a href="https://raygen.ch" target="_blank" rel="noopener noreferrer" class="custom-btn">
				Discover Raygen project
			</a>
		</div>
	</section>

	<!-- Community Section -->
	<section id="community" class="section section-alt" in:fade={{ duration: 800 }}>
		<div class="section-content">
			<h2>Community identities</h2>
			<p>
				I'm exploring how blockchain technology can revolutionize the way we think about brands,
				community ownership and value creation. By combining creative workshops, upcycled pieces,
				and decentralised technology, I am building tools for communities to create and truly own
				their collective identity.
			</p>
			<p>
				When a community exists and comes together - through events, gatherings, and shared
				experiences - they naturally create culture and value. This value, born from their essence
				and activities, belongs to them. Through RAVE technology, I am setting up the path that, as
				a community's identity grows, the benefits flow back to those who built it. 
			</p>
			<p>
				It's about building tools for communities to express their identity, 
				strengthen their bonds, grow and own the value created together. 
				Each piece becomes more than a fashion item - it's a share
				in the collective value created together.
			</p>
		</div>
	</section>

	<!-- Contact Section -->
	<section id="contact" class="section" in:fade={{ duration: 800 }}>
		<div class="section-content">
			<h2>Contact</h2>
			<div class="social-links">
				<a href="https://t.me/elie_lx" target="_blank" class="telegram-link">
					<img src="/telegram_icon.webp" alt="Telegram" class="telegram-icon" loading="lazy" />
				</a>
				<a href="https://instagram.com/elie.diy" target="_blank" class="instagram-link">
					<img src="/instagram_icon.png" alt="Instagram" class="instagram-icon" loading="lazy" />
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

	.section-content p {
		text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.4);
	}

	.hero {
		min-height: 100vh;
		position: relative;
		display: flex;
		align-items: center;
		justify-content: center;
		background-image: url('/velcro2.webp');
		background-size: cover;
		background-position: center;
		/* background-attachment: fixed; */
		margin-top: -4rem;
		padding-top: 4rem;
	}

	.hero-overlay {
		position: absolute;
		inset: 0;
		background: linear-gradient(
			to bottom,
			transparent,
			/* rgba(3, 65, 89, 0.8) 75%, */ /* rgba(255, 255, 255, 0.4), */
				/* var(--color-primary) 100% */ #fff 100%
		);
		z-index: 1;
	}

	.hero-content {
		position: relative;
		z-index: 2;
		text-align: center;
		padding: 0 1rem;
		max-width: 64rem;
		margin: 0 auto;
	}


	.hero h1 {
		font-family: 'Syne Mono', monospace;
		font-size: clamp(3rem, 8vw, 4rem); /* Responsive font size */
		color: var(--color-accent);
		margin-bottom: 1.5rem;
		text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.7);
	}

	.hero p {
   text-shadow: 
       2px 2px 0 #ffffff,
       -2px 2px 0 #ffffff,
       2px -2px 0 #ffffff,
       -2px -2px 0 #ffffff,
       0 0 8px #ffffff;
   font-size: clamp(1.1rem, 3vw, 1.5rem);
   max-width: 42rem;
   margin: 0 auto;
   color: var(--color-primary);
}

	#about {
		position: relative;
		background-image: url('/jp.webp');
		background-size: cover;
		background-position: center;
		background-attachment: fixed;
		padding: 8rem 1rem;
	}

	.about-overlay {
		position: absolute;
		inset: 0;
		background: linear-gradient(
			to bottom,
			#fff,
			rgba(255, 255, 255, 0.8) 30%,
			rgba(255, 255, 255, 0.7) 70%,
			#fff
		);
		z-index: 1;
	}

	.rave-overlay {
		position: absolute;
		inset: 0;
		background: linear-gradient(
			to bottom,
			#fff,
			rgba(255, 255, 255, 0.9) 30%,
			rgba(255, 255, 255, 0.8) 70%,
			#fff
		);
		z-index: 1;
	}

	#about .section-content,
	#rave .section-content {
		position: relative;
		z-index: 2;
	}

	.collection {
		margin-bottom: 4rem;
	}

	.collection h3 {
		font-family: 'Syne Mono', monospace;
		font-size: clamp(1.5rem, 3vw, 2rem);
		display: flex;
		justify-content: center;
		color: var(--color-secondary);
		margin-bottom: 1.5rem;
		text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.2);
	}

	.collection-images {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
		gap: 1.5rem;
		width: 100%;
	}

	.collection-images img {
		width: 100%;
		height: auto;
		aspect-ratio: 1;
		object-fit: cover;
		border-radius: 8px;
		transition: transform 0.3s ease;
	}

	.collection-images img:hover {
		transform: scale(1.1);
	}

	/* Responsive adjustments */
	@media (min-width: 768px) {
		.collection-images {
			grid-template-columns: repeat(3, 1fr);
		}
	}

	.section {
		padding: 6rem 1rem;
		position: relative;
	}

	.section-alt {
		background: linear-gradient(135deg, rgba(2, 115, 94, 0.1), rgba(3, 65, 89, 0.2));
	}

	.section-content {
		max-width: 48rem;
		margin: 0 auto;
		transition: transform 0.3s ease;
   		display: flex;
    	flex-direction: column;
    	align-items: center;
	}

	.section-content-creations {
		max-width: 70rem;
		margin: 0 auto;
		transition: transform 0.3s ease;
	}

	.section h2 {
		font-family: 'Syne Mono', monospace;
		font-size: clamp(2rem, 5vw, 3rem);
		color: var(--color-primary);
		margin-bottom: 2rem;
		text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.2);
	}

	.section p {
		font-size: clamp(1rem, 2vw, 1.125rem);
		color: var(--color-primary);
		line-height: 1.7;
		margin-bottom: 1.5rem;
		opacity: 0.9;
	}

	/* Add a subtle hover effect to sections */
	.section:hover .section-content {
		transform: translateY(-5px);
	}

	.section-content h2 {
    align-self: flex-start;
}

	#rave {
		position: relative;
		background-image: url('/cyp.webp');
		background-size: cover;
		background-position: center;
		background-attachment: fixed;
	}

	#community {
		position: relative;
		background-image: linear-gradient(rgba(255, 255, 255, 0.9), rgba(255, 255, 255, 0.9)),
			url('/communities.webp');
		background-size: cover;
		background-position: center;
		background-attachment: fixed;
		padding: 8rem 1rem;
	}

	#raygen {
		position: relative;
		background-image: linear-gradient(rgba(255, 255, 255, 0.6), rgba(255, 255, 255, 0.6)),
			url('/raygen.webp');
		background-size: 100%;
		background-repeat: no-repeat;
		background-position: center;
		background-attachment: fixed;
		padding: 8rem 1rem;
	}

	.social-links {
    display: flex;
    gap: 2rem;  /* Space between icons */
    justify-content: center;
}

	.instagram-icon,
	.telegram-icon {
		width: 48px; /* You can adjust this size */
		height: 48px;
		transition: transform 0.3s ease;
	}

	.instagram-icon:hover,
	.telegram-icon:hover {
		transform: scale(1.1);
	}

	.instagram-link,
	.telegram-link {
		display: inline-block;
		text-decoration: none;
	}

	.custom-btn {
		display: inline-block;
		font-family: 'Syne Mono', monospace;
		font-size: 1.1rem;
		color: var(--color-primary);
		background: var(--color-accent);;
		border: none;
		cursor: pointer;
		position: relative;
		padding: 0.75rem 1.5rem;
		transition: all 0.3s ease;
		letter-spacing: normal;
		text-decoration: none;
	}

	.custom-btn:hover {
		letter-spacing: 0.15em;
		background: var(--color-accent);;
		transform: translateY(-2px); /* Slight lift effect */
		box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1); /* Shadow on hover */
		text-decoration: underline;
	}

	.custom-btn:active {
		transform: translateY(0); /* Press effect */
	}
</style>
