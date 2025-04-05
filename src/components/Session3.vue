<template>


    <div class="container-rond">
        <div class="rond one"></div>
        <div class="rond two"></div>
        <div class="rond three"></div>
        <div class="rond fourth"></div> 
        <div class="rond five"></div>
        <div class="rond six"></div>
    </div>

  <div class="photo-container">
    <h1 class="title">{{ title }}</h1>
    <div class="photos-list">
      <div 
        v-for="(photo, index) in photos" 
        :key="index" 
        class="photo-item"
        @mouseenter="showImage(index, $event)"
        @mouseleave="hideImage(index)"
        @mousemove="updateImagePosition(index, $event)"
      >
        <div class="photo-wrapper">
          <div class="photo-name">
            <h1>{{ photo.name }}</h1>
            <h1 class="trait">{{ photo.trait }}</h1>
            <h1>{{ photo.type }}</h1>
          </div>
        </div>
        
        <!-- Image de survol -->
        <img 
          v-if="activeImages[index]"
          :src="activeImages[index].src" 
          :alt="activeImages[index].alt" 
          :style="activeImages[index].style"
          class="hover-image"
        />
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
import gsap from "gsap";

export default {
  data() {
    return {
      title: 'photographie.',
    }
  },
  setup() {
    const photos = ref([
      { name: "01-", type: "Children" },
      { name: "02-", type: "Silver" },
      { name: "03-", type: "Portrait" },
      { name: "04-", type: "People" },
      { name: "05-", type: "Alicante" },
      { name: "06-", type: "Madrid" },  
      { name: "07-", type: "Alberto Giacometti" },
      { name: "08-", type: "Japon" },
      { name: "09-", type: "Boston" },
      { name: "10-", type: "Martine Frank" }
    ]);

    const activeImages = ref([]);
    const imageExtensions = ['.jpg', '.webp', '.webp', '.jpg', '.webp', '.webp', '.webp', '.webp', '.webp', '.jpg'];

    const showImage = (index, e) => {
      const imgNumber = index + 1;
      const imgExtension = imageExtensions[index] || '.jpg';

      if (!activeImages.value[index]) {
        activeImages.value[index] = {
          src: `./img/${imgNumber}${imgExtension}`,
          alt: `Photo ${imgNumber}`,
          style: {
            position: "fixed",
            top: `${e.clientY - 200}px`,
            left: `${e.clientX - 200}px`,
            width: "400px",
            height: "400px",
            objectFit: "cover",
            scale: 0.5,
            opacity: 0,
            zIndex: 1000,
            pointerEvents: "none",
            transformOrigin: "center center",
            filter: "brightness(1.1) contrast(1.1)",
            boxShadow: "0 0 30px rgba(0,0,0,0.5)"
          }
        };
      }

      // Animation plus dynamique avec un effet "qui sort"
      gsap.to(activeImages.value[index].style, {
        scale: 1.5,
        opacity: 1,
        duration: 0.6,
        ease: "back.out(1.7)",
        y: -50, // Fait "sortir" l'image vers le haut
        rotation: gsap.utils.random(-5, 5) // Légère rotation aléatoire
      });
    };

    const updateImagePosition = (index, e) => {
      if (activeImages.value[index]) {
        gsap.to(activeImages.value[index].style, {
          top: `${e.clientY - 200}px`,
          left: `${e.clientX - 200}px`,
          duration: 0.2
        });
      }
    };

    const hideImage = (index) => {
      if (activeImages.value[index]) {
        gsap.to(activeImages.value[index].style, {
          scale: 0.5,
          opacity: 0,
          duration: 0.5,
          ease: "back.in(1.5)",
          y: 50, // Fait "rentrer" l'image vers le bas
          onComplete: () => {
            activeImages.value[index] = null;
          }
        });
      }
    };

    return {
      photos,
      activeImages,
      showImage,
      hideImage,
      updateImagePosition
    };
  }
};
</script>

<style scoped>

.photo-container {
  display: flex; 
  flex-direction: column;
  margin-left: 30rem;
  margin-top: 3rem;
  
}

.title {
  text-transform: uppercase;
  color: white;
  font-size: 7rem;
  border-bottom: 0.7px solid white;
  font-family: "Josefin Sans", sans-serif;
}

.photo-name h1 {
  text-transform: uppercase;
  font-size: 2rem;
  line-height: 0.9;
  font-weight: 300;
  font-family: "Inter", sans-serif;
  margin: 0;
}

.photos-list {
  max-width: 67vw;
  margin-top: 4.5rem;
  border-top: 0.8px solid rgba(255, 255, 255, 0.105);
}

.photo-item {
  position: relative;
  height: 80px;
  clip-path: polygon(0 0, 100% 0, 100% 100%, 0 100%);
}

.photo-wrapper {
  position: relative;
  height: 100%;
  will-change: transform;
}

.photo-name {
  padding: 0 1rem;
  position: relative;
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 80px;
  cursor: pointer;
  border-bottom: 0.8px solid rgba(255, 255, 255, 0.105);
  color: #ffffff;
  transition: all 0.3s ease-out;
  z-index: 1;
}

.photo-name:hover {
  background-color: rgba(255, 255, 255, 0.105);
  transform: translateX(10px);
}

.hover-image {
  position: fixed;
  width: 400px;
  height: 400px;
  object-fit: cover;
  will-change: transform, opacity;
  border-radius: 5px;
  transition: all 0.3s ease;
}


</style>