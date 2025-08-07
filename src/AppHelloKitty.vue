<script setup>
import { ref, onMounted, nextTick } from 'vue'
import { gsap } from 'gsap'

const showSurprise = ref(false)
const hearts = ref([])
const sparkles = ref([])
const hellokitties = ref([])
const currentPhotoIndex = ref(0)
const isPlayingMusic = ref(false)
const magicWandClicked = ref(false)

// Animaciones de entrada por fases
const phases = ref({
  title: false,
  message: false,
  qualities: false,
  gallery: false,
  final: false
})

// Timeline principal de GSAP
let masterTimeline = null

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

  // Crear Hello Kitties flotantes
  for (let i = 0; i < 8; i++) {
    hellokitties.value.push({
      id: i,
      left: Math.random() * 100,
      top: Math.random() * 100,
      animationDelay: Math.random() * 5,
      size: Math.random() * 25 + 20,
      kitty: ['🐱', '🐈', '😸', '😻', '🥰'][Math.floor(Math.random() * 5)]
    })
  }
  
  nextTick(() => {
    initGSAPAnimations()
  })
})

const initGSAPAnimations = () => {
  // Timeline maestro con GSAP
  masterTimeline = gsap.timeline()

  // Animación del título con efectos increíbles
  masterTimeline
    .from('.hello-kitty-decoration', {
      duration: 1.5,
      y: -100,
      opacity: 0,
      rotation: -10,
      ease: "bounce.out"
    })
    .from('.word-1', {
      duration: 0.8,
      x: -200,
      opacity: 0,
      rotation: -45,
      ease: "back.out(1.7)"
    }, "-=1")
    .from('.word-2', {
      duration: 0.8,
      x: 200,
      opacity: 0,
      rotation: 45,
      ease: "back.out(1.7)"
    }, "-=0.6")
    .from('.word-3', {
      duration: 1,
      scale: 0,
      opacity: 0,
      rotation: 360,
      ease: "elastic.out(1, 0.5)"
    }, "-=0.4")
    .from('.birthday-cake-container', {
      duration: 1,
      y: 100,
      opacity: 0,
      scale: 0.5,
      rotation: 180,
      ease: "bounce.out"
    }, "-=0.5")
    .from('.music-button', {
      duration: 0.8,
      scale: 0,
      opacity: 0,
      rotation: 720,
      ease: "back.out(2)"
    }, "-=0.3")

  // Animación de la tarjeta principal
  masterTimeline
    .from('.message-card', {
      duration: 1.5,
      y: 200,
      opacity: 0,
      scale: 0.8,
      rotation: 5,
      ease: "power3.out"
    }, "-=0.5")
    .from('.magical-title', {
      duration: 1,
      scale: 0,
      opacity: 0,
      rotation: -10,
      ease: "elastic.out(1, 0.3)"
    }, "-=1")

  // Animación de las cualidades
  gsap.from('.quality-item', {
    duration: 0.8,
    x: -100,
    opacity: 0,
    rotation: -10,
    stagger: 0.2,
    ease: "back.out(1.7)",
    delay: 3
  })

  // Animación de la galería
  gsap.from('.photo-carousel', {
    duration: 1.2,
    scale: 0,
    opacity: 0,
    rotation: 180,
    ease: "elastic.out(1, 0.5)",
    delay: 4
  })

  // Animación del mensaje final
  gsap.from('.message-box', {
    duration: 1.5,
    y: 150,
    opacity: 0,
    scale: 0.7,
    rotation: -5,
    ease: "power4.out",
    delay: 5
  })

  // Animaciones continuas para elementos Hello Kitty
  gsap.to('.hello-kitty-float', {
    duration: 3,
    y: -20,
    rotation: 10,
    repeat: -1,
    yoyo: true,
    ease: "power2.inOut",
    stagger: 0.5
  })

  // Efectos especiales para lazos
  gsap.to('.kitty-bow-left, .kitty-bow-right', {
    duration: 2,
    rotation: 15,
    scale: 1.1,
    repeat: -1,
    yoyo: true,
    ease: "power2.inOut",
    stagger: 0.5
  })
}

const playBirthdayMusic = () => {
  isPlayingMusic.value = !isPlayingMusic.value
  
  if (isPlayingMusic.value) {
    // Animación especial cuando se reproduce música
    gsap.to('.music-button', {
      duration: 0.5,
      scale: 1.2,
      rotation: 360,
      ease: "back.out(1.7)"
    })
    
    // Hacer que todos los elementos bailen
    gsap.to('.floating-heart, .sparkle, .hello-kitty-float', {
      duration: 1,
      scale: 1.3,
      rotation: 360,
      repeat: -1,
      yoyo: true,
      ease: "power2.inOut",
      stagger: 0.1
    })
  } else {
    gsap.killTweensOf('.floating-heart, .sparkle, .hello-kitty-float')
  }
}

const nextPhoto = () => {
  // Animación de transición de fotos
  gsap.to('.photo-placeholder', {
    duration: 0.3,
    rotationY: 90,
    ease: "power2.in",
    onComplete: () => {
      currentPhotoIndex.value = (currentPhotoIndex.value + 1) % 4
      gsap.fromTo('.photo-placeholder', 
        { rotationY: -90 },
        { duration: 0.3, rotationY: 0, ease: "power2.out" }
      )
    }
  })
}

const prevPhoto = () => {
  gsap.to('.photo-placeholder', {
    duration: 0.3,
    rotationY: -90,
    ease: "power2.in",
    onComplete: () => {
      currentPhotoIndex.value = currentPhotoIndex.value === 0 ? 3 : currentPhotoIndex.value - 1
      gsap.fromTo('.photo-placeholder', 
        { rotationY: 90 },
        { duration: 0.3, rotationY: 0, ease: "power2.out" }
      )
    }
  })
}

const magicWandClick = () => {
  magicWandClicked.value = !magicWandClicked.value
  
  // Crear explosión de partículas mágicas
  gsap.to('.magic-wand', {
    duration: 0.3,
    scale: 1.5,
    rotation: 720,
    ease: "power2.out",
    onComplete: () => {
      gsap.to('.magic-wand', {
        duration: 0.3,
        scale: 1,
        rotation: 0
      })
    }
  })

  // Crear efecto de magia en toda la página
  gsap.to('.birthday-container', {
    duration: 0.1,
    filter: 'hue-rotate(360deg)',
    repeat: 5,
    yoyo: true
  })
}

const hoverQuality = (event) => {
  gsap.to(event.currentTarget, {
    duration: 0.3,
    scale: 1.05,
    y: -10,
    rotation: 2,
    ease: "power2.out"
  })
}

const leaveQuality = (event) => {
  gsap.to(event.currentTarget, {
    duration: 0.3,
    scale: 1,
    y: 0,
    rotation: 0,
    ease: "power2.out"
  })
}
</script>

<template>
  <div class="birthday-container">
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
        {{ kitty.kitty }}
      </div>
    </div>

    <!-- Decoración Hello Kitty en las esquinas -->
    <div class="corner-decorations">
      <div class="corner top-left">
        <div class="kitty-corner">🎀</div>
        <div class="bow-decoration">🎀</div>
      </div>
      <div class="corner top-right">
        <div class="kitty-corner">🐱</div>
        <div class="bow-decoration">🎀</div>
      </div>
      <div class="corner bottom-left">
        <div class="kitty-corner">🌸</div>
        <div class="bow-decoration">🎀</div>
      </div>
      <div class="corner bottom-right">
        <div class="kitty-corner">💕</div>
        <div class="bow-decoration">🎀</div>
      </div>
    </div>

    <!-- Encabezado principal con más Hello Kitty -->
    <header class="main-header">
      <div class="hello-kitty-banner">
        <div class="kitty-train">
          <span class="train-kitty">🐱‍👤</span>
          <span class="train-heart">💖</span>
          <span class="train-kitty">🐱‍💻</span>
          <span class="train-heart">💖</span>
          <span class="train-kitty">🐱‍🏍</span>
        </div>
      </div>

      <div class="hello-kitty-decoration">
        <div class="kitty-bow-left">🎀</div>
        <h1 class="birthday-title">
          <span class="word-1">¡Feliz</span>
          <span class="word-2">Cumpleaños</span>
          <span class="word-3 highlight">Mi Princesa Hello Kitty</span>!
        </h1>
        <div class="kitty-bow-right">🎀</div>
      </div>
      
      <div class="birthday-cake-container">
        <div class="cake-decoration">
          <span class="mini-kitty">🐱</span>
          <div class="birthday-cake">🎂</div>
          <span class="mini-kitty">🐱</span>
        </div>
        <div class="candles">🕯️🎀🕯️🎀🕯️</div>
        <div class="kitty-party-hats">🎉🐱🎉🐱🎉</div>
      </div>

      <!-- Botón de música con Hello Kitty -->
      <button 
        class="music-button" 
        @click="playBirthdayMusic"
        :class="{ 'playing': isPlayingMusic }"
      >
        {{ isPlayingMusic ? '🐱🔇 Pausar música kitty' : '🐱🎵 Música Hello Kitty' }}
      </button>
    </header>

    <!-- Sección principal mejorada -->
    <main class="content-section">
      <div class="message-card">
        <div class="card-header">
          <h2 class="magical-title">
            <span class="magic-wand" @click="magicWandClick">🪄</span>
            Para mi Hello Kitty humana favorita
            <span class="magic-wand" @click="magicWandClick">🪄</span>
          </h2>
          <div class="kitty-crown-decoration">
            👑🐱👑
          </div>
        </div>
        
        <div class="message-content">
          <div class="love-message-container">
            <div class="kitty-border-decoration">
              <span class="border-kitty">🎀</span>
              <span class="border-kitty">🐱</span>
              <span class="border-kitty">🎀</span>
              <span class="border-kitty">🐱</span>
              <span class="border-kitty">🎀</span>
            </div>
            <p class="love-message">
              Mi querida Hello Kitty humana 🐱💕, en este día tan especial quiero decirte que eres 
              tan adorable como Hello Kitty, tan dulce como sus lazos rosa 🎀, 
              y tan especial como una edición limitada de Sanrio ✨
              Tu sonrisa es más brillante que todos los accesorios de Hello Kitty juntos! 🌟
            </p>
            <div class="floating-emoji">🦄</div>
            <div class="kitty-hearts">
              <span>🐱💕</span>
              <span>🎀💖</span>
              <span>🐱💕</span>
            </div>
          </div>
          
          <div class="qualities-section">
            <h3 class="qualities-title">
              <span class="crown">👑</span>
              Eres mi Hello Kitty perfecta porque...
              <span class="crown">👑</span>
            </h3>
            <div class="hello-kitty-separator">
              🎀🐱🎀🐱🎀🐱🎀🐱🎀
            </div>
            <div class="qualities-grid">
              <div class="quality-item" @mouseenter="hoverQuality" @mouseleave="leaveQuality">
                <span class="emoji">🐱💕</span>
                <span>Tienes la ternura de Hello Kitty</span>
                <div class="quality-shine"></div>
                <div class="kitty-mini">🎀</div>
              </div>
              <div class="quality-item" @mouseenter="hoverQuality" @mouseleave="leaveQuality">
                <span class="emoji">🎀⭐</span>
                <span>Brillas como los accesorios más kawaii</span>
                <div class="quality-shine"></div>
                <div class="kitty-mini">🐱</div>
              </div>
              <div class="quality-item" @mouseenter="hoverQuality" @mouseleave="leaveQuality">
                <span class="emoji">🌸🐱</span>
                <span>Eres tan dulce como los pasteles de Sanrio</span>
                <div class="quality-shine"></div>
                <div class="kitty-mini">🎀</div>
              </div>
              <div class="quality-item" @mouseenter="hoverQuality" @mouseleave="leaveQuality">
                <span class="emoji">🦄🎀</span>
                <span>Eres única como una Hello Kitty unicornio</span>
                <div class="quality-shine"></div>
                <div class="kitty-mini">🐱</div>
              </div>
              <div class="quality-item" @mouseenter="hoverQuality" @mouseleave="leaveQuality">
                <span class="emoji">🌟🐱</span>
                <span>Haces que todo sea más kawaii</span>
                <div class="quality-shine"></div>
                <div class="kitty-mini">🎀</div>
              </div>
              <div class="quality-item" @mouseenter="hoverQuality" @mouseleave="leaveQuality">
                <span class="emoji">👑🎀</span>
                <span>Eres la reina de mi colección Hello Kitty</span>
                <div class="quality-shine"></div>
                <div class="kitty-mini">🐱</div>
              </div>
            </div>
          </div>

          <!-- Galería de fotos con tema Hello Kitty -->
          <div class="photo-gallery">
            <h3 class="gallery-title">
              📸🐱 Nuestra colección de momentos kawaii 🐱📸
            </h3>
            <div class="kitty-photo-decoration">
              🎀📷🐱📷🎀📷🐱📷🎀
            </div>
            
            <div class="photo-carousel">
              <button class="carousel-btn prev" @click="prevPhoto">
                <span class="btn-kitty">🐱</span>❮
              </button>
              
              <div class="photo-container">
                <div class="photo-frame main-photo">
                  <div class="kitty-photo-border">
                    <span class="corner-bow">🎀</span>
                    <span class="corner-bow">🎀</span>
                    <span class="corner-bow">🎀</span>
                    <span class="corner-bow">🎀</span>
                  </div>
                  <div class="photo-placeholder" :class="`photo-${currentPhotoIndex}`">
                    <div class="placeholder-content">
                      <p v-if="currentPhotoIndex === 0">📷 Nuestra primera foto estilo Hello Kitty 🐱💕</p>
                      <p v-else-if="currentPhotoIndex === 1">🌹 Momento kawaii especial 🐱🌹</p>
                      <p v-else-if="currentPhotoIndex === 2">🎉 Celebrando como Hello Kitty 🐱🎉</p>
                      <p v-else>💑 Nuestro amor más kawaii que Hello Kitty 🐱💑</p>
                      <span class="hello-kitty-camera">📸🐱🎀</span>
                    </div>
                    <div class="photo-effects">
                      <div class="heart-effect">💖</div>
                      <div class="kitty-effect">🐱</div>
                    </div>
                  </div>
                </div>
              </div>
              
              <button class="carousel-btn next" @click="nextPhoto">
                ❯<span class="btn-kitty">🐱</span>
              </button>
            </div>

            <div class="photo-thumbnails">
              <div 
                v-for="i in 4" 
                :key="i"
                class="thumbnail"
                :class="{ 'active': currentPhotoIndex === i-1 }"
                @click="currentPhotoIndex = i-1"
              >
                <span class="thumb-emoji">{{ ['🐱💕', '🐱🌹', '🐱🎉', '🐱💑'][i-1] }}</span>
              </div>
            </div>
          </div>

          <!-- Mensaje final con Hello Kitty -->
          <div class="final-message">
            <div class="message-box">
              <div class="floating-hearts-bg">
                <span>💖</span><span>🐱</span><span>💕</span><span>🎀</span><span>💗</span>
              </div>
              <div class="kitty-final-decoration">
                <div class="big-kitty">🐱</div>
                <div class="kitty-accessories">
                  <span>🎀</span>
                  <span>👑</span>
                  <span>💖</span>
                  <span>🌸</span>
                  <span>🎀</span>
                </div>
              </div>
              <p class="final-text">
                Que este nuevo año de vida esté lleno de momentos tan kawaii como Hello Kitty:
              </p>
              <div class="wishes-container">
                <div class="wish-item">🌟🐱 Alegría kawaii infinita</div>
                <div class="wish-item">💫🎀 Sueños Hello Kitty cumplidos</div>
                <div class="wish-item">🦄🐱 Aventuras súper kawaii</div>
                <div class="wish-item">🌸🎀 Momentos perfectos y tiernos</div>
                <div class="wish-item">💕🐱 Amor eterno estilo Sanrio</div>
              </div>
              <div class="signature">
                <div class="signature-text">Con todo mi amor kawaii 🐱💖🎀</div>
                <div class="signature-heart">💝</div>
                <div class="kitty-signature">
                  De tu novio que te ama más que a toda la colección de Hello Kitty 🐱💕
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </main>

    <!-- Footer con fiesta Hello Kitty -->
    <footer class="birthday-footer">
      <div class="kitty-party-mega">
        <div class="party-line">
          <span class="party-kitty">🐱🎉</span>
          <span class="party-kitty">🎀🎂</span>
          <span class="party-kitty">🐱💕</span>
          <span class="party-kitty">🎈🐱</span>
          <span class="party-kitty">🎁🎀</span>
          <span class="party-kitty">🐱🎉</span>
        </div>
        <div class="kitty-celebration">
          <div class="dancing-kitty">🐱💃</div>
          <div class="party-elements">🎀 🎂 🌸 💕 🎈 🎁 🎀</div>
          <div class="dancing-kitty">💃🐱</div>
        </div>
      </div>
      <div class="birthday-wish">
        ¡Feliz cumpleaños a mi Hello Kitty humana favorita! 🐱💖🎀
      </div>
      <div class="final-kitty-message">
        Que siempre seas tan kawaii como eres 🐱✨
      </div>
    </footer>
  </div>
</template>

<style scoped>
.birthday-container {
  min-height: 100vh;
  background: linear-gradient(135deg, #ff9a9e 0%, #fecfef 30%, #ffeaa7 60%, #fecfef 100%);
  position: relative;
  overflow-x: hidden;
  font-family: 'Comic Sans MS', cursive, sans-serif;
}

/* Animaciones de partículas mejoradas */
.hearts-container, .sparkles-container, .hellokitty-container {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: 1;
}

.floating-heart, .sparkle, .hello-kitty-float {
  position: absolute;
  opacity: 0.8;
}

.floating-heart {
  animation: floatUpHeart 6s infinite ease-in-out;
}

.sparkle {
  animation: sparkleShine 3s infinite ease-in-out;
}

.hello-kitty-float {
  animation: kittyFloat 8s infinite ease-in-out;
  cursor: pointer;
}

/* Decoraciones en las esquinas */
.corner-decorations {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: 1;
}

.corner {
  position: absolute;
  font-size: 2rem;
}

.corner.top-left {
  top: 20px;
  left: 20px;
  animation: bounceCorner 3s infinite ease-in-out;
}

.corner.top-right {
  top: 20px;
  right: 20px;
  animation: bounceCorner 3s infinite ease-in-out 0.5s;
}

.corner.bottom-left {
  bottom: 20px;
  left: 20px;
  animation: bounceCorner 3s infinite ease-in-out 1s;
}

.corner.bottom-right {
  bottom: 20px;
  right: 20px;
  animation: bounceCorner 3s infinite ease-in-out 1.5s;
}

.bow-decoration {
  font-size: 1rem;
  margin-top: 5px;
  animation: spin 4s infinite linear;
}

/* Animaciones GSAP mejoradas */
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
    transform: scale(0.5) rotate(0deg);
    opacity: 0.5;
  }
  50% {
    transform: scale(1.8) rotate(180deg);
    opacity: 1;
  }
}

@keyframes kittyFloat {
  0%, 100% {
    transform: translateY(0) rotate(0deg) scale(1);
  }
  25% {
    transform: translateY(-30px) rotate(-10deg) scale(1.1);
  }
  50% {
    transform: translateY(-50px) rotate(0deg) scale(1.2);
  }
  75% {
    transform: translateY(-30px) rotate(10deg) scale(1.1);
  }
}

@keyframes bounceCorner {
  0%, 100% {
    transform: scale(1) rotate(0deg);
  }
  50% {
    transform: scale(1.2) rotate(15deg);
  }
}

/* Encabezado Hello Kitty mejorado */
.main-header {
  text-align: center;
  padding: 2rem;
  position: relative;
  z-index: 2;
}

.hello-kitty-banner {
  margin-bottom: 1rem;
}

.kitty-train {
  display: flex;
  justify-content: center;
  gap: 0.5rem;
  font-size: 1.5rem;
  animation: trainMove 4s infinite ease-in-out;
}

@keyframes trainMove {
  0%, 100% {
    transform: translateX(0);
  }
  50% {
    transform: translateX(20px);
  }
}

.train-kitty, .train-heart {
  animation: trainBounce 2s infinite ease-in-out;
}

.train-heart {
  animation-delay: 0.5s;
}

@keyframes trainBounce {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-10px);
  }
}

.hello-kitty-decoration {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 2rem;
  margin-bottom: 2rem;
}

.kitty-bow-left, .kitty-bow-right {
  font-size: 4rem;
}

.birthday-title {
  font-size: 3.5rem;
  color: #ffffff;
  text-shadow: 3px 3px 8px rgba(255, 105, 135, 0.8);
  margin: 0;
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.word-1, .word-2, .word-3 {
  display: inline-block;
}

.word-1 {
  color: #ff69b4;
}

.word-2 {
  color: #ff1493;
}

.word-3 {
  color: #ffd700;
  font-size: 3rem;
  text-shadow: 4px 4px 12px rgba(255, 215, 0, 0.8);
}

.birthday-cake-container {
  margin: 2rem 0;
}

.cake-decoration {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1rem;
  margin-bottom: 1rem;
}

.mini-kitty {
  font-size: 2rem;
  animation: miniKittyDance 2s infinite ease-in-out;
}

@keyframes miniKittyDance {
  0%, 100% {
    transform: rotate(-10deg);
  }
  50% {
    transform: rotate(10deg);
  }
}

.birthday-cake {
  font-size: 5rem;
  animation: cakeFloat 3s ease-in-out infinite;
}

.candles {
  font-size: 1.5rem;
  animation: candleFlicker 1s ease-in-out infinite alternate;
  margin-bottom: 0.5rem;
}

.kitty-party-hats {
  font-size: 1.2rem;
  animation: partyHatBounce 2s infinite ease-in-out;
}

@keyframes cakeFloat {
  0%, 100% {
    transform: translateY(0) rotate(-2deg);
  }
  50% {
    transform: translateY(-20px) rotate(2deg);
  }
}

@keyframes candleFlicker {
  0% {
    opacity: 1;
    filter: brightness(1);
  }
  100% {
    opacity: 0.8;
    filter: brightness(1.2);
  }
}

@keyframes partyHatBounce {
  0%, 100% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.1);
  }
}

.music-button {
  background: linear-gradient(135deg, #ff69b4, #ff1493);
  color: white;
  border: none;
  padding: 1rem 2rem;
  border-radius: 30px;
  font-size: 1.1rem;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 5px 15px rgba(255, 105, 135, 0.4);
  margin-top: 1rem;
}

.music-button:hover {
  transform: translateY(-3px) scale(1.05);
  box-shadow: 0 8px 25px rgba(255, 105, 135, 0.6);
}

.music-button.playing {
  animation: musicPulse 1s infinite;
}

@keyframes musicPulse {
  0%, 100% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.1);
  }
}

/* Contenido principal con Hello Kitty */
.content-section {
  padding: 2rem;
  display: flex;
  justify-content: center;
  position: relative;
  z-index: 2;
}

.message-card {
  background: rgba(255, 255, 255, 0.95);
  border-radius: 25px;
  padding: 3rem;
  max-width: 900px;
  width: 100%;
  box-shadow: 0 15px 40px rgba(255, 105, 135, 0.3);
  border: 4px solid #ff69b4;
  position: relative;
  overflow: hidden;
}

.message-card::before {
  content: '';
  position: absolute;
  top: -50%;
  left: -50%;
  width: 200%;
  height: 200%;
  background: linear-gradient(45deg, transparent, rgba(255, 255, 255, 0.1), transparent);
  animation: shimmer 3s infinite;
}

@keyframes shimmer {
  0% {
    transform: translateX(-100%) translateY(-100%) rotate(45deg);
  }
  100% {
    transform: translateX(100%) translateY(100%) rotate(45deg);
  }
}

.magical-title {
  color: #d63384;
  text-align: center;
  font-size: 2.2rem;
  margin-bottom: 1rem;
  text-shadow: 2px 2px 4px rgba(255, 105, 135, 0.5);
  position: relative;
}

.magic-wand {
  display: inline-block;
  cursor: pointer;
  transition: all 0.3s ease;
}

.magic-wand:hover {
  transform: scale(1.2) rotate(15deg);
}

.kitty-crown-decoration {
  font-size: 2rem;
  margin-bottom: 2rem;
  animation: crownSparkle 3s infinite ease-in-out;
}

@keyframes crownSparkle {
  0%, 100% {
    filter: brightness(1);
  }
  50% {
    filter: brightness(1.5);
  }
}

.love-message-container {
  position: relative;
  margin-bottom: 3rem;
}

.kitty-border-decoration {
  display: flex;
  justify-content: space-around;
  margin-bottom: 1rem;
  font-size: 1.5rem;
}

.border-kitty {
  animation: borderKittyBounce 2s infinite ease-in-out;
}

.border-kitty:nth-child(odd) {
  animation-delay: 0.5s;
}

@keyframes borderKittyBounce {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-8px);
  }
}

.love-message {
  font-size: 1.3rem;
  line-height: 1.8;
  color: #495057;
  text-align: center;
  font-style: italic;
  padding: 2rem;
  background: linear-gradient(135deg, #fce4ec, #f8bbd9);
  border-radius: 20px;
  border: 2px solid #ff69b4;
  position: relative;
}

.floating-emoji {
  position: absolute;
  top: -20px;
  right: -10px;
  font-size: 3rem;
  animation: floatEmoji 4s infinite ease-in-out;
}

.kitty-hearts {
  display: flex;
  justify-content: center;
  gap: 1rem;
  margin-top: 1rem;
  font-size: 1.5rem;
}

.kitty-hearts span {
  animation: kittyHeartBeat 2s infinite ease-in-out;
}

.kitty-hearts span:nth-child(2) {
  animation-delay: 0.5s;
}

.kitty-hearts span:nth-child(3) {
  animation-delay: 1s;
}

@keyframes floatEmoji {
  0%, 100% {
    transform: translateY(0) rotate(0deg);
  }
  50% {
    transform: translateY(-20px) rotate(15deg);
  }
}

@keyframes kittyHeartBeat {
  0%, 100% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.2);
  }
}

.qualities-section {
  margin-bottom: 3rem;
}

.qualities-title {
  color: #d63384;
  text-align: center;
  font-size: 1.8rem;
  margin-bottom: 1rem;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1rem;
}

.crown {
  font-size: 2rem;
  animation: crownShine 2s infinite ease-in-out;
}

@keyframes crownShine {
  0%, 100% {
    filter: brightness(1);
    transform: scale(1);
  }
  50% {
    filter: brightness(1.5);
    transform: scale(1.1);
  }
}

.hello-kitty-separator {
  text-align: center;
  font-size: 1.2rem;
  margin-bottom: 2rem;
  animation: separatorDance 4s infinite ease-in-out;
}

@keyframes separatorDance {
  0%, 100% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.05);
  }
}

.qualities-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 1.5rem;
  margin-bottom: 3rem;
}

.quality-item {
  display: flex;
  align-items: center;
  gap: 1rem;
  padding: 1.5rem;
  background: linear-gradient(135deg, #fce4ec, #f8bbd9);
  border-radius: 20px;
  border: 3px solid #ff69b4;
  position: relative;
  overflow: hidden;
  cursor: pointer;
  transition: all 0.3s ease;
}

.quality-item:hover {
  transform: translateY(-5px) scale(1.02);
  box-shadow: 0 10px 25px rgba(255, 105, 135, 0.4);
}

.quality-item .emoji {
  font-size: 2rem;
  animation: emojiDance 2s infinite ease-in-out;
}

.kitty-mini {
  position: absolute;
  top: 5px;
  right: 5px;
  font-size: 1rem;
  animation: miniKittySparkle 3s infinite ease-in-out;
}

@keyframes emojiDance {
  0%, 100% {
    transform: rotate(-5deg) scale(1);
  }
  50% {
    transform: rotate(5deg) scale(1.1);
  }
}

@keyframes miniKittySparkle {
  0%, 100% {
    opacity: 0.7;
    transform: scale(1);
  }
  50% {
    opacity: 1;
    transform: scale(1.3);
  }
}

.quality-shine {
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.4), transparent);
  animation: shine 3s infinite;
}

@keyframes shine {
  0% {
    left: -100%;
  }
  100% {
    left: 100%;
  }
}

/* Galería Hello Kitty */
.photo-gallery {
  margin: 3rem 0;
}

.gallery-title {
  color: #d63384;
  text-align: center;
  font-size: 1.8rem;
  margin-bottom: 1rem;
  animation: titlePulse 2s infinite ease-in-out;
}

.kitty-photo-decoration {
  text-align: center;
  font-size: 1.2rem;
  margin-bottom: 2rem;
  animation: photoDecorationSway 3s infinite ease-in-out;
}

@keyframes titlePulse {
  0%, 100% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.05);
  }
}

@keyframes photoDecorationSway {
  0%, 100% {
    transform: translateX(0);
  }
  50% {
    transform: translateX(10px);
  }
}

.photo-carousel {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 2rem;
  margin-bottom: 2rem;
}

.carousel-btn {
  background: linear-gradient(135deg, #ff69b4, #ff1493);
  color: white;
  border: none;
  width: 60px;
  height: 60px;
  border-radius: 50%;
  font-size: 1.2rem;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 5px 15px rgba(255, 105, 135, 0.4);
  display: flex;
  align-items: center;
  justify-content: center;
}

.carousel-btn:hover {
  transform: scale(1.1);
  box-shadow: 0 8px 25px rgba(255, 105, 135, 0.6);
}

.btn-kitty {
  margin: 0 3px;
  font-size: 0.8rem;
}

.photo-container {
  perspective: 1000px;
}

.photo-frame.main-photo {
  width: 400px;
  height: 300px;
  background: linear-gradient(135deg, #ffffff, #fce4ec);
  border: 5px solid #ff69b4;
  border-radius: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  transition: all 0.5s ease;
  transform-style: preserve-3d;
}

.kitty-photo-border {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
}

.corner-bow {
  position: absolute;
  font-size: 1.5rem;
  animation: cornerBowSpin 4s infinite linear;
}

.corner-bow:nth-child(1) {
  top: -5px;
  left: -5px;
}

.corner-bow:nth-child(2) {
  top: -5px;
  right: -5px;
  animation-delay: 1s;
}

.corner-bow:nth-child(3) {
  bottom: -5px;
  left: -5px;
  animation-delay: 2s;
}

.corner-bow:nth-child(4) {
  bottom: -5px;
  right: -5px;
  animation-delay: 3s;
}

@keyframes cornerBowSpin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

.photo-placeholder {
  text-align: center;
  padding: 2rem;
  position: relative;
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.placeholder-content p {
  font-size: 1.2rem;
  color: #495057;
  margin-bottom: 1rem;
}

.hello-kitty-camera {
  font-size: 3rem;
  animation: cameraFlash 3s infinite;
}

@keyframes cameraFlash {
  0%, 90%, 100% {
    opacity: 1;
  }
  95% {
    opacity: 0.3;
  }
}

.photo-effects {
  position: absolute;
  top: 10px;
  right: 10px;
  display: flex;
  flex-direction: column;
  gap: 5px;
}

.heart-effect, .kitty-effect {
  font-size: 1.5rem;
  animation: effectFloat 2s infinite ease-in-out;
}

.kitty-effect {
  animation-delay: 0.5s;
}

@keyframes effectFloat {
  0%, 100% {
    transform: translateY(0) scale(1);
  }
  50% {
    transform: translateY(-8px) scale(1.1);
  }
}

.photo-thumbnails {
  display: flex;
  justify-content: center;
  gap: 1rem;
}

.thumbnail {
  width: 60px;
  height: 60px;
  background: linear-gradient(135deg, #fce4ec, #f8bbd9);
  border: 3px solid #ff69b4;
  border-radius: 15px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all 0.3s ease;
}

.thumbnail:hover, .thumbnail.active {
  transform: scale(1.1);
  border-color: #ff1493;
  box-shadow: 0 5px 15px rgba(255, 105, 135, 0.4);
}

.thumb-emoji {
  font-size: 1.2rem;
}

/* Mensaje final Hello Kitty */
.final-message {
  margin-top: 3rem;
}

.message-box {
  background: linear-gradient(135deg, #ff69b4, #ff1493);
  color: white;
  padding: 3rem;
  border-radius: 25px;
  text-align: center;
  position: relative;
  overflow: hidden;
}

.floating-hearts-bg {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: space-around;
  align-items: center;
  opacity: 0.2;
  font-size: 3rem;
}

.floating-hearts-bg span {
  animation: bgHeartFloat 4s infinite ease-in-out;
}

.floating-hearts-bg span:nth-child(2) {
  animation-delay: 0.8s;
}

.floating-hearts-bg span:nth-child(3) {
  animation-delay: 1.6s;
}

.floating-hearts-bg span:nth-child(4) {
  animation-delay: 2.4s;
}

.floating-hearts-bg span:nth-child(5) {
  animation-delay: 3.2s;
}

@keyframes bgHeartFloat {
  0%, 100% {
    transform: translateY(0) rotate(0deg);
  }
  50% {
    transform: translateY(-20px) rotate(180deg);
  }
}

.kitty-final-decoration {
  margin-bottom: 2rem;
  z-index: 1;
  position: relative;
}

.big-kitty {
  font-size: 4rem;
  animation: bigKittyPulse 3s infinite ease-in-out;
  margin-bottom: 1rem;
}

@keyframes bigKittyPulse {
  0%, 100% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.2);
  }
}

.kitty-accessories {
  display: flex;
  justify-content: center;
  gap: 1rem;
  font-size: 1.5rem;
}

.kitty-accessories span {
  animation: accessoryTwinkle 2s infinite ease-in-out;
}

.kitty-accessories span:nth-child(odd) {
  animation-delay: 0.5s;
}

@keyframes accessoryTwinkle {
  0%, 100% {
    opacity: 0.8;
    transform: scale(1);
  }
  50% {
    opacity: 1;
    transform: scale(1.3);
  }
}

.final-text {
  font-size: 1.4rem;
  margin-bottom: 2rem;
  z-index: 1;
  position: relative;
}

.wishes-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 1rem;
  margin-bottom: 2rem;
  z-index: 1;
  position: relative;
}

.wish-item {
  background: rgba(255, 255, 255, 0.2);
  padding: 1rem;
  border-radius: 15px;
  font-size: 1.1rem;
  animation: wishGlow 3s infinite ease-in-out;
}

@keyframes wishGlow {
  0%, 100% {
    box-shadow: 0 0 10px rgba(255, 255, 255, 0.3);
  }
  50% {
    box-shadow: 0 0 20px rgba(255, 255, 255, 0.6);
  }
}

.signature {
  z-index: 1;
  position: relative;
}

.signature-text {
  font-size: 1.5rem;
  font-weight: bold;
  margin-bottom: 1rem;
}

.signature-heart {
  font-size: 3rem;
  animation: signatureHeartBeat 1.5s infinite ease-in-out;
  margin-bottom: 1rem;
}

@keyframes signatureHeartBeat {
  0%, 100% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.2);
  }
}

.kitty-signature {
  font-size: 1.1rem;
  font-style: italic;
  opacity: 0.9;
}

/* Footer Hello Kitty mejorado */
.birthday-footer {
  text-align: center;
  padding: 3rem 2rem;
  position: relative;
  z-index: 2;
}

.kitty-party-mega {
  margin-bottom: 2rem;
}

.party-line {
  display: flex;
  justify-content: center;
  gap: 1rem;
  margin-bottom: 2rem;
  font-size: 1.5rem;
}

.party-kitty {
  animation: partyKittyBounce 2s infinite ease-in-out;
}

.party-kitty:nth-child(even) {
  animation-delay: 0.5s;
}

@keyframes partyKittyBounce {
  0%, 100% {
    transform: translateY(0) scale(1);
  }
  50% {
    transform: translateY(-15px) scale(1.1);
  }
}

.kitty-celebration {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 2rem;
}

.dancing-kitty {
  font-size: 3rem;
  animation: kittyDance 2s infinite ease-in-out;
}

.dancing-kitty:nth-child(3) {
  animation-delay: 1s;
}

@keyframes kittyDance {
  0%, 100% {
    transform: translateY(0) rotate(-5deg);
  }
  50% {
    transform: translateY(-15px) rotate(5deg);
  }
}

.party-elements {
  font-size: 2rem;
  animation: partyPulse 3s infinite ease-in-out;
}

@keyframes partyPulse {
  0%, 100% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.1);
  }
}

.birthday-wish {
  font-size: 1.5rem;
  color: #ffffff;
  text-shadow: 2px 2px 4px rgba(255, 105, 135, 0.8);
  font-weight: bold;
  animation: wishShine 4s infinite ease-in-out;
  margin-bottom: 1rem;
}

@keyframes wishShine {
  0%, 100% {
    text-shadow: 2px 2px 4px rgba(255, 105, 135, 0.8);
  }
  50% {
    text-shadow: 2px 2px 20px rgba(255, 215, 0, 1);
  }
}

.final-kitty-message {
  font-size: 1.2rem;
  color: #ffffff;
  text-shadow: 1px 1px 3px rgba(255, 105, 135, 0.6);
  font-style: italic;
  animation: finalMessageGlow 5s infinite ease-in-out;
}

@keyframes finalMessageGlow {
  0%, 100% {
    opacity: 0.8;
  }
  50% {
    opacity: 1;
  }
}

/* Responsive Hello Kitty */
@media (max-width: 768px) {
  .birthday-title {
    font-size: 2.5rem;
  }
  
  .word-3 {
    font-size: 2rem;
  }
  
  .message-card {
    margin: 1rem;
    padding: 2rem;
  }
  
  .qualities-grid {
    grid-template-columns: 1fr;
  }
  
  .photo-frame.main-photo {
    width: 300px;
    height: 225px;
  }
  
  .photo-carousel {
    gap: 1rem;
  }
  
  .wishes-container {
    grid-template-columns: 1fr;
  }
  
  .hello-kitty-decoration {
    flex-direction: column;
    gap: 1rem;
  }
  
  .kitty-celebration {
    flex-direction: column;
    gap: 1rem;
  }

  .party-line {
    flex-wrap: wrap;
    gap: 0.5rem;
  }

  .kitty-train {
    flex-wrap: wrap;
  }
}

@media (max-width: 480px) {
  .birthday-title {
    font-size: 2rem;
  }
  
  .word-3 {
    font-size: 1.8rem;
  }
  
  .photo-frame.main-photo {
    width: 250px;
    height: 180px;
  }
  
  .message-card {
    padding: 1.5rem;
  }

  .carousel-btn {
    width: 50px;
    height: 50px;
    font-size: 1rem;
  }

  .corner {
    font-size: 1.5rem;
  }

  .floating-heart, .sparkle, .hello-kitty-float {
    font-size: 1rem !important;
  }
}

/* Animaciones especiales para interacciones */
.magic-wand:active {
  animation: wandMagicBlast 0.5s ease-out;
}

@keyframes wandMagicBlast {
  0% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.5) rotate(180deg);
  }
  100% {
    transform: scale(1) rotate(360deg);
  }
}

/* Efectos hover especiales */
.hello-kitty-float:hover {
  transform: scale(1.3) rotate(15deg) !important;
  animation-play-state: paused;
}

.corner:hover {
  transform: scale(1.5) rotate(15deg) !important;
}

.border-kitty:hover {
  transform: scale(1.3) !important;
  animation-play-state: paused;
}
</style>
