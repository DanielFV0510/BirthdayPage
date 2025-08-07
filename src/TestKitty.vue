<template>
  <div id="app">
    <div class="simple-test">
      <h1>🐱 Test Simple Hello Kitty 🐱</h1>
      
      <div class="test-grid">
        <div class="test-item">
          <h3>Imagen SVG Directa:</h3>
          <img src="/images/hello-kitty-1.png" alt="Hello Kitty 1" class="direct-img" />
        </div>
        
        <div class="test-item">
          <h3>Hello Kitty con Emoji:</h3>
          <div class="emoji-kitty">🐱</div>
        </div>
        
        <div class="test-item">
          <h3>Hello Kitty Flotante (como en el código):</h3>
          <div class="hello-kitty-float">
            <img src="/images/hello-kitty-2.jpg" alt="Hello Kitty Float" class="kitty-svg" />
          </div>
        </div>
        
        <div class="test-item">
          <h3>Hello Kitty en esquina:</h3>
          <img src="/images/hello-kitty-birthday.png" alt="Hello Kitty Corner" class="kitty-corner-svg" />
        </div>
      </div>
      
      <div class="back-button">
        <a href="/" style="color: white; text-decoration: none; background: #ff69b4; padding: 10px 20px; border-radius: 25px;">
          🏠 Volver a la página principal
        </a>
      </div>
    </div>
  </div>
</template>

<script setup>
// Componente de prueba simple sin animaciones complejas
</script>

<style scoped>
#app {
  background: linear-gradient(135deg, #ff69b4, #ffc0cb, #ff1493);
  min-height: 100vh;
  padding: 20px;
  font-family: 'Comic Sans MS', cursive;
}

.simple-test {
  text-align: center;
  color: white;
}

h1 {
  font-size: 2.5rem;
  text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
  margin-bottom: 2rem;
}

.test-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
  margin: 2rem 0;
}

.test-item {
  background: rgba(255, 255, 255, 0.9);
  padding: 1.5rem;
  border-radius: 20px;
  color: #ff1493;
  box-shadow: 0 8px 25px rgba(0,0,0,0.2);
}

.test-item h3 {
  margin-bottom: 1rem;
  color: #ff1493;
}

.direct-img {
  width: 80px;
  height: 80px;
  border: 2px solid #ff69b4;
  border-radius: 50%;
  background: white;
  padding: 5px;
}

.emoji-kitty {
  font-size: 4rem;
  animation: bounce 2s infinite;
}

.hello-kitty-float {
  display: inline-block;
  animation: float 3s ease-in-out infinite;
}

.kitty-svg {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  filter: drop-shadow(0 5px 10px rgba(255, 105, 135, 0.3));
  transition: all 0.3s ease;
}

.kitty-svg:hover {
  transform: scale(1.2);
}

.kitty-corner-svg {
  width: 80px;
  height: 80px;
  filter: drop-shadow(0 5px 15px rgba(255, 105, 135, 0.4));
  transition: all 0.3s ease;
}

.back-button {
  margin-top: 3rem;
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

@keyframes float {
  0%, 100% {
    transform: translateY(0px);
  }
  50% {
    transform: translateY(-20px);
  }
}
</style>
