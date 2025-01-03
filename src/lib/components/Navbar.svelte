<script lang="ts">
  import { onMount } from "svelte";

  let isMenuOpen = $state(false);

  let isScrolled = $state(false);

  function handleScroll() {
  isScrolled = window.scrollY > 0; // Change background after scrolling 50px
}
  
  function toggleMenu() {
    isMenuOpen = !isMenuOpen;
  }

  function scrollToSection(id: string) {
    const element = document.getElementById(id);
    if (element) {
      element.scrollIntoView({ behavior: 'smooth' });
      isMenuOpen = false;
    }
  }

  onMount(() => {
  window.addEventListener('scroll', handleScroll);
  return () => {
    window.removeEventListener('scroll', handleScroll);
  };
});
</script>

<nav class="nav" class:scrolled={isScrolled}>
  <!-- <nav class="nav"> -->
  <div class="container">
    <div class="nav-content">
      <a href="/" class="logo">Elie.diy</a>
      
      <!-- Desktop Menu -->
      <div class="desktop-menu">
        <div class="menu-items">
          <button 
            onclick={() => scrollToSection('about')}
            aria-label="Scroll to About section">
            About
          </button>
          <button 
            onclick={() => scrollToSection('creations')}
            aria-label="Scroll to Creations section">
            Creations
          </button>
          <button 
            onclick={() => scrollToSection('rave')}
            aria-label="Scroll to RAVE section">
            RAVE
          </button>
          <button 
            onclick={() => scrollToSection('raygen')}
            aria-label="Scroll to RAVE section">
            Raygen
          </button>
          <button 
            onclick={() => scrollToSection('community')}
            aria-label="Scroll to Community section">
            Community_IDs
          </button>
          <button 
            onclick={() => scrollToSection('contact')}
            aria-label="Scroll to Community section">
            Contact
          </button>
          <a 
            href="https://instagram.com/elie.diy" 
            target="_blank" 
            rel="noopener noreferrer"
            aria-label="Visit Instagram profile"
            class="instagram-link">
            <svg class="instagram-icon" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
              <path fill-rule="evenodd" d="M12.315 2c2.43 0 2.784.013 3.808.06 1.064.049 1.791.218 2.427.465a4.902 4.902 0 011.772 1.153 4.902 4.902 0 011.153 1.772c.247.636.416 1.363.465 2.427.048 1.067.06 1.407.06 4.123v.08c0 2.643-.012 2.987-.06 4.043-.049 1.064-.218 1.791-.465 2.427a4.902 4.902 0 01-1.153 1.772 4.902 4.902 0 01-1.772 1.153c-.636.247-1.363.416-2.427.465-1.067.048-1.407.06-4.123.06h-.08c-2.643 0-2.987-.012-4.043-.06-1.064-.049-1.791-.218-2.427-.465a4.902 4.902 0 01-1.772-1.153 4.902 4.902 0 01-1.153-1.772c-.247-.636-.416-1.363-.465-2.427-.047-1.024-.06-1.379-.06-3.808v-.63c0-2.43.013-2.784.06-3.808.049-1.064.218-1.791.465-2.427a4.902 4.902 0 011.153-1.772A4.902 4.902 0 015.45 2.525c.636-.247 1.363-.416 2.427-.465C8.901 2.013 9.256 2 11.685 2h.63zm-.081 1.802h-.468c-2.456 0-2.784.011-3.807.058-.975.045-1.504.207-1.857.344-.467.182-.8.398-1.15.748-.35.35-.566.683-.748 1.15-.137.353-.3.882-.344 1.857-.047 1.023-.058 1.351-.058 3.807v.468c0 2.456.011 2.784.058 3.807.045.975.207 1.504.344 1.857.182.466.399.8.748 1.15.35.35.683.566 1.15.748.353.137.882.3 1.857.344 1.054.048 1.37.058 4.041.058h.08c2.597 0 2.917-.01 3.96-.058.976-.045 1.505-.207 1.858-.344.466-.182.8-.398 1.15-.748.35-.35.566-.683.748-1.15.137-.353.3-.882.344-1.857.048-1.055.058-1.37.058-4.041v-.08c0-2.597-.01-2.917-.058-3.96-.045-.976-.207-1.505-.344-1.858a3.097 3.097 0 00-.748-1.15 3.098 3.098 0 00-1.15-.748c-.353-.137-.882-.3-1.857-.344-1.023-.047-1.351-.058-3.807-.058zM12 6.865a5.135 5.135 0 110 10.27 5.135 5.135 0 010-10.27zm0 1.802a3.333 3.333 0 100 6.666 3.333 3.333 0 000-6.666zm5.338-3.205a1.2 1.2 0 110 2.4 1.2 1.2 0 010-2.4z" clip-rule="evenodd"></path>
            </svg>
          </a>
        </div>
      </div>
      
      <!-- Mobile menu button -->
      <button
        class="mobile-menu-button"
        onclick={toggleMenu}
        aria-label="Toggle menu"
        aria-expanded={isMenuOpen}
      >
        <svg
          class="menu-icon"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
          aria-hidden="true"
        >
          {#if isMenuOpen}
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
          {:else}
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
          {/if}
        </svg>
      </button>
    </div>
  </div>

  <!-- Mobile menu -->
  {#if isMenuOpen}
    <div class="mobile-menu">
      <div class="mobile-menu-items">
        <button
          onclick={() => scrollToSection('about')}
          aria-label="Scroll to About section"
        >
          About
        </button>
        <button
          onclick={() => scrollToSection('creations')}
          aria-label="Scroll to Creations section"
        >
          Creations
        </button>
        <button
          onclick={() => scrollToSection('rave')}
          aria-label="Scroll to RAVE section"
        >
          RAVE
        </button>
        <button
          onclick={() => scrollToSection('community')}
          aria-label="Scroll to Community section"
        >
          Community
        </button>
        <a
          href="https://instagram.com/elie.diy"
          target="_blank"
          rel="noopener noreferrer"
          aria-label="Visit Instagram profile"
        >
          Instagram
        </a>
      </div>
    </div>
  {/if}
</nav>

<style>
 .nav {
  position: fixed;
  width: 100%;
  transition: all 0.3s ease;
  z-index: 50;
}

/* Nav when at top */
.nav:not(.scrolled) {
  background-color: transparent;
}

/* Nav when scrolled */
.nav.scrolled {
  background-color: rgba(255, 255, 255, 0.6);
  backdrop-filter: blur(4px);
}

  .container {
    max-width: 1280px;
    margin: 0 auto;
    padding: 0 1rem;
  }

  .nav-content {
    display: flex;
    align-items: center;
    justify-content: space-between;
    height: 4rem;
  }

  .logo {
  font-family: 'Syne Mono', monospace;
  font-size: 2rem;
  color: var(--color-primary);
  text-decoration: none;
  display: block;
}

  

  .desktop-menu {
    display: block;
  }

  @media (max-width: 767px) {
    .desktop-menu {
      display: none;
    }
  }

  .menu-items {
  display: flex;
  align-items: baseline;
  gap: 0.5rem;
}

/* .menu-items button, .menu-items a {
  font-family: 'Syne Mono', monospace;
  font-size: 1.1rem;
  color: var(--color-primary);
  background: none;
  border: none;
  cursor: pointer;
 
  position: relative;
  padding: 0.5rem 1rem;
  transition: color 0.3s ease;
} */

.menu-items button, .menu-items a {
  font-family: 'Syne Mono', monospace;
  font-size: 1.1rem;
  color: var(--color-primary);
  background: none;
  border: none;
  cursor: pointer;
  position: relative;
  padding: 0.5rem 1rem;
  transition: all 0.3s ease;
  letter-spacing: normal;
}

.menu-items button:hover, .menu-items a:hover {
  letter-spacing: 0.15em; /* Spread letters on hover */
  text-decoration: underline;
}

.menu-items button::before, .menu-items a::before {
  z-index: -1;
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: var(--color-accent);
  transform: scale(0);
  /* opacity: 1; */
  transition: transform 0.3s ease;
  
}

.menu-items button:hover::before, .menu-items a:hover::before {
  transform: scale(1);
}

  .instagram-icon {
    width: 1.5rem;
    height: 1.5rem;
  }

  .mobile-menu-button {
    display: block;
    background: none;
    border: none;
    color: var(--color-primary);
    padding: 0.5rem;
    cursor: pointer;
  }

  .menu-icon {
    width: 1.5rem;
    height: 1.5rem;
  }

  .mobile-menu {
    background-color: rgba(3, 65, 89, 0.95);
    backdrop-filter: blur(4px);
  }

  .mobile-menu-items {
    padding: 0.5rem;
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
  }

  .mobile-menu-items button, .mobile-menu-items a {
    width: 100%;
    text-align: left;
    padding: 0.75rem;
    font-family: 'Syne Mono', monospace;
    color: white;
    background: none;
    border: none;
    cursor: pointer;
    transition: color 0.3s;
  }

  .mobile-menu-items button:hover, .mobile-menu-items a:hover {
    color: var(--color-accent);
  }

  @media (min-width: 768px) {
    .desktop-menu {
      display: block;
    }

    .mobile-menu-button {
      display: none;
    }
  }
</style>