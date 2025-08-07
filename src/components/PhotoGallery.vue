<template>
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
</template>

<script setup>
import { ref } from 'vue'
import { gsap } from 'gsap'

const currentPhotoIndex = ref(0)

// Función para generar rutas correctas para GitHub Pages
const getImagePath = (path) => {
  const base = import.meta.env.BASE_URL || '/'
  return `${base}${path.startsWith('/') ? path.slice(1) : path}`
}

// Array de fotos reales con descripciones
const photos = ref([
  {
    src: getImagePath('images/fotos/foto_nosotros_en_la_universidad.jpg'),
    title: 'Nosotros en la universidad',
    description: 'Donde todo comenzó, nuestros primeros momentos juntos 💖'
  },
  {
    src: getImagePath('images/fotos/foto_juntitos.jpg'), 
    title: 'Momentos tiernos',
    description: 'Juntitos y felices, así es como me gusta estar contigo 💕'
  },
  {
    src: getImagePath('images/fotos/foto_juntos_almorzando.jpg'),
    title: 'Compartiendo momentos',
    description: 'Un almuerzo contigo es especial mi princesa 🌹'
  },
  {
    src: getImagePath('images/fotos/foto_ella_chula_titulandose.jpg'),
    title: 'Mi graduada hermosa',
    description: 'El día que te titulaste, tan orgulloso de ti mi reina 👑'
  },
  {
    src: getImagePath('images/fotos/foto_ella_chula.jpg'),
    title: 'Mi chica hermosa',
    description: 'Siempre tan bella, mi chica perfecta 💎'
  },
  {
    src: getImagePath('images/fotos/foto_ella_chula_con_sus_rosas.jpg'),
    title: 'Mi preciosa con rosas',
    description: 'Tan hermosa con tus rosas, pero tú brillas más 🌹'
  },
  {
    src: getImagePath('images/fotos/foto_juntos_con_sus_rosas.jpg'),
    title: 'Beshito de nosotros',
    description: 'Juntos con tus rosas bellas 💖🌹'
  },
  {
    src: getImagePath('images/fotos/fotos_juntos_elegantes.jpg'),
    title: 'Elegantes como siempre',
    description: 'Tan elegantes juntos, sacando nuestros pasos prohibidos :3 💎👑'
  }
])

const nextPhoto = () => {
  // Animación de transición de fotos
  gsap.to('.photo-placeholder', {
    duration: 0.3,
    rotationY: 90,
    ease: "power2.in",
    onComplete: () => {
      currentPhotoIndex.value = (currentPhotoIndex.value + 1) % photos.value.length
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
      currentPhotoIndex.value = currentPhotoIndex.value === 0 ? photos.value.length - 1 : currentPhotoIndex.value - 1
      gsap.fromTo('.photo-placeholder', 
        { rotationY: 90 },
        { duration: 0.3, rotationY: 0, ease: "power2.out" }
      )
    }
  })
}

const goToPhoto = (index) => {
  if (index !== currentPhotoIndex.value) {
    gsap.to('.photo-placeholder', {
      duration: 0.3,
      rotationY: 90,
      ease: "power2.in",
      onComplete: () => {
        currentPhotoIndex.value = index
        gsap.fromTo('.photo-placeholder', 
          { rotationY: -90 },
          { duration: 0.3, rotationY: 0, ease: "power2.out" }
        )
      }
    })
  }
}

const onPhotoLoad = () => {
  // Animación cuando la foto se carga correctamente
  gsap.from('.real-photo', {
    duration: 0.8,
    scale: 0.8,
    opacity: 0,
    ease: "back.out(1.7)"
  })
}

const onPhotoError = () => {
  console.error('Error cargando la foto:', photos.value[currentPhotoIndex.value].src)
}
</script>

<style scoped>
.photo-gallery {
  margin: 3rem 0;
  padding: 2rem;
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.9), rgba(252, 228, 236, 0.9));
  border-radius: 25px;
  border: 3px solid #ff69b4;
  box-shadow: 0 10px 30px rgba(255, 105, 135, 0.3);
}

.gallery-title {
  color: #d63384;
  text-align: center;
  font-size: 1.8rem;
  margin-bottom: 1rem;
  animation: titlePulse 2s infinite ease-in-out;
}

.elegant-photo-decoration {
  text-align: center;
  font-size: 1.2rem;
  margin-bottom: 2rem;
  animation: photoDecorationSway 3s infinite ease-in-out;
}

@keyframes titlePulse {
  0%, 100% { transform: scale(1); }
  50% { transform: scale(1.05); }
}

@keyframes photoDecorationSway {
  0%, 100% { transform: translateX(0); }
  50% { transform: translateX(10px); }
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

.btn-elegant {
  margin: 0 3px;
  font-size: 0.8rem;
}

.photo-container {
  perspective: 1000px;
}

.photo-frame {
  background: linear-gradient(135deg, #ffffff, #fce4ec);
  border: 5px solid #ff69b4;
  border-radius: 20px;
  position: relative;
  transition: all 0.5s ease;
  transform-style: preserve-3d;
  overflow: hidden;
}

.photo-frame.main-photo {
  width: 600px;
  height: 400px;
  margin: 0 auto;
  display: flex;
  align-items: center;
  justify-content: center;
}

.elegant-photo-border {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
}

.corner-gem {
  position: absolute;
  font-size: 1.2rem;
  animation: gemSparkle 3s infinite ease-in-out;
}

.corner-gem.top-left {
  top: 5px;
  left: 5px;
}

.corner-gem.top-right {
  top: 5px;
  right: 5px;
  animation-delay: 0.5s;
}

.corner-gem.bottom-left {
  bottom: 5px;
  left: 5px;
  animation-delay: 1s;
}

.corner-gem.bottom-right {
  bottom: 5px;
  right: 5px;
  animation-delay: 1.5s;
}

@keyframes gemSparkle {
  0%, 100% { transform: scale(1) rotate(0deg); opacity: 0.8; }
  50% { transform: scale(1.2) rotate(180deg); opacity: 1; }
}

.photo-placeholder {
  position: relative;
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  border-radius: 15px;
  overflow: hidden;
}

.real-photo-container {
  position: relative;
  width: 100%;
  height: 100%;
  border-radius: 15px;
  overflow: hidden;
  box-shadow: 0 10px 30px rgba(255, 105, 135, 0.3);
  display: flex;
  align-items: center;
  justify-content: center;
  background: #ffffff;
}

.real-photo {
  max-width: 100%;
  max-height: 100%;
  width: auto;
  height: auto;
  object-fit: contain;
  transition: all 0.3s ease;
  border-radius: 10px;
}

.real-photo:hover {
  transform: scale(1.02);
}

.photo-overlay {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background: linear-gradient(transparent, rgba(0,0,0,0.8));
  color: white;
  padding: 2rem 1.5rem 1.5rem;
  transform: translateY(100%);
  transition: transform 0.3s ease;
}

.real-photo-container:hover .photo-overlay {
  transform: translateY(0);
}

.photo-title {
  font-size: 1.1rem;
  font-weight: bold;
  margin-bottom: 0.5rem;
  color: #ffd700;
  text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
}

.photo-description {
  font-size: 0.9rem;
  opacity: 0.9;
  margin: 0;
  line-height: 1.4;
}

.photo-effects {
  position: absolute;
  top: 10px;
  right: 10px;
  display: flex;
  gap: 5px;
  pointer-events: none;
}

.heart-effect, .elegant-effect {
  font-size: 1.2rem;
  animation: heartFloat 2s infinite ease-in-out alternate;
}

.elegant-effect {
  animation-delay: 0.5s;
}

@keyframes heartFloat {
  0% { transform: translateY(0) scale(1); }
  100% { transform: translateY(-10px) scale(1.1); }
}

/* Contador de fotos */
.photo-counter {
  text-align: center;
  margin: 1.5rem 0;
  font-size: 1.2rem;
  color: #ff1493;
  font-weight: bold;
}

.current-photo {
  color: #ff69b4;
  font-size: 1.4rem;
}

.separator {
  color: #ffb6c1;
  margin: 0 0.5rem;
}

.total-photos {
  color: #ff1493;
}

/* Thumbnails */
.photo-thumbnails {
  display: flex;
  justify-content: center;
  gap: 0.8rem;
  margin-top: 2rem;
  flex-wrap: wrap;
}

.thumbnail {
  width: 80px;
  height: 80px;
  border-radius: 10px;
  overflow: hidden;
  cursor: pointer;
  position: relative;
  border: 3px solid transparent;
  transition: all 0.3s ease;
}

.thumbnail:hover {
  transform: scale(1.1);
  border-color: #ff69b4;
}

.thumbnail.active {
  border-color: #ff1493;
  transform: scale(1.15);
  box-shadow: 0 5px 15px rgba(255, 20, 147, 0.5);
}

.thumbnail-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: all 0.3s ease;
}

.thumbnail-overlay {
  position: absolute;
  bottom: 2px;
  right: 2px;
  background: rgba(255, 105, 180, 0.9);
  color: white;
  border-radius: 50%;
  width: 20px;
  height: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 0.7rem;
  font-weight: bold;
}

/* Responsive para la galería */
@media (max-width: 768px) {
  .photo-frame.main-photo {
    width: 90vw;
    height: 300px;
  }
  
  .photo-carousel {
    gap: 1rem;
  }
  
  .carousel-btn {
    width: 50px;
    height: 50px;
    font-size: 1rem;
  }
}
</style>
