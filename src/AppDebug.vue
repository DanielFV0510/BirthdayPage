<template>
  <div id="app">
    <!-- Fondo rosa con degradado -->
    <div class="background-container">
      <div class="gradient-bg"></div>
    </div>

    <!-- HELLO KITTY MUY VISIBLE PARA PRUEBA -->
    <div class="debug-kitty-section">
      <h1 style="color: white; text-align: center; font-size: 3rem; text-shadow: 2px 2px 4px rgba(0,0,0,0.5); margin: 2rem 0;">
        🐱 HELLO KITTY TEST 🐱
      </h1>
      
      <div style="display: flex; justify-content: center; gap: 2rem; flex-wrap: wrap; margin: 2rem;">
        <div style="text-align: center; background: rgba(255,255,255,0.9); padding: 1rem; border-radius: 15px;">
          <h3 style="color: #ff1493; margin-bottom: 1rem;">SVG 1</h3>
          <img src="/images/hello-kitty-1.png" alt="Hello Kitty 1" 
               style="width: 100px; height: 100px; border: 3px solid #ff69b4; border-radius: 50%; background: white;" />
        </div>
        
        <div style="text-align: center; background: rgba(255,255,255,0.9); padding: 1rem; border-radius: 15px;">
          <h3 style="color: #ff1493; margin-bottom: 1rem;">SVG 2</h3>
          <img src="/images/hello-kitty-2.jpg" alt="Hello Kitty 2" 
               style="width: 100px; height: 100px; border: 3px solid #ff69b4; border-radius: 50%; background: white;" />
        </div>
        
        <div style="text-align: center; background: rgba(255,255,255,0.9); padding: 1rem; border-radius: 15px;">
          <h3 style="color: #ff1493; margin-bottom: 1rem;">Birthday</h3>
          <img src="/images/hello-kitty-birthday.png" alt="Hello Kitty Birthday" 
               style="width: 100px; height: 100px; border: 3px solid #ff69b4; border-radius: 50%; background: white;" />
        </div>
        
        <div style="text-align: center; background: rgba(255,255,255,0.9); padding: 1rem; border-radius: 15px;">
          <h3 style="color: #ff1493; margin-bottom: 1rem;">Small</h3>
          <img src="/images/hello-kitty-small.png" alt="Hello Kitty Small" 
               style="width: 100px; height: 100px; border: 3px solid #ff69b4; border-radius: 50%; background: white;" />
        </div>
      </div>
      
      <div style="text-align: center; margin: 2rem;">
        <button @click="toggleOriginalApp" 
                style="background: #ff1493; color: white; padding: 15px 30px; border: none; border-radius: 25px; font-size: 1.2rem; cursor: pointer;">
          {{ showOriginal ? '🐱 Mostrar solo test' : '🎉 Mostrar app completa' }}
        </button>
      </div>
    </div>

    <!-- APP ORIGINAL (OCULTA POR DEFECTO PARA DEBUGGEAR) -->
    <div v-if="showOriginal" class="original-app">
      <!-- Corazones flotantes -->
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

      <!-- Hello Kitties flotantes -->
      <div class="hellokitty-container">
        <div 
          v-for="kitty in hellokitties" 
          :key="kitty.id"
          class="hello-kitty-float"
          :style="{
            left: kitty.left + '%',
            top: kitty.top + '%',
            animationDelay: kitty.animationDelay + 's',
            fontSize: kitty.size + 'px'
          }"
        >
          <img 
            v-if="kitty.type === 'svg'" 
            :src="kitty.svgSrc" 
            :alt="'Hello Kitty ' + kitty.id"
            class="kitty-svg"
            :style="{ width: kitty.size + 'px', height: kitty.size + 'px' }"
          />
          <span v-else>{{ kitty.kitty }}</span>
        </div>
      </div>

      <!-- Resto del contenido original... -->
      <header class="main-header">
        <div class="hello-kitty-decoration">
          <h1 class="birthday-title">
            <span class="word-1">¡Feliz</span>
            <span class="word-2">Cumpleaños</span>
            <span class="word-3 highlight">Mi Princesa Hello Kitty</span>!
          </h1>
        </div>
        
        <div class="birthday-cake-container">
          <div class="cake-decoration">
            <img src="/images/hello-kitty-small.png" alt="Hello Kitty" class="mini-kitty-svg" />
            <div class="birthday-cake">🎂</div>
            <img src="/images/hello-kitty-small.png" alt="Hello Kitty" class="mini-kitty-svg" />
          </div>
        </div>
      </header>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const showOriginal = ref(false)
const hearts = ref([])
const sparkles = ref([])
const hellokitties = ref([])

const toggleOriginalApp = () => {
  showOriginal.value = !showOriginal.value
}

onMounted(() => {
  // Crear corazones flotantes
  for (let i = 0; i < 15; i++) {
    hearts.value.push({
      id: i,
      left: Math.random() * 100,
      animationDelay: Math.random() * 4,
      size: Math.random() * 30 + 15,
      color: ['💖', '💕', '💗', '💝', '🌸', '🎀', '💐'][Math.floor(Math.random() * 7)]
    })
  }
  
  // Crear destellos mágicos
  for (let i = 0; i < 10; i++) {
    sparkles.value.push({
      id: i,
      left: Math.random() * 100,
      top: Math.random() * 100,
      animationDelay: Math.random() * 3,
      size: Math.random() * 20 + 10
    })
  }

  // Crear Hello Kitties flotantes
  for (let i = 0; i < 6; i++) {
    hellokitties.value.push({
      id: i,
      left: Math.random() * 100,
      top: Math.random() * 100,
      animationDelay: Math.random() * 5,
      size: Math.random() * 40 + 30, // Más grandes para debug
      type: Math.random() > 0.3 ? 'svg' : 'emoji', // Más SVGs que emojis
      kitty: ['🐱', '🐈', '😸', '😻', '🥰'][Math.floor(Math.random() * 5)],
      svgSrc: [
        '/images/hello-kitty-1.png',
        '/images/hello-kitty-2.jpg', 
        '/images/hello-kitty-birthday.png',
        '/images/hello-kitty-small.png'
      ][Math.floor(Math.random() * 4)]
    })
  }
})
</script>

<style scoped>
#app {
  position: relative;
  min-height: 100vh;
  overflow-x: hidden;
  font-family: 'Comic Sans MS', cursive;
}

.background-container {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: -1;
}

.gradient-bg {
  width: 100%;
  height: 100%;
  background: linear-gradient(135deg, #ff69b4, #ffc0cb, #ff1493, #ffb6c1);
  background-size: 400% 400%;
  animation: gradientShift 8s ease infinite;
}

@keyframes gradientShift {
  0% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}

.debug-kitty-section {
  position: relative;
  z-index: 1000;
  padding: 2rem;
  background: rgba(0,0,0,0.1);
  backdrop-filter: blur(5px);
}

.original-app {
  position: relative;
  z-index: 10;
}

/* Corazones flotantes */
.hearts-container {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: 1;
}

.floating-heart {
  position: absolute;
  animation: float 6s infinite ease-in-out;
  opacity: 0.8;
}

@keyframes float {
  0%, 100% {
    transform: translateY(100vh) rotate(0deg);
    opacity: 0;
  }
  10%, 90% {
    opacity: 1;
  }
  50% {
    transform: translateY(-20px) rotate(180deg);
    opacity: 1;
  }
}

/* Destellos */
.sparkles-container {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: 1;
}

.sparkle {
  position: absolute;
  animation: sparkle 4s infinite ease-in-out;
  opacity: 0.7;
}

@keyframes sparkle {
  0%, 100% {
    transform: scale(0) rotate(0deg);
    opacity: 0;
  }
  50% {
    transform: scale(1) rotate(180deg);
    opacity: 1;
  }
}

/* Hello Kitties flotantes */
.hellokitty-container {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: 100; /* Z-index más alto para debug */
}

.hello-kitty-float {
  position: absolute;
  animation: kittyFloat 8s infinite ease-in-out;
  cursor: pointer;
  pointer-events: auto;
  background: rgba(255,255,255,0.2); /* Fondo temporal para debug */
  border-radius: 50%;
  padding: 5px;
  border: 2px solid rgba(255,105,135,0.5); /* Borde temporal para debug */
}

.kitty-svg {
  border-radius: 50%;
  transition: all 0.3s ease;
  filter: drop-shadow(0 5px 10px rgba(255, 105, 135, 0.5));
  background: white; /* Fondo blanco para contraste */
  border: 2px solid #ff69b4; /* Borde para visibilidad */
}

.kitty-svg:hover {
  transform: scale(1.3) rotate(15deg);
  filter: drop-shadow(0 8px 20px rgba(255, 105, 135, 0.8));
}

@keyframes kittyFloat {
  0%, 100% {
    transform: translateY(0px) rotate(0deg);
  }
  25% {
    transform: translateY(-30px) rotate(5deg);
  }
  50% {
    transform: translateY(-15px) rotate(-10deg);
  }
  75% {
    transform: translateY(-25px) rotate(3deg);
  }
}

/* Header styles */
.main-header {
  text-align: center;
  padding: 2rem;
  position: relative;
  z-index: 50;
  background: rgba(255,255,255,0.1);
  backdrop-filter: blur(10px);
  border-radius: 20px;
  margin: 2rem;
}

.birthday-title {
  font-size: 3rem;
  color: white;
  text-shadow: 3px 3px 6px rgba(0,0,0,0.3);
  margin: 1rem 0;
}

.word-1, .word-2, .word-3 {
  display: inline-block;
  margin: 0 0.5rem;
}

.highlight {
  color: #ff1493;
  text-shadow: 2px 2px 4px rgba(255,20,147,0.5);
}

.birthday-cake-container {
  margin: 2rem 0;
}

.cake-decoration {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 1rem;
  margin: 1rem 0;
}

.mini-kitty-svg {
  width: 40px;
  height: 40px;
  filter: drop-shadow(0 3px 6px rgba(255, 105, 135, 0.4));
  background: white;
  border-radius: 50%;
  border: 2px solid #ff69b4;
  padding: 2px;
}

.birthday-cake {
  font-size: 3rem;
  animation: bounce 2s infinite;
}

@keyframes bounce {
  0%, 20%, 50%, 80%, 100% {
    transform: translateY(0);
  }
  40% {
    transform: translateY(-30px);
  }
  60% {
    transform: translateY(-15px);
  }
}
</style>
