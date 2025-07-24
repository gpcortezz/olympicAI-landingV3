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
        <img :src="backgroundTexture" alt="" class="w-full h-full object-cover opacity-20" />
      </div>
    </div>
    
    <!-- Main content with custom grid -->
    <main class="relative z-10 px-3 flex-1 flex items-center justify-center">
      <div class="max-w-screen-xl mx-auto w-full h-full flex items-center justify-center">
        <div class="grid-container">

          <!-- Logo - arriba de los textos -->
          <div class="logo-container">
            <img :src="newLogoImg" alt="Logo" class="logo-image" />
          </div>

          <!-- Main title - div6 -->
          <div class="main-title">
            <h1 class="text-5xl lg:text-6xl xl:text-7xl font-extrabold leading-tight">
              <span style="color: #ffffff; text-shadow: 0 0 20px rgba(255, 255, 255, 0.3);">Olimpiadas </span>
              <span style="color: #27c479; text-shadow: 0 0 30px rgba(39, 196, 121, 0.8);">PRODUCT</span><br>
              <span style="color: #ffffff; text-shadow: 0 0 20px rgba(255, 255, 255, 0.3);">KEYNOTE </span>
              <span style="color: #27c479; text-shadow: 0 0 30px rgba(39, 196, 121, 0.8);">2023</span>
            </h1>
          </div>

          <!-- Description - div7 -->
          <div class="description">
            <p class="text-xl lg:text-2xl leading-relaxed max-w-xl" style="color: #ffffff; opacity: 0.9; text-shadow: 0 0 15px rgba(255, 255, 255, 0.1);">
              Travaillez ensemble en temps réel et offrez aux designers de nouvelles 
              façons de créer. Maintenez l'efficacité des workflows grâce à
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

// FECHA Y HORA DEL EVENTO (ajusta aquí)
const eventDateTime = '2025-09-18T18:00:00'

// Countdown timer state
const countdown = ref({
  days: '10',
  hours: '00',
  minutes: '00',
  seconds: '00'
})

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
  } else {
    // Event has ended
    countdown.value = {
      days: '00',
      hours: '00',
      minutes: '00',
      seconds: '00'
    }
  }
}

onMounted(() => {
  updateCountdown()
  timer = setInterval(updateCountdown, 1000)
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
  grid-template-columns: auto 1fr auto;
  grid-template-rows: auto auto auto auto auto;
  gap: 24px 40px;
  height: fit-content;
  width: 100%;
  align-items: center;
}

@media (max-width: 1024px) {
  .grid-container {
    gap: 16px 16px;
  }
}

@media (max-width: 768px) {
  .grid-container {
    grid-template-columns: 1fr;
    grid-template-rows: auto auto auto auto auto auto auto;
    gap: 12px 0;
    justify-items: center;
  }
  .date-card {
    grid-column: 1;
    grid-row: 1;
    margin-bottom: 0.5rem;
    justify-content: center;
  }
  .logo-container {
    grid-column: 1;
    grid-row: 2;
    justify-content: flex-start;
  }
  .main-title {
    grid-column: 1;
    grid-row: 3;
    justify-content: flex-start;
    text-align: left;
  }
  .description {
    grid-column: 1;
    grid-row: 4;
    justify-content: flex-start;
    text-align: left;
  }
  .countdown-grid {
    grid-column: 1;
    grid-row: 5;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: 1fr 1fr;
    gap: 10px 10px;
    margin-top: 1rem;
    justify-self: center;
  }
}

@media (max-width: 640px) {
  .grid-container {
    gap: 8px 0;
    padding: 0 0.5rem;
  }
  .logo-image {
    height: 60px;
  }
  .main-title h1 {
    font-size: 2rem !important;
    line-height: 2.4rem !important;
  }
  .description p {
    font-size: 1rem !important;
    line-height: 1.4rem !important;
  }
  .countdown-card {
    min-width: 70px;
    padding: 12px 6px;
  }
  .date-card > div {
    padding: 10px 8px !important;
  }
  .countdown-grid {
    grid-template-columns: 1fr !important;
    grid-template-rows: repeat(4, 1fr) !important;
    gap: 6px 0 !important;
  }
}
@media (min-width: 641px) and (max-width: 1023px) {
  .countdown-grid {
    grid-template-columns: repeat(4, 1fr) !important;
    grid-template-rows: 1fr !important;
    gap: 10px 10px !important;
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
  grid-column: 2;
  grid-row: 2;
  display: flex;
  align-items: center;
}

.main-title {
  grid-column: 2;
  grid-row: 3;
  display: flex;
  align-items: center;
}

.description {
  grid-column: 2;
  grid-row: 4;
  display: flex;
  align-items: center;
}

.action-buttons {
  grid-column: 2;
  grid-row: 5;
  display: flex;
  align-items: center;
}

.countdown-container {
  grid-column: 3;
  grid-row: 1 / -1;
  display: flex;
  align-items: center;
  animation: countdown-float 5s ease-in-out infinite;
}

.countdown-grid {
  grid-column: 3;
  grid-row: 1 / -1;
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 1fr 1fr;
  gap: 15px 15px;
  justify-self: center;
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
  grid-column: 2;
  grid-row: 1;
  display: flex;
  justify-content: flex-start;
  align-items: center;
  margin-bottom: 1rem;
  padding: 10px;
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
</style>
