<template>
  <div class="description">
    <div class="body">
      <div class="text-container" ref="textContainer">
        <p id="text">
          <template v-for="(segment, index) in textSegments" :key="index">
            <span v-if="segment.isWord" class="mask">
              <span 
                class="word" 
                :class="{ visible: isVisible }"
                :style="{ transitionDelay: `${index * 0.02}s` }"
              >
                {{ segment.content }}
              </span>
            </span>
            <span v-else class="space">
              {{ segment.content }}
            </span>
          </template>
        </p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const textSegments = ref([]);
const isVisible = ref(false);
const textContainer = ref(null);

const originalText = 'Henri Cartier-Bresson (1908-2004) est l’un des photographes les plus influents du XXe siècle, considéré comme un pionnier du photojournalisme et de la photographie de rue. Né à Chanteloup-en-Brie, en France, il se passionne très tôt pour l’art et découvre la photographie après avoir été influencé par le surréalisme.';

onMounted(() => {
  // Découpage plus intelligent qui conserve tous les espaces
  const segments = [];
  let currentSegment = '';
  let isWord = false;
  
  for (const char of originalText) {
    if (char === ' ') {
      if (currentSegment && isWord) {
        segments.push({ content: currentSegment, isWord: true });
        currentSegment = '';
      }
      currentSegment += char;
      isWord = false;
    } else {
      if (currentSegment && !isWord) {
        segments.push({ content: currentSegment, isWord: false });
        currentSegment = '';
      }
      currentSegment += char;
      isWord = true;
    }
  }
  
  // Ajouter le dernier segment
  if (currentSegment) {
    segments.push({ content: currentSegment, isWord: isWord });
  }
  
  textSegments.value = segments;

  const observer = new IntersectionObserver(
    ([entry]) => {
      isVisible.value = entry.isIntersecting;
    },
    { threshold: 0.1 }
  );
  
  if (textContainer.value) {
    observer.observe(textContainer.value);
  }
});
</script>



<style scoped>
.description {
  padding: 2px;
  margin-top: 1rem;
}


.text-container {
  max-width: 100%;
}

.text-container p {
  border-top: 0.2px solid rgba(255, 255, 255, 0.315);
  padding-top: 15px;
  color: rgba(255, 255, 255, 0.516);
  font-size: 2.7rem;
  font-family: "Inter", sans-serif;
  font-weight: 500;
  width: 80%;

}

/* Animation */
.mask {
  display: inline-block;
  overflow: hidden;
  vertical-align: top;
}

.word {
  display: inline-block;
  transform: translateY(100%);
  transition: transform 0.4s cubic-bezier(0.16, 1, 0.3, 1);
  will-change: transform;
}

.word.visible {
  transform: translateY(0);
}
</style>