<script setup>
import { ref, onMounted, nextTick } from 'vue'
import { gsap } from 'gsap'

// Importar componentes
import HeaderSection from './components/HeaderSection.vue'
import QualitiesSection from './components/QualitiesSection.vue'
import PhotoGallery from './components/PhotoGallery.vue'
import FloatingEffects from './components/FloatingEffects.vue'

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
    <!-- Efectos flotantes -->
    <FloatingEffects />

    <!-- Header principal -->
    <HeaderSection />

    <!-- Sección principal -->
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
          
          <!-- Sección de cualidades -->
          <QualitiesSection />

          <!-- Galería de fotos -->
          <PhotoGallery />

          <!-- Mensaje final -->
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

/* Estilos para la sección final */
.final-message {
  margin-top: 3rem;
  padding: 2rem 0;
}

.message-box {
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.9), rgba(252, 228, 236, 0.9));
  border: 3px solid #ff69b4;
  border-radius: 25px;
  padding: 2.5rem;
  margin: 2rem auto;
  max-width: 600px;
  position: relative;
  box-shadow: 0 15px 35px rgba(255, 105, 135, 0.3);
  backdrop-filter: blur(10px);
}

.floating-hearts-bg {
  position: absolute;
  top: -10px;
  left: 0;
  right: 0;
  text-align: center;
  font-size: 1.5rem;
  z-index: 2;
}

.floating-hearts-bg span {
  margin: 0 0.5rem;
  animation: heartBounce 2s infinite ease-in-out;
}

.floating-hearts-bg span:nth-child(2) { animation-delay: 0.2s; }
.floating-hearts-bg span:nth-child(3) { animation-delay: 0.4s; }
.floating-hearts-bg span:nth-child(4) { animation-delay: 0.6s; }
.floating-hearts-bg span:nth-child(5) { animation-delay: 0.8s; }

@keyframes heartBounce {
  0%, 100% { transform: translateY(0) scale(1); }
  50% { transform: translateY(-10px) scale(1.1); }
}

.kitty-final-decoration {
  text-align: center;
  margin-bottom: 2rem;
  position: relative;
}

.elegant-centerpiece {
  display: inline-block;
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.9), rgba(252, 228, 236, 0.9));
  border: 4px solid #ff69b4;
  border-radius: 50%;
  width: 140px;
  height: 140px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  box-shadow: 0 10px 25px rgba(255, 105, 135, 0.4);
  transition: all 0.3s ease;
  position: relative;
  overflow: hidden;
}

.elegant-centerpiece::before {
  content: '';
  position: absolute;
  top: -50%;
  left: -50%;
  width: 200%;
  height: 200%;
  background: linear-gradient(45deg, transparent, rgba(255, 105, 135, 0.1), transparent);
  animation: shimmer 3s infinite linear;
}

@keyframes shimmer {
  0% { transform: translateX(-100%) translateY(-100%); }
  100% { transform: translateX(100%) translateY(100%); }
}

.elegant-centerpiece:hover {
  transform: scale(1.1) rotate(5deg);
  box-shadow: 0 15px 35px rgba(255, 105, 135, 0.6);
}

.princess-crown {
  font-size: 2.5rem;
  margin-bottom: 0.2rem;
  animation: crownGlow 2s infinite ease-in-out;
  z-index: 2;
  position: relative;
}

@keyframes crownGlow {
  0%, 100% { transform: scale(1) rotate(0deg); filter: brightness(1); }
  50% { transform: scale(1.1) rotate(5deg); filter: brightness(1.2); }
}

.love-gems {
  font-size: 1.2rem;
  margin: 0.1rem 0;
  z-index: 2;
  position: relative;
}

.elegant-roses {
  font-size: 1rem;
  z-index: 2;
  position: relative;
}

.kitty-accessories {
  margin-top: 1rem;
  font-size: 1.3rem;
}

.kitty-accessories span {
  margin: 0 0.3rem;
  animation: accessoryFloat 3s infinite ease-in-out;
}

.kitty-accessories span:nth-child(2) { animation-delay: 0.5s; }
.kitty-accessories span:nth-child(3) { animation-delay: 1s; }
.kitty-accessories span:nth-child(4) { animation-delay: 1.5s; }
.kitty-accessories span:nth-child(5) { animation-delay: 2s; }

@keyframes accessoryFloat {
  0%, 100% { transform: translateY(0) rotate(0deg); }
  50% { transform: translateY(-8px) rotate(10deg); }
}

.final-text {
  font-size: 1.3rem;
  text-align: center;
  color: #d63384;
  margin-bottom: 1.5rem;
  font-weight: bold;
  text-shadow: 1px 1px 2px rgba(0,0,0,0.1);
}

.wishes-container {
  display: grid;
  gap: 1rem;
  margin: 2rem 0;
}

.wish-item {
  background: linear-gradient(135deg, #ffeaa7, #fab1a0);
  padding: 1rem 1.5rem;
  border-radius: 15px;
  text-align: center;
  font-size: 1.1rem;
  color: #d63384;
  font-weight: bold;
  box-shadow: 0 5px 15px rgba(255, 105, 135, 0.2);
  transition: all 0.3s ease;
  border: 2px solid #ff69b4;
}

.wish-item:hover {
  transform: translateY(-5px) scale(1.02);
  box-shadow: 0 10px 25px rgba(255, 105, 135, 0.4);
  background: linear-gradient(135deg, #ffd89b, #19547b);
}

.signature {
  text-align: center;
  margin-top: 2rem;
  padding-top: 1.5rem;
  border-top: 2px solid #ff69b4;
}

.signature-text {
  font-size: 1.2rem;
  color: #d63384;
  font-weight: bold;
  margin-bottom: 0.5rem;
}

.signature-heart {
  font-size: 2rem;
  margin: 0.5rem 0;
  animation: heartPulse 2s infinite ease-in-out;
}

@keyframes heartPulse {
  0%, 100% { transform: scale(1); }
  50% { transform: scale(1.2); }
}

.romantic-signature {
  font-size: 1rem;
  color: #ff1493;
  font-style: italic;
  margin-top: 0.5rem;
}

/* Estilos para el footer */
.birthday-footer {
  background: linear-gradient(135deg, #ff9a9e, #fecfef);
  padding: 3rem 1rem 2rem;
  text-align: center;
  margin-top: 3rem;
  border-top: 3px solid #ff69b4;
  position: relative;
}

.elegant-party-mega {
  margin-bottom: 2rem;
}

.party-line {
  display: flex;
  justify-content: center;
  gap: 1rem;
  margin-bottom: 1.5rem;
  flex-wrap: wrap;
}

.party-elegant {
  font-size: 1.5rem;
  animation: partyBounce 2s infinite ease-in-out;
}

.party-elegant:nth-child(2) { animation-delay: 0.2s; }
.party-elegant:nth-child(3) { animation-delay: 0.4s; }
.party-elegant:nth-child(4) { animation-delay: 0.6s; }
.party-elegant:nth-child(5) { animation-delay: 0.8s; }
.party-elegant:nth-child(6) { animation-delay: 1s; }

@keyframes partyBounce {
  0%, 100% { transform: translateY(0) scale(1); }
  50% { transform: translateY(-15px) scale(1.1); }
}

.elegant-celebration {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 2rem;
  margin-bottom: 2rem;
  flex-wrap: wrap;
}

.dancing-princess {
  font-size: 2rem;
  animation: dance 3s infinite ease-in-out;
}

.dancing-princess:nth-child(3) {
  animation-delay: 1.5s;
}

@keyframes dance {
  0%, 100% { transform: rotate(0deg) scale(1); }
  25% { transform: rotate(10deg) scale(1.1); }
  50% { transform: rotate(-10deg) scale(1); }
  75% { transform: rotate(5deg) scale(1.1); }
}

.party-elements {
  font-size: 1.3rem;
  animation: elementFloat 4s infinite ease-in-out;
}

@keyframes elementFloat {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-10px); }
}

.birthday-wish {
  font-size: 1.6rem;
  color: #d63384;
  font-weight: bold;
  margin-bottom: 1rem;
  text-shadow: 2px 2px 4px rgba(0,0,0,0.1);
  animation: wishGlow 3s infinite ease-in-out;
}

@keyframes wishGlow {
  0%, 100% { text-shadow: 2px 2px 4px rgba(0,0,0,0.1); }
  50% { text-shadow: 2px 2px 8px rgba(255, 105, 135, 0.5); }
}

.final-romantic-message {
  font-size: 1.2rem;
  color: #ff1493;
  font-style: italic;
  margin-top: 1rem;
  padding: 1rem;
  background: rgba(255, 255, 255, 0.3);
  border-radius: 15px;
  backdrop-filter: blur(5px);
  border: 2px solid rgba(255, 105, 135, 0.3);
}
</style>
