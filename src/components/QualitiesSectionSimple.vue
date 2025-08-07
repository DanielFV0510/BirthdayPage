<template>
  <div class="qualities-section-simple">
    <h3>TEST - Eres mi chica perfecta porque...</h3>
    <div class="qualities-grid-simple">
      <div class="quality-item-simple">
        <span>💖💕</span>
        <span>Tienes la dulzura más hermosa</span>
      </div>
      <div class="quality-item-simple">
        <span>✨⭐</span>
        <span>Brillas con una luz única</span>
      </div>
      <div class="quality-item-simple">
        <span>🌹💎</span>
        <span>Eres elegante como una rosa</span>
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted } from 'vue'

onMounted(() => {
  console.log('QualitiesSectionSimple mounted!')
})
</script>

<style scoped>
.qualities-section-simple {
  margin: 2rem 0;
  padding: 1rem;
  background: rgba(255, 192, 203, 0.1);
  border: 2px solid #ff69b4;
}

.qualities-grid-simple {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 1rem;
  margin-top: 1rem;
}

.quality-item-simple {
  background: linear-gradient(135deg, #ffeaa7, #fab1a0);
  padding: 1rem;
  border-radius: 10px;
  text-align: center;
  border: 2px solid #ff69b4;
  opacity: 1 !important;
  visibility: visible !important;
  display: block !important;
}

.quality-item-simple span {
  display: block;
  margin: 0.5rem 0;
  font-size: 1.1rem;
  color: #d63384;
}
</style>
