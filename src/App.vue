<template>
  <header>
    <Navbar />
  </header>

  <main>
    <div class="presentation" ref="hero">
      <img :src="'/cartier1.webp'" alt="image" ref="heroImage">
      <h1 ref="heroTitle">{{ titre1 }}</h1>
    </div>

    <Session2 />
    <Session3 />
  </main>
</template>

<script>
import Navbar from './components/Navbar.vue';
import Session2 from './components/Session2.vue';
import Session3 from './components/Session3.vue';
import { gsap } from 'gsap';

export default {
  name: 'App',
  components: {
    Navbar,
    Session2,
    Session3
  },
  data() {
    return {
      titre1: "Henri Cartier-Bresson."
    };
  },
  mounted() {
    // Crée une timeline GSAP
    const tl = gsap.timeline({ defaults: { ease: "power2.out" } });
    
    // Animation du conteneur
    tl.from(this.$refs.hero, {
      opacity: 0,
      duration: 0.5
    });
    
    // Animation de l'image
    tl.from(this.$refs.heroImage, {
      scale: 1.2,
      opacity: 0,
      duration: 1.5
    }, "-=0.3"); // Chevauchement de 0.3s avec l'animation précédente
    
    // Animation du titre
    tl.from(this.$refs.heroTitle, {
      y: 50,
      opacity: 0,
      duration: 1
    }, "-=0.5"); // Chevauchement de 0.5s
  }
};
</script>

<style scoped>
main {
  min-height: 55vh;
  margin: 0 auto;
  padding: 2.5rem;
}

.presentation {
  height: 80%;
  width: 100%;
  position: relative;
  overflow: hidden; /* Cache le débordement pendant l'animation */
}

.presentation img {
  width: 100%;
  height: 690px;
  object-fit: cover;
  object-position: bottom;
  display: block; /* Évite l'espace sous l'image */
}

h1 {
  color: white;
  font-family: "Imbue", serif;
  font-weight: 200;
  font-size: 8rem;
  position: absolute;
  bottom: 2rem;
  left: 2rem;
  margin: 0;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5); /* Améliore la lisibilité */
}
</style>