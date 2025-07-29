<template>
  <div class="min-h-screen relative flex flex-col">
    <!-- Futuristic circular background -->
    <div class="fixed inset-0 z-0 bg-black pointer-events-none">
      <div class="absolute inset-0" style="background: linear-gradient(120deg, rgba(255,255,255,0.10) 0%, rgba(200,230,255,0.08) 100%);"></div>
      <div class="absolute inset-0">
        <div class="absolute" style="top: -20%; right: -10%; width: 80%; height: 80%; background: radial-gradient(circle, rgba(27, 112, 117, 0.15) 0%, rgba(12, 68, 65, 0.08) 30%, transparent 70%); border-radius: 50%; transform: scale(1.2); animation: rotate-slow 60s linear infinite;"></div>
      </div>
      <!-- Overlay texture pattern -->
      <div class="absolute inset-0 opacity-15 pointer-events-none" style="background-image: radial-gradient(circle at 1px 1px, rgba(27, 112, 117, 0.2) 1px, transparent 0); background-size: 25px 25px;"></div>
      
      <!-- Background texture overlay -->
      <div class="absolute inset-0 pointer-events-none">
        <div id="light"></div>
        <img :src="backgroundTexture" alt="" class="w-full h-full object-cover opacity-20" />
      </div>
    </div>
    
    <!-- Main content with custom grid -->
    <main class="relative z-10 px-6 flex-1 flex items-center justify-center">
      <div class="max-w-screen-xl mx-auto w-full h-full flex items-center justify-center">
        <div class="grid-container">

          <!-- Logo - arriba de los textos -->
          <div class="logo-container">
            <img :src="newLogoImg" alt="Logo" class="logo-image" />
          </div>

          <!-- Main title - div6 -->
          <div class="main-title">
            <h1 class="text-5xl lg:text-6xl xl:text-7xl font-extrabold leading-tight">
              <span style="color: #ffffff; text-shadow: 0 0 20px rgba(255, 255, 255, 0.3);">OLIMPIADAS </span>
              <span style="color: #27c479; text-shadow: 0 0 30px rgba(39, 196, 121, 0.8);">UNIVERSITARIAS</span><br>
              <span style="color: #ffffff; text-shadow: 0 0 20px rgba(255, 255, 255, 0.3);">DE </span>
              <span style="color: #27c479; text-shadow: 0 0 30px rgba(39, 196, 121, 0.8);">IA </span>
              <span style="color: #ffffff; text-shadow: 0 0 20px rgba(255, 255, 255, 0.3);">2025</span>
            </h1>
          </div>

          <!-- Description - div7 -->
          <div class="description">
            <p class="text-xl lg:text-2xl leading-relaxed max-w-3xl" style="color: #ffffff; opacity: 0.9; text-shadow: 0 0 15px rgba(255, 255, 255, 0.1);">
              Compite con los mejores estudiantes universitarios en desafíos de 
              inteligencia artificial. Demuestra tus habilidades en machine learning,
              algoritmos y soluciones innovadoras.
            </p>
          </div>

          <!-- Countdown timer cards - lado derecho -->
          <div class="countdown-container">
            <div class="countdown-grid">
              <!-- Días -->
              <div class="countdown-card countdown-card--main" style="grid-area: dias;">
                <div class="text-4xl lg:text-5xl font-bold font-mono">
                  {{ countdown.days }}
                </div>
                <div class="text-sm text-white opacity-70 mt-2">Días</div>
              </div>
              
              <!-- Horas -->
              <div class="countdown-card countdown-card--light countdown-card--up md:translate-y-[-20px]" style="grid-area: horas;">
                <div class="text-4xl lg:text-5xl font-bold font-mono">
                  {{ countdown.hours }}
                </div>
                <div class="text-sm text-white opacity-70 mt-2">Horas</div>
              </div>
              
              <!-- Minutos -->
              <div class="countdown-card countdown-card--light" style="grid-area: minutos;">
                <div class="text-4xl lg:text-5xl font-bold font-mono">
                  {{ countdown.minutes }}
                </div>
                <div class="text-sm text-white opacity-70 mt-2">Minutos</div>
              </div>
              
              <!-- Segundos -->
              <div class="countdown-card countdown-card--light countdown-card--up md:translate-y-[-20px]" style="grid-area: segundos;">
                <div class="text-4xl lg:text-5xl font-bold font-mono">
                  {{ countdown.seconds }}
                </div>
                <div class="text-sm text-white opacity-70 mt-2">Segundos</div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import backgroundTextureImg from '../assets/img/background-no-texture.png'
import newLogoImg from '../assets/img/newLogo.png'
import { tsParticles } from "https://cdn.jsdelivr.net/npm/@tsparticles/engine@3.0.3/+esm";
import { loadAll } from "https://cdn.jsdelivr.net/npm/@tsparticles/all@3.0.3/+esm";

// FECHA Y HORA DEL EVENTO (ajusta aquí)
const eventDateTime = '2025-09-28T00:00:00'

// Countdown timer state
const countdown = ref({
  days: '10',
  hours: '00',
  minutes: '00',
  seconds: '00'
})

// Estado para los fuegos artificiales
const showFireworks = ref(false)
let fireworksLaunched = false // Variable para controlar que solo se lancen una vez

// Timer for countdown
let timer = null

const backgroundTexture = backgroundTextureImg

// Function to update countdown
const updateCountdown = () => {
  // Usa la variable eventDateTime como fecha objetivo
  const now = new Date()
  const targetDate = new Date(eventDateTime)
  
  const diff = targetDate.getTime() - now.getTime()
  
  if (diff > 0) {
    const days = Math.floor(diff / (1000 * 60 * 60 * 24))
    const hours = Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60))
    const minutes = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60))
    const seconds = Math.floor((diff % (1000 * 60)) / 1000)
    
    countdown.value = {
      days: String(days).padStart(2, '0'),
      hours: String(hours).padStart(2, '0'),
      minutes: String(minutes).padStart(2, '0'),
      seconds: String(seconds).padStart(2, '0')
    }
    
    // Resetear la bandera cuando el contador vuelve a ser mayor que 0
    fireworksLaunched = false
  } else {
    // Event has ended
    countdown.value = {
      days: '00',
      hours: '00',
      minutes: '00',
      seconds: '00'
    }
    
    // Lanzar fuegos artificiales solo una vez cuando el contador llegue a 0
    if (!fireworksLaunched) {
      fireworksLaunched = true
      launchFireworks()
    }
  }
}

const launchFireworks = () => {
  showFireworks.value = true

  // Crear múltiples fuegos artificiales distribuidos en 20 segundos
  createFirework()
  setTimeout(() => createFirework(), 500)
  setTimeout(() => createFirework(), 1000)
  setTimeout(() => createFirework(), 1500)
  setTimeout(() => createFirework(), 2000)
  setTimeout(() => createFirework(), 2500)
  setTimeout(() => createFirework(), 3000)
  setTimeout(() => createFirework(), 3500)
  setTimeout(() => createFirework(), 4000)
  setTimeout(() => createFirework(), 4500)
  setTimeout(() => createFirework(), 5000)
  setTimeout(() => createFirework(), 5500)
  setTimeout(() => createFirework(), 6000)
  setTimeout(() => createFirework(), 6500)
  setTimeout(() => createFirework(), 7000)
  setTimeout(() => createFirework(), 7500)
  setTimeout(() => createFirework(), 8000)
  setTimeout(() => createFirework(), 8500)
  setTimeout(() => createFirework(), 9000)
  setTimeout(() => createFirework(), 9500)
  setTimeout(() => createFirework(), 10000)
  setTimeout(() => createFirework(), 10500)
  setTimeout(() => createFirework(), 11000)
  setTimeout(() => createFirework(), 11500)
  setTimeout(() => createFirework(), 12000)
  setTimeout(() => createFirework(), 12500)
  setTimeout(() => createFirework(), 13000)
  setTimeout(() => createFirework(), 13500)
  setTimeout(() => createFirework(), 14000)
  setTimeout(() => createFirework(), 14500)
  setTimeout(() => createFirework(), 15000)
  setTimeout(() => createFirework(), 15500)
  setTimeout(() => createFirework(), 16000)
  setTimeout(() => createFirework(), 16500)
  setTimeout(() => createFirework(), 17000)
  setTimeout(() => createFirework(), 17500)
  setTimeout(() => createFirework(), 18000)
  setTimeout(() => createFirework(), 18500)
  setTimeout(() => createFirework(), 19000)
  setTimeout(() => createFirework(), 19500)

  // Ocultar fuegos artificiales después de 20 segundos
  setTimeout(() => {
    showFireworks.value = false
    // Limpiar partículas restantes
    const fireworks = document.querySelectorAll('.firework-particle')
    fireworks.forEach(fw => fw.remove())
  }, 20000)
}

const createFirework = () => {
  // Usar la paleta de colores de tu página
  const colors = ['#27c479', '#4ade80', '#1b7069', '#34d4a7', '#3dd8ab', '#46dcaf', '#4fe0b3', '#58e4b7', '#61e8bb', '#ffffff']
  const container = document.body

  // Posición aleatoria
  const x = Math.random() * window.innerWidth
  const y = Math.random() * (window.innerHeight / 2) + 100

  // Crear 20-30 partículas por fuego artificial
  const particleCount = 20 + Math.random() * 10

  for (let i = 0; i < particleCount; i++) {
    const particle = document.createElement('div')
    particle.className = 'firework-particle'
    particle.style.cssText = `
      position: fixed;
      left: ${x}px;
      top: ${y}px;
      width: 4px;
      height: 4px;
      background: ${colors[Math.floor(Math.random() * colors.length)]};
      border-radius: 50%;
      pointer-events: none;
      z-index: 1000;
    `

    container.appendChild(particle)

    // Animación de la partícula - duración extendida
    const angle = (Math.PI * 2 * i) / particleCount
    const velocity = 100 + Math.random() * 100
    const life = 3 + Math.random() * 3 // Aumentado de 2-4 segundos a 3-6 segundos

    const dx = Math.cos(angle) * velocity
    const dy = Math.sin(angle) * velocity

    particle.animate([
      {
        transform: 'translate(0, 0) scale(1)',
        opacity: 1
      },
      {
        transform: `translate(${dx}px, ${dy + 100}px) scale(0)`,
        opacity: 0
      }
    ], {
      duration: life * 1000,
      easing: 'cubic-bezier(0.25, 0.46, 0.45, 0.94)'
    }).onfinish = () => {
      particle.remove()
    }
  }
}

onMounted(async () => {
  updateCountdown()
  timer = setInterval(updateCountdown, 1000)

  // Configuración de tsParticles
  await loadAll(tsParticles);

  await tsParticles.addPreset("lightdark", {
    fullScreen: {
      enable: true,
      zIndex: 1
    },
    particles: {
      links: {
        enable: true
      },
      move: {
        enable: true
      },
      number: {
        value: 100,
        density: {
          enable: true,
          area: 150
        }
      },
      opacity: {
        value: { min: 0.005, max: 0.005 }
      },
      shape: {
        type: "text",
        options: {
          text: {
            value: ["*"],
            style: "",
            weight: "1000",
            font: "Arial"
          }
        }
      },
      size: {
        value: { min: 1, max: 1 }
      }
    }
  });

  await tsParticles.load({
    id: "light",
    options: {
      preset: "lightdark",
      particles: {
        color: {
          value: ["#27c479", "#4ade80", "#1b7069"]
        },
        links: {
          color: "#27c479",
          opacity: 0.03,
          width: 2
        },
        size: {
          value: { min: 7, max: 7 }
        },
        opacity: {
          value: { min: 0.3, max: 0.55 }
        }
      }
    }
  });
})

onUnmounted(() => {
  if (timer) {
    clearInterval(timer)
  }
})
</script>

<style scoped>
/* Custom animations */
@keyframes float {
  0%, 100% { transform: translateY(0px) rotate(0deg); }
  50% { transform: translateY(-10px) rotate(180deg); }
}

@keyframes pulse-glow {
  0%, 100% { opacity: 0.4; transform: scale(1); }
  50% { opacity: 0.8; transform: scale(1.1); }
}

@keyframes rotate-slow {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}

@keyframes logo-glow {
  0%, 100% { 
    filter: drop-shadow(0 0 8px rgba(39, 196, 121, 0.5)) 
            drop-shadow(0 0 15px rgba(39, 196, 121, 0.3));
  }
  50% { 
    filter: drop-shadow(0 0 12px rgba(39, 196, 121, 0.8)) 
            drop-shadow(0 0 20px rgba(39, 196, 121, 0.4));
  }
}

/* Floating animation for images */
.animate-float {
  animation: float 8s ease-in-out infinite;
}

/* Custom opacity classes for faded elements */
.opacity-2 { opacity: 0.02; }
.opacity-3 { opacity: 0.03; }
.opacity-4 { opacity: 0.04; }
.opacity-5 { opacity: 0.05; }

.grid-container {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: auto auto auto auto auto;
  gap: 24px 80px;
  height: fit-content;
  width: 100%;
  align-items: center;
  max-width: 1400px;
  margin: 0 auto;
  padding: 0 2rem;
}

@media (min-width: 1440px) {
  .grid-container {
    gap: 24px 120px;
    max-width: 1600px;
    padding: 0 3rem;
  }
}

@media (max-width: 1024px) {
  .grid-container {
    gap: 16px 40px;
    padding: 0 1rem;
  }
  .logo-container,
  .main-title,
  .description {
    padding-left: 0.5rem;
  }
  .countdown-container {
    padding-right: 0.5rem;
  }
}

@media (max-width: 768px) {
  .grid-container {
    grid-template-columns: 1fr;
    grid-template-rows: auto auto auto auto auto auto auto;
    gap: 12px 0;
    justify-items: center;
  }
  .logo-container {
    grid-column: 1;
    grid-row: 1;
    justify-content: center;
  }
  .main-title {
    grid-column: 1;
    grid-row: 2;
    justify-content: center;
    text-align: center;
  }
  .description {
    grid-column: 1;
    grid-row: 3;
    justify-content: center;
    text-align: center;
  }
  .countdown-container {
    grid-column: 1 !important;
    grid-row: 4 !important;
    justify-content: center !important;
    align-items: center !important;
    width: 100%;
    display: flex;
    animation: none;
    margin-top: 1rem;
  }
  .countdown-grid {
    grid-template-columns: 1fr 1fr;
    grid-template-rows: 1fr 1fr;
    gap: 10px 10px;
    margin-top: 0;
    justify-self: center;
  }
}

@media (max-width: 640px) {
  .grid-container {
    justify-items: center !important;
  }
  .main-title,
  .description {
    text-align: center !important;
    justify-content: center !important;
  }
  .countdown-container {
    justify-content: center !important;
    display: flex !important;
    width: 100% !important;
  }
  .countdown-grid {
    justify-content: center !important;
    width: 100% !important;
  }
}

@media (max-width: 640px) {
  .grid-container {
    padding: 0 0.5rem;
  }
  .logo-image {
    height: 48px !important;
  }
  .main-title h1 {
    font-size: 1.3rem !important;
    line-height: 1.7rem !important;
  }
  .description p {
    font-size: 0.95rem !important;
    line-height: 1.2rem !important;
    max-width: 100% !important;
    width: 100% !important;
  }
  .countdown-grid {
    display: flex !important;
    flex-direction: row !important;
    width: 100% !important;
    overflow-x: unset !important;
    gap: 4px !important;
    min-width: 0 !important;
    margin: 0 !important;
    grid-template-columns: unset !important;
    grid-template-rows: unset !important;
    grid-template-areas: unset !important;
  }
  .countdown-card {
    flex: 1 1 0 !important;
    min-width: 0 !important;
    width: auto !important;
    padding: 6px 2px !important;
  }
  .countdown-card .text-4xl,
  .countdown-card .text-5xl {
    font-size: 1.1rem !important;
    line-height: 1.3rem !important;
  }
  .countdown-card .text-sm {
    font-size: 0.7rem !important;
    line-height: 1rem !important;
  }
}

@media (max-width: 640px) {
  .description p {
    max-width: 320px !important;
    width: 100% !important;
    margin-left: auto !important;
    margin-right: auto !important;
  }
}

/* Responsive blobs and backgrounds */
@media (max-width: 1024px) {
  .bg-blur {
    width: 250px !important;
    height: 250px !important;
  }
}
@media (max-width: 768px) {
  .bg-blur {
    width: 160px !important;
    height: 160px !important;
  }
}
@media (max-width: 640px) {
  .bg-blur {
    width: 90px !important;
    height: 90px !important;
  }
}

/* Responsive decorative images */
@media (max-width: 1024px) {
  .decor-img {
    width: 5rem !important;
    height: 5rem !important;
  }
}
@media (max-width: 768px) {
  .decor-img {
    width: 3.5rem !important;
    height: 3.5rem !important;
  }
}
@media (max-width: 640px) {
  .decor-img {
    width: 2rem !important;
    height: 2rem !important;
  }
}

.date-card {
  grid-column: 1;
  grid-row: 1 / -1;
  display: flex;
  align-items: center;
  justify-self: center;
  animation: float-pulse 4s ease-in-out infinite;
}

@keyframes float-pulse {
  0%, 100% {
    transform: translateY(0) scale(1);
    box-shadow: 0 8px 32px rgba(39, 196, 121, 0.35);
  }
  50% {
    transform: translateY(-18px) scale(1.04);
    box-shadow: 0 16px 48px rgba(39, 196, 121, 0.45);
  }
}

@keyframes countdown-float {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-12px);
  }
}

.date-card:hover > div {
  transform: scale(1.05);
  box-shadow: 0 12px 40px rgba(39, 196, 121, 0.5) !important;
  transition: all 0.3s ease;
}

.subtitle {
  grid-column: 1;
  grid-row: 2;
  display: flex;
  align-items: center;
}

.main-title {
  grid-column: 1;
  grid-row: 3;
  display: flex;
  align-items: center;
  justify-content: flex-start;
  padding-left: 1rem;
}

.description {
  grid-column: 1;
  grid-row: 4;
  display: flex;
  align-items: center;
  justify-content: flex-start;
  padding-left: 1rem;
}

.action-buttons {
  grid-column: 1;
  grid-row: 5;
  display: flex;
  align-items: center;
}

.countdown-container {
  grid-column: 2;
  grid-row: 1 / -1;
  display: flex;
  align-items: center;
  justify-content: flex-end;
  animation: countdown-float 5s ease-in-out infinite;
  padding-right: 1rem;
}

.countdown-grid {
  grid-column: 2;
  grid-row: 1 / -1;
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 1fr 1fr;
  gap: 15px 15px;
  justify-self: end;
  align-self: center;
  grid-template-areas:
    "dias horas"
    "minutos segundos";
}

.countdown-card {
  background: #101c1b;
  border: 2px solid #27c479;
  border-radius: 4px;
  padding: 20px 12px;
  text-align: center;
  box-shadow: 0 2px 8px rgba(39, 196, 121, 0.18);
  transition: box-shadow 0.18s cubic-bezier(.4,0,.2,1), border-color 0.18s cubic-bezier(.4,0,.2,1), transform 0.18s cubic-bezier(.4,0,.2,1);
  min-width: 100px;
  font-family: 'Lexend Deca', 'ui-sans-serif', 'system-ui', sans-serif;
}

.countdown-card:hover {
  box-shadow: 0 8px 32px rgba(39, 196, 121, 0.7);
  border-color: #27c479;
  background: #162825;
}
.countdown-card:not(.countdown-card--up):hover {
  transform: translateY(-5px);
}
.countdown-card.countdown-card--up:hover {
  transform: translateY(-25px);
}

/* Fondo y hover para la carta principal (días) */
.countdown-card--main {
  background: linear-gradient(135deg, rgba(39, 196, 121, 0.22) 0%, rgba(27, 112, 117, 0.13) 100%) !important;
  border: 2.5px solid #27c479 !important;
  box-shadow: 0 8px 32px rgba(39, 196, 121, 0.35) !important;
}
.countdown-card--main:hover {
  background: linear-gradient(135deg, rgba(39, 196, 121, 0.32) 0%, rgba(27, 112, 117, 0.18) 100%) !important;
  box-shadow: 0 12px 40px rgba(39, 196, 121, 0.55) !important;
  border-color: #27c479 !important;
  transform: translateY(-8px) scale(1.06);
}

/* Fondo y hover para las cartas secundarias (horas, minutos, segundos) */
.countdown-card--light {
  background: rgba(30, 36, 40, 0.72) !important;
  border: 2.5px solid rgba(200, 210, 220, 0.25) !important; /* borde gris claro opaco */
  box-shadow: 0 2px 8px rgba(39, 196, 121, 0.10) !important;
}
.countdown-card--light:hover {
  background: rgba(50, 56, 60, 0.88) !important;
  border-color: #27c479 !important; /* verde en hover para coherencia visual */
  box-shadow: 0 8px 32px rgba(39, 196, 121, 0.18) !important;
  transform: translateY(-10px) scale(1.04);
}

.countdown-card--main, .countdown-card--light {
  background: linear-gradient(135deg, rgba(39, 196, 121, 0.22) 0%, rgba(27, 112, 117, 0.13) 100%) !important;
  border: 2.5px solid #27c479 !important;
  box-shadow: 0 8px 32px rgba(39, 196, 121, 0.35) !important;
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);
}
.countdown-card--main:hover, .countdown-card--light:hover {
  background: linear-gradient(135deg, rgba(39, 196, 121, 0.32) 0%, rgba(27, 112, 117, 0.18) 100%) !important;
  box-shadow: 0 12px 40px rgba(39, 196, 121, 0.55) !important;
  border-color: #27c479 !important;
  transform: translateY(-8px) scale(1.06);
}

.date-card > div {
  border-radius: 4px !important;
  font-family: 'Lexend Deca', 'ui-sans-serif', 'system-ui', sans-serif !important;
}

button, .action-buttons button {
  border-radius: 0 !important;
  text-transform: uppercase;
  font-weight: 800;
  font-family: 'Lexend Deca', 'ui-sans-serif', 'system-ui', sans-serif !important;
  letter-spacing: 0.04em;
}

.main-title h1, .main-title span {
  font-family: 'Lexend Deca', 'ui-sans-serif', 'system-ui', sans-serif !important;
  font-weight: 800 !important;
  letter-spacing: 0.01em;
}

.countdown-card .text-4xl, .countdown-card .text-5xl, .countdown-card .font-mono {
  font-family: 'Lexend Deca', 'ui-sans-serif', 'system-ui', sans-serif !important;
  font-weight: 800 !important;
}

.countdown-card--main .text-4xl,
.countdown-card--main .text-5xl,
.countdown-card--main .font-mono {
  color: #27c479 !important;
  text-shadow: 0 0 25px rgba(39, 196, 121, 0.7);
}

.countdown-card--light .text-4xl,
.countdown-card--light .text-5xl,
.countdown-card--light .font-mono {
  color: #f5f7fa !important;
  text-shadow: 0 0 18px rgb(250, 245, 245);
}

.logo-container {
  margin-top: 1rem;
  margin-bottom: 0.5rem;
  grid-column: 1;
  grid-row: 1;
  display: flex;
  justify-content: flex-start;
  align-items: center;
  padding-left: 1rem;
}

.logo-image {
  height: 100px; /* Aumenté el tamaño temporalmente */
  width: auto;
  object-fit: contain;
  animation: logo-glow 3s ease-in-out infinite;
  transition: all 0.3s ease;
  position: relative;
}

.logo-image:hover {
  transform: scale(1.05);
  filter: drop-shadow(0 0 12px rgba(39, 196, 121, 0.9)) 
          drop-shadow(0 0 20px rgba(39, 196, 121, 0.5))
          brightness(1.05);
}

@media (max-width: 768px) {
  .countdown-container {
    display: block !important;
    width: 100% !important;
    margin: 1.5rem 0 0 0 !important;
    grid-column: unset !important;
    grid-row: unset !important;
    justify-content: unset !important;
    align-items: unset !important;
  }
  .countdown-grid {
    width: 100% !important;
    margin: 0 auto !important;
    grid-column: unset !important;
    grid-row: unset !important;
    justify-self: unset !important;
  }
}

@media (max-width: 768px) {
  .logo-container,
  .main-title,
  .description,
  .subtitle,
  .action-buttons,
  .countdown-container {
    grid-column: unset !important;
    grid-row: unset !important;
  }
}

@media (max-width: 640px) {
  .countdown-grid {
    display: flex !important;
    flex-direction: row !important;
    overflow-x: auto !important;
    gap: 6px !important;
    width: 100vw !important;
    min-width: 0 !important;
    margin: 0 !important;
    grid-template-columns: unset !important;
    grid-template-rows: unset !important;
    grid-template-areas: unset !important;
  }
  .countdown-card {
    min-width: 90px !important;
    flex: 0 0 auto !important;
  }
}

@media (max-width: 640px) {
  body {
    overflow-x: hidden !important;
  }
  .main,
  .grid-container,
  .countdown-grid {
    width: 100% !important;
    min-width: 0 !important;
    padding-left: 0 !important;
    padding-right: 0 !important;
    margin-left: 0 !important;
    margin-right: 0 !important;
  }
}

@media (max-width: 640px) {
  .countdown-card:hover,
  .countdown-card--main:hover,
  .countdown-card--light:hover {
    background: linear-gradient(135deg, rgba(39, 196, 121, 0.22) 0%, rgba(27, 112, 117, 0.13) 100%) !important;
    border: 2.5px solid #27c479 !important;
    box-shadow: 0 8px 32px rgba(39, 196, 121, 0.35) !important;
    transform: none !important;
    filter: none !important;
  }
}

/* Estilos para los fuegos artificiales */
.firework-particle {
  position: fixed;
  pointer-events: none;
  z-index: 1000;
  border-radius: 50%;
  box-shadow: 0 0 6px currentColor;
  animation: firework-glow 0.5s ease-out;
}

@keyframes firework-glow {
  0% {
    box-shadow: 0 0 2px currentColor;
  }
  50% {
    box-shadow: 0 0 8px currentColor, 0 0 12px currentColor;
  }
  100% {
    box-shadow: 0 0 4px currentColor;
  }
}

/* Efecto de brillo adicional para las partículas */
.firework-particle::before {
  content: '';
  position: absolute;
  top: -2px;
  left: -2px;
  right: -2px;
  bottom: -2px;
  border-radius: 50%;
  background: radial-gradient(circle, currentColor 0%, transparent 70%);
  opacity: 0.3;
  animation: firework-pulse 1s ease-out;
}

@keyframes firework-pulse {
  0% {
    transform: scale(0.5);
    opacity: 0.8;
  }
  100% {
    transform: scale(2);
    opacity: 0;
  }
}
</style>

<style>
/* Asegura que html, body y #app ocupen todo el alto */
html, body, #app {
  height: 100%;
  margin: 0;
  padding: 0;
}

/* El div raíz debe ocupar todo el alto */
.min-h-screen {
  min-height: 100vh;
}

/* Centrado del main */
main {
  display: flex !important;
  align-items: center !important;
  justify-content: center !important;
  min-height: 100vh !important;
}

#light {
	position: absolute;
	top: 0;
	left: 0;
	width: 100%;
	height: 100%;
	z-index: 1;
}

#light canvas {
	background-color: transparent;
	position: absolute;
	top: 0;
	left: 0;
	width: 100% !important;
	height: 100% !important;
}
</style>
