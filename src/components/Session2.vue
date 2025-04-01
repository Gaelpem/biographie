<template>
  <div class="description">
    <div class="body">
      <p ref="textElement" id="text">
        {{ originalText }}
      </p>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, nextTick } from 'vue';

const textElement = ref(null);
const originalText = "Henri Cartier-Bresson (1908-2004) est l’un des photographes les plus influents du XXe siècle, considéré comme un pionnier du photojournalisme et de la photographie de rue. Né à Chanteloup-en-Brie, en France, il se passionne très tôt pour l’art et découvre la photographie après avoir été influencé par le surréalisme.";

onMounted(() => {
  if (!textElement.value) return;

  textElement.value.textContent = '';
  const wordsAndSpaces = originalText.split(/(\s+)/).filter(item => item.length > 0);

  wordsAndSpaces.forEach((item, index) => {
    if (item.trim() !== '') {
      const span = document.createElement('span');
      span.classList.add('mask');

      const innerSpan = document.createElement('span');
      innerSpan.classList.add('word');
      innerSpan.textContent = item;
      innerSpan.style.transitionDelay = `${index * 0.05}s`;

      span.appendChild(innerSpan);
      textElement.value.appendChild(span);
    } else {
      textElement.value.appendChild(document.createTextNode(item));
    }
  });

  nextTick(() => {
    const observer = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          const words = textElement.value.querySelectorAll('.word');
          if (entry.isIntersecting) {
            words.forEach(word => word.classList.add('visible'));
          }
        });
      },
      { threshold: 0.1 }
    );
    observer.observe(textElement.value);
  });
});
</script>

<style scoped>
.description {
  border: 1px solid rgb(255, 255, 255);
  padding: 50px;
}
.body p {
  color: white;
  font-size: 1.5rem;
  font-family: Impact, sans-serif; 
  width: 60%;
}
:deep(.mask) {
  display: inline-block;
  overflow: hidden;
}
:deep(.word) {
  display: inline-block;
  transform: translateY(100%);
  transition: transform 0.3s ease;
}
:deep(.word.visible) {
  transform: translateY(0);
}
</style>