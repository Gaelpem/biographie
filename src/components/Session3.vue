<template>
    <div class="photos-list">
      <div 
        v-for="(photo, index) in photos" 
        :key="index" 
        class="photo"
        @mouseenter="showImage(index, $event)"
        @mouseleave="hideImage(index)"
      >
        <div class="photo-wrapper">
          <div class="photo-name">
            <h1>{{ photo.name }}</h1>
            <h1>{{ photo.type }}</h1>
          </div>
        </div>
      </div>
  
      <!-- Afficher les images dynamiquement -->
      <img 
        v-for="(img, idx) in activeImages" 
        :key="idx" 
        :src="img.src" 
        :alt="img.alt" 
        :style="img.style"
      />
    </div>
  </template>
  
  <script>
  import { ref } from "vue";
  import gsap from "gsap";
  
  export default {
    setup() {
      // Liste des awards (identique à ton tableau)
      const photos = ref([
        { name: "01", type: "Children" },
        { name: "02", type: "Silver" },
        { name: "03", type: "Portrait" },
        { name: "04", type: "People" },
      ]);
  
      // Tableau pour stocker les images actives
      const activeImages = ref([]);
      const imageExtensions = ['.jpg', '.webp', '.webp', '.jpg'];
  
      // Afficher l'image au survol
      const showImage = (index, e) => {
        const imgNumber = index + 1;
        const imgExtension = imageExtensions[index] || '.jpg';
  
        // Créer un objet pour l'image
        const newImg = {
          src: `./img/${imgNumber}${imgExtension}`,
          alt: `Award ${imgNumber}`,
          style: {
            position: "absolute",
            top: `${e.clientY - (-400)}px`, // Centre l'image sur la souris
            left: `${e.clientX - 100}px`,
            width: "400px",
            height: "400px",
            objectFit: "cover",
            scale: "0",
            zIndex: 1000,
          },
          index: index, // Pour identifier quelle image supprimer
        };
  
        // Ajouter l'image au tableau
        activeImages.value.push(newImg);
  
        // Animer l'image avec GSAP
        gsap.to(newImg.style, {
          scale: 1,
          duration: 0.4,
          ease: "power2.out",
        });
      };
  
      // Cacher l'image quand la souris quitte
      const hideImage = (index) => {
        const imgToRemove = activeImages.value.find(img => img.index === index);
        if (imgToRemove) {
          gsap.to(imgToRemove.style, {
            scale: 0,
            duration: 0.4,
            ease: "power2.out",
            onComplete: () => {
              // Supprimer l'image du tableau après l'animation
              activeImages.value = activeImages.value.filter(img => img.index !== index);
            },
          });
        }
      };
  
      return {
        photos,
        activeImages,
        showImage,
        hideImage,
      };
    },
  };
  </script>
  
  <style scoped>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  
  body {
    background-color: #ffffff;
    font-family: Arial, Helvetica, sans-serif;
  }
  
  img {
    position: absolute;
    width: 100%;
    height: 100%;
    object-fit: cover;
    will-change: transform;
  }
  
  h1 {
    text-transform: uppercase;
    font-size: 72px;
    line-height: 0.9;
  }
  
  p {
    text-transform: uppercase;
    font-size: 1.5rem;
    font-weight: 700;
  }
  
  section {
    position: relative;
    width: 100vw;
    height: 100vh;
    overflow: hidden;
  }
  
  .photos {
    min-height: 100vh;
    height: max;
  }
  
  .photos p {
    padding: 5px 20px;
  }
  
  .photos-list {
    margin-top: 4.5rem;
    border-top: 0.5px solid white;
 
  }
  
  .photo {
    height: 80px;
    clip-path: polygon(0 0, 100% 0, 100% 100%, 0 100%);
  }
  
  .photo-wrapper {
    position: relative;
    height: 240px;
    will-change: transform;
    transform: translateY(0);
  }
  
  .photo-name {
    width: 100%;
    display: flex;
    justify-content: space-between;
    align-items: center;
    height: 80px;
    padding: 5px 15px;
    cursor: pointer;
    border-bottom: 0.5px solid #ffffff;
    background-color: #000000;
    color: #ffffff;
    transition: all 0.6s ease-out;
  }
  

  </style>