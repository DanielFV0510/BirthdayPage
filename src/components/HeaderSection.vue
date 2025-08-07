<template>
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
      <h1 class="birthday-title">🙊
        <span class="word-1">¡Feliz</span>
        <span class="word-2">Cumpleaños</span>
        <span class="word-3 highlight">Mi Princesa</span>!🙊
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
      @click="toggleMusic"
      :class="{ 'playing': isPlayingMusic }"
    >
      {{ isPlayingMusic ? '💖🔇 Pausar música' : '💖🎵 Música romántica' }}
    </button>
  </header>
</template>

<script setup>
import { ref } from 'vue'
import { gsap } from 'gsap'

const isPlayingMusic = ref(false)

const toggleMusic = () => {
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
    gsap.to('.floating-heart, .sparkle, .romantic-float', {
      duration: 1,
      scale: 1.3,
      rotation: 360,
      repeat: -1,
      yoyo: true,
      ease: "power2.inOut",
      stagger: 0.1
    })
  } else {
    gsap.killTweensOf('.floating-heart, .sparkle, .romantic-float')
  }
}
</script>

<style scoped>
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
</style>
