<template>
    <div class="awards-list">
      <div 
        v-for="(award, index) in awards" 
        :key="index" 
        class="award"
        @mouseenter="showImage(index, $event)"
        @mouseleave="hideImage"
      >
        <div class="award-wrapper">
          <div class="award-name">
            <h1>{{ award.name }}</h1>
            <h1>{{ award.type }}</h1>
          </div>
        </div>
      </div>
    </div>
  
    <img 
      v-if="currentImg" 
      :src="currentImg" 
      :alt="`Award ${currentIndex + 1}`" 
      :style="imgStyle"
    />
  </template>
  
  <script>
  import { ref } from "vue";
  import gsap from "gsap";
  
  export default {
    setup() {
      // Liste des awards
      const awards = ref([
        { name: "Photo One", type: "Children" },
        { name: "Photo Two", type: "Silver" },
        { name: "Photo Three", type: "Portrait" },
        { name: "Photo Four", type: "People" },
      ]);
  
      // Image actuelle affichée
      const currentImg = ref(null);
      const currentIndex = ref(null);
      const imgStyle = ref({});
  
      // Tableau des extensions d’image
      const imageExtensions = [".jpg", ".webp", ".webp", ".jpg"];
  
      // Afficher l'image quand la souris entre
      const showImage = (index, e) => {
        const imgNumber = index + 1;
        const imgExtension = imageExtensions[index] || ".jpg";
        currentImg.value = `/img/${imgNumber}${imgExtension}`;
        currentIndex.value = index;
  
        // Positionner l’image sous la souris
        imgStyle.value = {
          position: "absolute",
          top: `${e.clientY - 100}px`,
          left: `${e.clientX - 100}px`,
          width: "400px",
          height: "400px",
          objectFit: "cover",
          zIndex: 1000,
          pointerEvents: "none",
          scale: 0, // Initialement caché
        };
  
        // Animation GSAP pour agrandir l'image
        gsap.to(imgStyle.value, {
          scale: 1,
          duration: 0.4,
          ease: "power2.out",
        });
      };
  
      // Cacher l’image quand la souris sort
      const hideImage = () => {
        gsap.to(imgStyle.value, {
          scale: 0,
          duration: 0.4,
          ease: "power2.out",
          onComplete: () => {
            currentImg.value = null;
            currentIndex.value = null;
          },
        });
      };
  
      return {
        awards,
        currentImg,
        currentIndex,
        imgStyle,
        showImage,
        hideImage,
      };
    },
  };
  </script>
  
  <style scoped>
  
img{
    position: absolute;
    width: 100%;
    height: 100%;
    object-fit: cover;
    will-change: transform;

}

h1{
    text-transform: uppercase;
    font-size: 72px;
    line-height: 0.9;
}

p{
    text-transform: uppercase; 
    font-size: 1.5rem;
    font-weight: 700;
}

section{
    position:relative; 
    width: 100vw;
    height: 100vh;
    overflow: hidden;
}


.awards{
    min-height: 100vh;
  height: max;
}

.awards p{
    padding: 5px 20px;
}

.awards-list{
    border: 0.5px solid #000;
}
.award{
    height: 80px;
    clip-path: polygon(0 0, 100% 0, 100% 100%, 0 100%);
}

.award-wrapper{
    position: relative;
    height: 240px;
    will-change: transform;
    transform: translateY(0);
}

.award-name{
    width: 100%;
    display: flex;
    justify-content: space-between;
    align-items: center;
    height: 80px;
    padding: 5px 15px;
    cursor: pointer;
    border-bottom: 1px solid #000;
    background-color: #ffffff;
    color: #000000;
    transition:all  0.6s ease-out;
}

.award-name:hover{
    background-color: rgb(0, 0, 0);
    color: rgb(255, 255, 255);
}

  </style>
  