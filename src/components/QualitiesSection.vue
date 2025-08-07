<template>
  <div class="qualities-section" ref="qualitiesSection">
    <h3 class="qualities-title">
      <span class="crown">👑</span>
      Eres mi chica perfecta porque...
      <span class="crown">👑</span>
    </h3>
    <div class="elegant-separator">
      💎💖💎💕💎💖💎💕💎
    </div>
    <div class="qualities-grid">
      <div 
        v-for="(quality, index) in qualities" 
        :key="index"
        class="quality-item" 
        @mouseenter="hoverQuality" 
        @mouseleave="leaveQuality"
      >
        <span class="emoji">{{ quality.emoji }}</span>
        <span>{{ quality.text }}</span>
        <div class="quality-shine"></div>
        <div class="elegant-mini">{{ quality.mini }}</div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, nextTick } from 'vue'
import { gsap } from 'gsap'

const qualities = ref([
  {
    emoji: '💖💕',
    text: 'Tienes la dulzura más hermosa',
    mini: '💎'
  },
  {
    emoji: '✨⭐',
    text: 'Brillas con una luz única',
    mini: '💕'
  },
  {
    emoji: '🌹💎',
    text: 'Eres elegante como una rosa',
    mini: '💎'
  },
  {
    emoji: '👑💖',
    text: 'Eres única como una verdadera reina',
    mini: '💕'
  },
  {
    emoji: '🌟💕',
    text: 'Haces que todo sea más hermoso',
    mini: '💎'
  },
  {
    emoji: '👑💎',
    text: 'Eres la reina de mi corazón',
    mini: '💖'
  }
])

// Ref para el contenedor
const qualitiesSection = ref(null)

// Animación inicial al montar el componente
onMounted(() => {
  nextTick(() => {
    const items = qualitiesSection.value?.querySelectorAll('.quality-item')
    
    if (items && items.length > 0) {
      // Animación suave que no oculta los elementos
      gsap.fromTo(items, 
        {
          y: 30,
          scale: 0.95
        },
        {
          duration: 0.8,
          y: 0,
          scale: 1,
          ease: "power2.out",
          stagger: 0.1,
          delay: 2
        }
      )
    }
  })
})

const hoverQuality = (event) => {
  gsap.to(event.target, {
    duration: 0.3,
    scale: 1.05,
    y: -5,
    ease: "back.out(1.7)"
  })
}

const leaveQuality = (event) => {
  gsap.to(event.target, {
    duration: 0.3,
    scale: 1,
    y: 0,
    ease: "back.out(1.7)"
  })
}
</script>

<style scoped>
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
  /* Estilos garantizados para visibilidad */
  opacity: 1 !important;
  visibility: visible !important;
  display: block !important;
  transform: translateX(0) translateY(0) scale(1) rotate(0deg);
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
</style>
