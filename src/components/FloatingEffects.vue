<template>
  <div>
    <!-- Corazones flotantes mejorados -->
    <div class="hearts-container">
      <div 
        v-for="heart in hearts" 
        :key="heart.id"
        class="floating-heart"
        :style="{
          left: heart.left + '%',
          animationDelay: heart.animationDelay + 's',
          fontSize: heart.size + 'px'
        }"
      >
        {{ heart.color }}
      </div>
    </div>

    <!-- Destellos mágicos -->
    <div class="sparkles-container">
      <div 
        v-for="sparkle in sparkles" 
        :key="sparkle.id"
        class="sparkle"
        :style="{
          left: sparkle.left + '%',
          top: sparkle.top + '%',
          animationDelay: sparkle.animationDelay + 's',
          fontSize: sparkle.size + 'px'
        }"
      >
        ✨
      </div>
    </div>

    <!-- Elementos románticos flotantes -->
    <div class="romantic-container">
      <div 
        v-for="element in romanticElements" 
        :key="element.id"
        class="romantic-float"
        :style="{
          left: element.left + '%',
          top: element.top + '%',
          animationDelay: element.animationDelay + 's',
          fontSize: element.size + 'px'
        }"
      >
        <span>{{ element.emoji }}</span>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const hearts = ref([])
const sparkles = ref([])
const romanticElements = ref([])

onMounted(() => {
  // Crear corazones flotantes
  for (let i = 0; i < 30; i++) {
    hearts.value.push({
      id: i,
      left: Math.random() * 100,
      animationDelay: Math.random() * 4,
      size: Math.random() * 30 + 15,
      color: ['💖', '💕', '💗', '💝', '🌸', '🎀', '💐'][Math.floor(Math.random() * 7)]
    })
  }
  
  // Crear destellos mágicos
  for (let i = 0; i < 25; i++) {
    sparkles.value.push({
      id: i,
      left: Math.random() * 100,
      top: Math.random() * 100,
      animationDelay: Math.random() * 3,
      size: Math.random() * 20 + 10
    })
  }

  // Crear elementos románticos flotantes
  for (let i = 0; i < 8; i++) {
    romanticElements.value.push({
      id: i,
      left: Math.random() * 100,
      top: Math.random() * 100,
      animationDelay: Math.random() * 5,
      size: Math.random() * 25 + 20,
      emoji: ['💖', '💕', '👑', '🌹', '💎'][Math.floor(Math.random() * 5)]
    })
  }
})
</script>

<style scoped>
.hearts-container, .sparkles-container, .romantic-container {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: 1;
}

.floating-heart, .sparkle, .romantic-float {
  position: absolute;
  opacity: 0.8;
}

.floating-heart {
  animation: floatUpHeart 6s infinite ease-in-out;
}

.sparkle {
  animation: sparkleShine 3s infinite ease-in-out;
}

.romantic-float {
  animation: romanticFloat 8s infinite ease-in-out;
  cursor: pointer;
  z-index: 100;
  pointer-events: auto;
}

@keyframes floatUpHeart {
  0% {
    transform: translateY(100vh) rotate(0deg) scale(0.5);
    opacity: 0;
  }
  15% {
    opacity: 1;
    transform: scale(1);
  }
  85% {
    opacity: 1;
  }
  100% {
    transform: translateY(-100px) rotate(360deg) scale(0.3);
    opacity: 0;
  }
}

@keyframes sparkleShine {
  0%, 100% {
    opacity: 0;
    transform: scale(0) rotate(0deg);
  }
  50% {
    opacity: 1;
    transform: scale(1) rotate(180deg);
  }
}

@keyframes romanticFloat {
  0%, 100% {
    transform: translateY(0px) rotate(0deg) scale(1);
  }
  25% {
    transform: translateY(-20px) rotate(5deg) scale(1.1);
  }
  50% {
    transform: translateY(-10px) rotate(-5deg) scale(0.9);
  }
  75% {
    transform: translateY(-30px) rotate(10deg) scale(1.05);
  }
}
</style>
