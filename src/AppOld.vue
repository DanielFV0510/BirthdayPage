<script setup>
import { ref, onMounted, nextTick } from 'vue'
import { gsap } from 'gsap'

// Importar componentes
import HeaderSection from './components/HeaderSection.vue'
import QualitiesSection from './components/QualitiesSection.vue'
import PhotoGallery from './components/PhotoGallery.vue'
import FloatingEffects from './components/FloatingEffects.vue'

const showSurprise = ref(false)
const magicWandClicked = ref(false)

// Timeline principal de GSAP
let masterTimeline = null

onMounted(() => {
  nextTick(() => {
    initGSAPAnimations()
  })
})

const initGSAPAnimations = () => {
  // Timeline maestro con GSAP
  masterTimeline = gsap.timeline()

  // Animación del título con efectos increíbles
  masterTimeline
    .from('.princess-decoration', {
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

  // Animaciones continuas para elementos románticos
  gsap.to('.romantic-float', {
    duration: 3,
    y: -20,
    rotation: 10,
    repeat: -1,
    yoyo: true,
    ease: "power2.inOut",
    stagger: 0.5
  })

  // Efectos especiales para elementos elegantes
  gsap.to('.elegant-bow-left, .elegant-bow-right', {
    duration: 2,
    rotation: 15,
    scale: 1.1,
    repeat: -1,
    yoyo: true,
    ease: "power2.inOut",
    stagger: 0.5
  })
}

const magicWandClick = () => {
  magicWandClicked.value = !magicWandClicked.value
  
  // Crear explosión de partículas mágicas
  for (let i = 0; i < 20; i++) {
    const particle = document.createElement('div')
    particle.style.cssText = `
      position: fixed;
      width: 10px;
      height: 10px;
      background: linear-gradient(45deg, #ff69b4, #ffd700);
      border-radius: 50%;
      pointer-events: none;
      z-index: 1000;
    `
    document.body.appendChild(particle)
    
    gsap.set(particle, {
      x: window.innerWidth / 2,
      y: window.innerHeight / 2
    })
    
    gsap.to(particle, {
      duration: 2,
      x: Math.random() * window.innerWidth,
      y: Math.random() * window.innerHeight,
      scale: 0,
      rotation: 360,
      ease: "power2.out",
      onComplete: () => particle.remove()
    })
  }
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

    <!-- Elementos románticos flotantes -->
    <div class="romantic-container">
      <div 
        v-for="kitty in hellokitties" 
        :key="kitty.id"
        class="romantic-float"
        :style="{
          left: kitty.left + '%',
          top: kitty.top + '%',
          animationDelay: kitty.animationDelay + 's',
          fontSize: kitty.size + 'px'
        }"
      >
        <span>{{ kitty.kitty }}</span>
      </div>
    </div>

    <!-- Decoración Hello Kitty en las esquinas -->
    <!-- Encabezado principal elegante -->
    <header class="main-header">
      <div class="romantic-banner">
        <div class="elegant-train">
          <span class="elegant-emoji">💖</span>
          <span class="train-heart">💖</span>
          <span class="elegant-emoji">💕</span>
          <span class="train-heart">💖</span>
          <span class="elegant-emoji">👑</span>
        </div>
      </div>

      <div class="princess-decoration">
        <div class="elegant-bow-left">💎</div>
        <h1 class="birthday-title">
          <span class="word-1">¡Feliz</span>
          <span class="word-2">Cumpleaños</span>
          <span class="word-3 highlight">Mi Princesa</span>!
        </h1>
        <div class="elegant-bow-right">💎</div>
      </div>
      
      <div class="birthday-cake-container">
        <div class="cake-decoration">
          <span class="elegant-decoration">💎</span>
          <div class="birthday-cake">🎂</div>
          <span class="elegant-decoration">💎</span>
        </div>
        <div class="candles">🕯️💎🕯️💎🕯️</div>
        <div class="party-decorations">
          <span class="party-emoji">👑</span>
          🎉🎉
          <span class="party-emoji">👑</span>
        </div>
      </div>

      <!-- Botón de música elegante -->
      <button 
        class="music-button" 
        @click="playBirthdayMusic"
        :class="{ 'playing': isPlayingMusic }"
      >
        {{ isPlayingMusic ? '��🔇 Pausar música' : '💖🎵 Música romántica' }}
      </button>
    </header>

    <!-- Sección principal mejorada -->
    <main class="content-section">
      <div class="message-card">
        <div class="card-header">
          <h2 class="magical-title">
            <span class="magic-wand" @click="magicWandClick">🪄</span>
            Para mi Reina del corazón
            <span class="magic-wand" @click="magicWandClick">🪄</span>
          </h2>
          <div class="crown-decoration">
            👑💖👑
          </div>
        </div>
        
        <div class="message-content">
          <div class="love-message-container">
            <div class="elegant-border-decoration">
              <span class="border-element">💎</span>
              <span class="border-element">💖</span>
              <span class="border-element">💎</span>
              <span class="border-element">💕</span>
              <span class="border-element">💎</span>
            </div>
            <p class="love-message">
              Mi querida princesa 💖💕, en este día tan especial quiero decirte que eres 
              la mujer más hermosa del mundo, tan elegante como una reina 👑, 
              y tan especial que iluminas cada día de mi vida ✨
              Tu sonrisa es más brillante que todos los diamantes del mundo! 🌟
            </p>
            <div class="floating-emoji">💖</div>
            <div class="kitty-hearts">
              <span>🐱💕</span>
              <span>🎀💖</span>
              <span>🐱💕</span>
            </div>
          </div>
          
          <div class="qualities-section">
            <h3 class="qualities-title">
              <span class="crown">👑</span>
              Eres mi chica perfecta porque...
              <span class="crown">👑</span>
            </h3>
            <div class="elegant-separator">
              💎💖💎💕💎💖💎💕💎
            </div>
            <div class="qualities-grid">
              <div class="quality-item" @mouseenter="hoverQuality" @mouseleave="leaveQuality">
                <span class="emoji">💖💕</span>
                <span>Tienes la dulzura más hermosa</span>
                <div class="quality-shine"></div>
                <div class="elegant-mini">💎</div>
              </div>
              <div class="quality-item" @mouseenter="hoverQuality" @mouseleave="leaveQuality">
                <span class="emoji">✨⭐</span>
                <span>Brillas con una luz única</span>
                <div class="quality-shine"></div>
                <div class="elegant-mini">💕</div>
              </div>
              <div class="quality-item" @mouseenter="hoverQuality" @mouseleave="leaveQuality">
                <span class="emoji">🌹💎</span>
                <span>Eres elegante como una rosa</span>
                <div class="quality-shine"></div>
                <div class="elegant-mini">💎</div>
              </div>
              <div class="quality-item" @mouseenter="hoverQuality" @mouseleave="leaveQuality">
                <span class="emoji">👑💖</span>
                <span>Eres única como una verdadera reina</span>
                <div class="quality-shine"></div>
                <div class="elegant-mini">💕</div>
              </div>
              <div class="quality-item" @mouseenter="hoverQuality" @mouseleave="leaveQuality">
                <span class="emoji">🌟💕</span>
                <span>Haces que todo sea más hermoso</span>
                <div class="quality-shine"></div>
                <div class="elegant-mini">💎</div>
              </div>
              <div class="quality-item" @mouseenter="hoverQuality" @mouseleave="leaveQuality">
                <span class="emoji">👑💎</span>
                <span>Eres la reina de mi corazón</span>
                <div class="quality-shine"></div>
                <div class="elegant-mini">💖</div>
              </div>
            </div>
          </div>

          <!-- Galería de fotos elegante -->
          <div class="photo-gallery">
            <h3 class="gallery-title">
              📸💎 Nuestros momentos especiales 💎📸
            </h3>
            <div class="elegant-photo-decoration">
              💎📷💖📷💎📷💕📷💎
            </div>
            
            <div class="photo-carousel">
              <button class="carousel-btn prev" @click="prevPhoto">
                <span class="btn-elegant">💖</span>❮
              </button>
              
              <div class="photo-container">
                <div class="photo-frame main-photo">
                  <div class="elegant-photo-border">
                    <span class="corner-gem top-left">💎</span>
                    <span class="corner-gem top-right">💎</span>
                    <span class="corner-gem bottom-left">💎</span>
                    <span class="corner-gem bottom-right">💎</span>
                  </div>
                  <div class="photo-placeholder">
                    <!-- Foto real -->
                    <div class="real-photo-container">
                      <img 
                        :src="photos[currentPhotoIndex].src" 
                        :alt="photos[currentPhotoIndex].title"
                        class="real-photo"
                        @load="onPhotoLoad"
                        @error="onPhotoError"
                      />
                      <div class="photo-overlay">
                        <h4 class="photo-title">{{ photos[currentPhotoIndex].title }}</h4>
                        <p class="photo-description">{{ photos[currentPhotoIndex].description }}</p>
                      </div>
                    </div>
                    <div class="photo-effects">
                      <div class="heart-effect">💖</div>
                      <div class="elegant-effect">💕</div>
                    </div>
                  </div>
                </div>
              </div>
              
              <button class="carousel-btn next" @click="nextPhoto">
                ❯<span class="btn-elegant">💕</span>
              </button>
            </div>

            <!-- Contador de fotos -->
            <div class="photo-counter">
              <span class="current-photo">{{ currentPhotoIndex + 1 }}</span>
              <span class="separator"> / </span>
              <span class="total-photos">{{ photos.length }}</span>
            </div>

            <!-- Thumbnails -->
            <div class="photo-thumbnails">
              <div 
                v-for="(photo, index) in photos" 
                :key="index"
                class="thumbnail"
                :class="{ 'active': currentPhotoIndex === index }"
                @click="goToPhoto(index)"
              >
                <img 
                  :src="photo.src" 
                  :alt="photo.title"
                  class="thumbnail-image"
                />
                <div class="thumbnail-overlay">
                  <span class="thumbnail-number">{{ index + 1 }}</span>
                </div>
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
                <div class="elegant-centerpiece">
                  <div class="princess-crown">👑</div>
                  <div class="love-gems">💎💖💎</div>
                  <div class="elegant-roses">🌹💕🌹</div>
                </div>
                <div class="kitty-accessories">
                  <span>🎀</span>
                  <span>👑</span>
                  <span>💖</span>
                  <span>🌸</span>
                  <span>🎀</span>
                </div>
              </div>
              <p class="final-text">
                Que este nuevo año de vida esté lleno de momentos hermosos mi princesa:
              </p>
              <div class="wishes-container">
                <div class="wish-item">🌟💎 Alegría infinita y brillante</div>
                <div class="wish-item">💫👑 Sueños de realeza cumplidos</div>
                <div class="wish-item">💖💕 Aventuras llenas de amor</div>
                <div class="wish-item">🌸💎 Momentos perfectos y tiernos</div>
                <div class="wish-item">💕💖 Amor eterno y verdadero</div>
              </div>
              <div class="signature">
                <div class="signature-text">Con todo mi amor infinito 💖💕💎</div>
                <div class="signature-heart">💝</div>
                <div class="romantic-signature">
                  De tu novio que te ama más que a nada en el mundo mi reina 👑💕
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </main>

    <!-- Footer con celebración elegante -->
    <footer class="birthday-footer">
      <div class="elegant-party-mega">
        <div class="party-line">
          <span class="party-elegant">💖🎉</span>
          <span class="party-elegant">💎🎂</span>
          <span class="party-elegant">💕💕</span>
          <span class="party-elegant">🎈👑</span>
          <span class="party-elegant">🎁💎</span>
          <span class="party-elegant">💖🎉</span>
        </div>
        <div class="elegant-celebration">
          <div class="dancing-princess">💖💃</div>
          <div class="party-elements">💎 🎂 🌸 💕 🎈 🎁 💎</div>
          <div class="dancing-princess">💃💕</div>
        </div>
      </div>
      <div class="birthday-wish">
        ¡Feliz cumpleaños a mi princesa hermosa! 👑💖💎
      </div>
      <div class="final-romantic-message">
        Que siempre seas tan radiante como eres mi chica 💖✨
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

.kitty-svg {
  border-radius: 50%;
  transition: all 0.3s ease;
  filter: drop-shadow(0 5px 10px rgba(255, 105, 135, 0.5));
  background: white;
  border: 2px solid #ff69b4;
  padding: 2px;
}

.kitty-svg:hover {
  transform: scale(1.3) rotate(15deg);
  filter: drop-shadow(0 10px 25px rgba(255, 105, 135, 0.8));
  border-color: #ff1493;
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

.kitty-corner-svg {
  width: 80px;
  height: 80px;
  filter: drop-shadow(0 5px 15px rgba(255, 105, 135, 0.6));
  transition: all 0.3s ease;
  background: white;
  border-radius: 50%;
  border: 2px solid #ff69b4;
  padding: 3px;
}

.kitty-corner-svg:hover {
  transform: scale(1.3) rotate(20deg);
  filter: drop-shadow(0 8px 25px rgba(255, 105, 135, 0.7));
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

/* Estilos principales de estructura */
.main-header {
  text-align: center;
  padding: 2rem 1rem;
  position: relative;
  z-index: 10;
}

.romantic-banner {
  margin-bottom: 1.5rem;
}

.elegant-train {
  display: flex;
  justify-content: center;
  gap: 1rem;
  font-size: 1.5rem;
  margin-bottom: 1rem;
}

.elegant-emoji, .train-heart {
  animation: trainMove 3s infinite ease-in-out;
}

.train-heart {
  animation-delay: 0.5s;
}

@keyframes trainMove {
  0%, 100% { transform: translateX(0) scale(1); }
  50% { transform: translateX(10px) scale(1.1); }
}

.princess-decoration {
  position: relative;
  margin: 2rem 0;
}

.elegant-bow-left, .elegant-bow-right {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  font-size: 2rem;
  animation: bowFloat 3s infinite ease-in-out;
}

.elegant-bow-left {
  left: -3rem;
}

.elegant-bow-right {
  right: -3rem;
  animation-delay: 1s;
}

@keyframes bowFloat {
  0%, 100% { transform: translateY(-50%) rotate(0deg); }
  50% { transform: translateY(-70%) rotate(10deg); }
}

.birthday-title {
  font-size: 3rem;
  color: #d63384;
  text-shadow: 3px 3px 6px rgba(0,0,0,0.3);
  margin: 1rem 0;
  font-family: 'Comic Sans MS', cursive;
}

.word-1, .word-2, .word-3 {
  display: inline-block;
  margin: 0 0.5rem;
}

.word-3.highlight {
  color: #ff1493;
  text-shadow: 3px 3px 6px rgba(255, 20, 147, 0.5);
}

.birthday-cake-container {
  margin: 2rem 0;
}

.cake-decoration {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 1rem;
  margin-bottom: 1rem;
}

.elegant-decoration {
  font-size: 1.5rem;
  animation: decorationSparkle 2s infinite ease-in-out;
}

.birthday-cake {
  font-size: 3rem;
  animation: cakeBounce 3s infinite ease-in-out;
}

@keyframes decorationSparkle {
  0%, 100% { transform: scale(1) rotate(0deg); }
  50% { transform: scale(1.2) rotate(180deg); }
}

@keyframes cakeBounce {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-10px); }
}

.candles {
  font-size: 1.5rem;
  margin: 0.5rem 0;
}

.party-decorations {
  font-size: 1.3rem;
  margin-top: 1rem;
}

.party-emoji {
  margin: 0 0.5rem;
  animation: partyFloat 2s infinite ease-in-out;
}

@keyframes partyFloat {
  0%, 100% { transform: translateY(0) scale(1); }
  50% { transform: translateY(-8px) scale(1.1); }
}

.music-button {
  background: linear-gradient(135deg, #ff69b4, #ff1493);
  color: white;
  border: none;
  padding: 1rem 2rem;
  font-size: 1.1rem;
  border-radius: 25px;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 5px 15px rgba(255, 105, 135, 0.4);
  margin-top: 1.5rem;
}

.music-button:hover {
  transform: translateY(-3px);
  box-shadow: 0 8px 25px rgba(255, 105, 135, 0.6);
}

.music-button.playing {
  background: linear-gradient(135deg, #28a745, #20c997);
  animation: musicPulse 1s infinite ease-in-out;
}

@keyframes musicPulse {
  0%, 100% { transform: scale(1); }
  50% { transform: scale(1.05); }
}

.content-section {
  padding: 2rem 1rem;
  max-width: 1200px;
  margin: 0 auto;
  position: relative;
  z-index: 10;
}

.message-card {
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.95), rgba(252, 228, 236, 0.95));
  border: 3px solid #ff69b4;
  border-radius: 25px;
  padding: 2.5rem;
  margin: 2rem auto;
  box-shadow: 0 15px 35px rgba(255, 105, 135, 0.3);
  backdrop-filter: blur(10px);
  position: relative;
}

.card-header {
  text-align: center;
  margin-bottom: 2rem;
}

.magical-title {
  font-size: 2.2rem;
  color: #d63384;
  margin-bottom: 1rem;
  text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
}

.magic-wand {
  cursor: pointer;
  margin: 0 0.5rem;
  transition: all 0.3s ease;
}

.magic-wand:hover {
  transform: scale(1.3) rotate(15deg);
}

.crown-decoration {
  font-size: 1.5rem;
  margin-top: 1rem;
}

/* Estilos para la sección de mensaje y cualidades */
.message-content {
  text-align: center;
}

.love-message-container {
  margin: 2rem 0;
  position: relative;
}

.elegant-border-decoration {
  display: flex;
  justify-content: center;
  gap: 1rem;
  margin-bottom: 1.5rem;
  font-size: 1.3rem;
}

.border-element {
  animation: borderFloat 3s infinite ease-in-out;
}

.border-element:nth-child(2) { animation-delay: 0.3s; }
.border-element:nth-child(3) { animation-delay: 0.6s; }
.border-element:nth-child(4) { animation-delay: 0.9s; }
.border-element:nth-child(5) { animation-delay: 1.2s; }

@keyframes borderFloat {
  0%, 100% { transform: translateY(0) scale(1); }
  50% { transform: translateY(-10px) scale(1.1); }
}

.love-message {
  font-size: 1.2rem;
  line-height: 1.6;
  color: #d63384;
  margin: 1.5rem 0;
  padding: 1.5rem;
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.8), rgba(252, 228, 236, 0.8));
  border-radius: 15px;
  border: 2px solid rgba(255, 105, 135, 0.3);
  backdrop-filter: blur(5px);
}

.floating-emoji {
  position: absolute;
  top: -10px;
  right: 20px;
  font-size: 2rem;
  animation: emojiFloat 3s infinite ease-in-out;
}

@keyframes emojiFloat {
  0%, 100% { transform: translateY(0) rotate(0deg); }
  50% { transform: translateY(-15px) rotate(10deg); }
}

.kitty-hearts {
  display: flex;
  justify-content: center;
  gap: 2rem;
  margin-top: 1rem;
  font-size: 1.5rem;
}

.kitty-hearts span {
  animation: heartDance 2s infinite ease-in-out;
}

.kitty-hearts span:nth-child(2) { animation-delay: 0.5s; }
.kitty-hearts span:nth-child(3) { animation-delay: 1s; }

@keyframes heartDance {
  0%, 100% { transform: scale(1) rotate(0deg); }
  50% { transform: scale(1.2) rotate(15deg); }
}

.qualities-section {
  margin: 3rem 0;
}

.qualities-title {
  font-size: 1.8rem;
  color: #d63384;
  text-align: center;
  margin-bottom: 1rem;
  text-shadow: 2px 2px 4px rgba(0,0,0,0.1);
}

.crown {
  margin: 0 1rem;
  animation: crownShine 3s infinite ease-in-out;
}

@keyframes crownShine {
  0%, 100% { transform: scale(1); filter: brightness(1); }
  50% { transform: scale(1.1); filter: brightness(1.3); }
}

.elegant-separator {
  text-align: center;
  font-size: 1.2rem;
  margin: 1.5rem 0;
}

.qualities-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 1.5rem;
  margin-top: 2rem;
}

.quality-item {
  background: linear-gradient(135deg, #ffeaa7, #fab1a0);
  padding: 1.5rem;
  border-radius: 15px;
  text-align: center;
  transition: all 0.3s ease;
  border: 3px solid #ff69b4;
  position: relative;
  overflow: hidden;
  cursor: pointer;
}

.quality-item::before {
  content: '';
  position: absolute;
  top: -50%;
  left: -50%;
  width: 200%;
  height: 200%;
  background: linear-gradient(45deg, transparent, rgba(255, 255, 255, 0.1), transparent);
  transform: translateX(-100%) translateY(-100%);
  transition: transform 0.6s ease;
}

.quality-item:hover::before {
  transform: translateX(100%) translateY(100%);
}

.quality-item:hover {
  transform: translateY(-5px) scale(1.02);
  box-shadow: 0 10px 25px rgba(255, 105, 135, 0.4);
}

.quality-item .emoji {
  font-size: 2rem;
  display: block;
  margin-bottom: 0.5rem;
}

.quality-item span:not(.emoji) {
  font-size: 1.1rem;
  color: #d63384;
  font-weight: bold;
}

.quality-shine {
  position: absolute;
  top: 5px;
  right: 5px;
  width: 20px;
  height: 20px;
  background: radial-gradient(circle, rgba(255, 255, 255, 0.8), transparent);
  border-radius: 50%;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.quality-item:hover .quality-shine {
  opacity: 1;
}

.elegant-mini {
  position: absolute;
  bottom: 5px;
  left: 5px;
  font-size: 1rem;
  animation: miniFloat 2s infinite ease-in-out;
}

@keyframes miniFloat {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-5px); }
}

/* ...existing code... */
</style>
