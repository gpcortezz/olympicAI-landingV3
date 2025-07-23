<template>
  <div class="min-h-screen relative flex flex-col">
    <!-- Futuristic circular background -->
    <div class="fixed inset-0 z-0 bg-black pointer-events-none">
      <!-- Fondo azul translúcido en vez de negro -->
      <div class="absolute inset-0" style="background: linear-gradient(120deg, rgba(36,80,180,0.38) 0%, rgba(27,112,117,0.22) 100%);"></div>
      <!-- Overlay blanco/azul claro para iluminar -->
      <div class="absolute inset-0" style="background: linear-gradient(120deg, rgba(255,255,255,0.10) 0%, rgba(200,230,255,0.08) 100%);"></div>
      <!-- Gradiente radial claro en el centro -->
      <div class="absolute inset-0" style="background: radial-gradient(circle at 55% 55%, rgba(255,255,255,0.18) 0%, transparent 60%);"></div>
      <!-- Blobs/Manchas difuminadas -->
      <div class="absolute bg-blur" style="top: 10%; left: 5%; width: 400px; height: 400px; background: radial-gradient(circle, rgba(27, 112, 117, 0.48) 0%, transparent 70%); border-radius: 50%; filter: blur(8px);"></div>
      <div class="absolute bg-blur" style="top: 60%; left: 15%; width: 300px; height: 300px; background: radial-gradient(circle, rgba(39, 196, 121, 0.38) 0%, transparent 70%); border-radius: 50%; filter: blur(12px);"></div>
      <div class="absolute bg-blur" style="top: 10%; right: 5%; width: 500px; height: 500px; background: radial-gradient(circle, rgba(12, 68, 65, 0.38) 0%, transparent 70%); border-radius: 50%; filter: blur(12px);"></div>
      <div class="absolute bg-blur" style="bottom: 10%; right: 20%; width: 250px; height: 250px; background: radial-gradient(circle, rgba(27, 112, 117, 0.32) 0%, transparent 70%); border-radius: 50%; filter: blur(14px);"></div>
      <div class="absolute bg-blur" style="bottom: 20%; right: 8%; width: 300px; height: 300px; background: radial-gradient(circle, rgba(39, 196, 121, 0.28) 0%, transparent 70%); border-radius: 50%; filter: blur(16px);"></div>
      
      <!-- Large background circles -->
      <div class="absolute inset-0">
        <!-- Main large circle -->
        <div class="absolute" style="top: -20%; right: -10%; width: 80%; height: 80%; background: radial-gradient(circle, rgba(27, 112, 117, 0.15) 0%, rgba(12, 68, 65, 0.08) 30%, transparent 70%); border-radius: 50%; transform: scale(1.2); animation: rotate-slow 60s linear infinite;"></div>

        <!-- Small accent circles -->
        <div class="absolute" style="top: 10%; right: 20%; width: 200px; height: 200px; background: radial-gradient(circle, rgba(27, 112, 117, 0.18) 0%, rgba(12, 68, 65, 0.08) 50%, transparent 70%); border-radius: 50%; animation: float 6s ease-in-out infinite;"></div>
        <div class="absolute" style="bottom: 20%; left: 10%; width: 150px; height: 150px; background: radial-gradient(circle, rgba(39, 196, 121, 0.14) 0%, rgba(27, 112, 117, 0.06) 50%, transparent 70%); border-radius: 50%; animation: pulse-glow 10s ease-in-out infinite reverse;"></div>
        <div class="absolute" style="top: 60%; right: 5%; width: 100px; height: 100px; background: radial-gradient(circle, rgba(12, 68, 65, 0.2) 0%, rgba(27, 112, 117, 0.1) 40%, transparent 60%); border-radius: 50%; animation: float 8s ease-in-out infinite;"></div>
      </div>
      
      <!-- Floating particles/dots -->
      <div class="absolute inset-0">
        <div class="absolute animate-pulse" style="top: 15%; left: 25%; width: 3px; height: 3px; background: #27c479; border-radius: 50%; box-shadow: 0 0 10px rgba(39, 196, 121, 0.8);"></div>
        <div class="absolute animate-pulse" style="top: 40%; right: 30%; width: 2px; height: 2px; background: #34a059; border-radius: 50%; box-shadow: 0 0 8px rgba(52, 160, 89, 0.6); animation-delay: 1s;"></div>
        <div class="absolute animate-pulse" style="bottom: 30%; left: 40%; width: 4px; height: 4px; background: #27c479; border-radius: 50%; box-shadow: 0 0 12px rgba(39, 196, 121, 0.9); animation-delay: 2s;"></div>
        <div class="absolute animate-pulse" style="top: 70%; right: 45%; width: 2px; height: 2px; background: #1b7075; border-radius: 50%; box-shadow: 0 0 6px rgba(27, 112, 117, 0.7); animation-delay: 0.5s;"></div>
        <div class="absolute animate-pulse" style="top: 25%; right: 60%; width: 3px; height: 3px; background: #27c479; border-radius: 50%; box-shadow: 0 0 10px rgba(39, 196, 121, 0.8); animation-delay: 1.5s;"></div>
      </div>
      
      <!-- Floating background images (faded) -->
      <div class="absolute inset-0 overflow-hidden">
        <!-- Asterisco elements -->
        <img :src="asterisco" alt="" class="absolute opacity-5 object-contain animate-float decor-img" style="top: 20%; right: 15%; filter: sepia(100%) saturate(200%) hue-rotate(90deg); animation: float 12s ease-in-out infinite;" />
        <img :src="asterisco" alt="" class="absolute opacity-3 object-contain animate-float decor-img" style="bottom: 25%; left: 20%; filter: sepia(100%) saturate(200%) hue-rotate(90deg); animation: float 15s ease-in-out infinite reverse;" />
        <img :src="asterisco" alt="" class="absolute opacity-4 object-contain animate-float decor-img" style="top: 60%; right: 70%; filter: sepia(100%) saturate(200%) hue-rotate(90deg); animation: float 18s ease-in-out infinite;" />
        

        <!-- Additional asterisco elements for depth -->
        <img :src="asterisco" alt="" class="absolute opacity-3 object-contain animate-float decor-img" style="bottom: 10%; right: 5%; filter: sepia(100%) saturate(200%) hue-rotate(90deg); animation: rotate-slow 80s linear infinite;" />
        <img :src="asterisco" alt="" class="absolute opacity-2 object-contain animate-float decor-img" style="top: 80%; left: 5%; filter: sepia(100%) saturate(200%) hue-rotate(90deg); animation: float 22s ease-in-out infinite reverse;" />
      </div>
      
      <!-- Overlay texture pattern -->
      <div class="absolute inset-0 opacity-15 pointer-events-none" style="background-image: radial-gradient(circle at 1px 1px, rgba(27, 112, 117, 0.2) 1px, transparent 0); background-size: 25px 25px;"></div>
      
      <!-- Content area fade -->
      <div class="absolute inset-0 pointer-events-none" style="background: linear-gradient(to right, rgba(27, 112, 117, 0.4) 0%, rgba(12, 68, 65, 0.2) 40%, transparent 80%);"></div>
    </div>
    
    <!-- Main content with custom grid -->
    <main class="relative z-10 px-3 flex-1 flex items-center justify-center">
      <div class="max-w-screen-xl mx-auto w-full h-full flex items-center justify-center">
        <div class="grid-container">
          <!-- Date card - div4 -->
          <div class="date-card">
            <div class="rounded-lg p-4 shadow-lg h-fit" style="border: 2px solid #27c479; background: linear-gradient(135deg, rgba(39, 196, 121, 0.1) 0%, rgba(27, 112, 117, 0.08) 100%); backdrop-filter: blur(10px); box-shadow: 0 8px 32px rgba(39, 196, 121, 0.3);">
              <div class="text-center">
                <div class="text-3xl font-bold text-black" style="color: #27c479;">19</div>
                <div class="text-3xl font-bold text-black" style="color: #27c479;">20</div>
                <div class="text-sm font-medium text-gray-600 mt-0.5" style="color: #34a059;">JANV.</div>
                <div class="text-base font-bold text-black" style="color: #27c479;">2023</div>
              </div>
            </div>
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
    </main>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import asteriscoImg from '../assets/img/asterisco.png'
import trophyImg from '../assets/img/trophy.png'

// FECHA Y HORA DEL EVENTO (ajusta aquí)
const eventDateTime = '2025-10-01T18:00:00'

// Countdown timer state
const countdown = ref({
  days: '10',
  hours: '00',
  minutes: '00',
  seconds: '00'
})

// Date display for the event
const eventDate = ref({
  day1: '00',
  day2: '00',
  month: 'JAN',
  year: '2024'
})

// Timer for countdown
let timer = null

// Background images references
const asterisco = asteriscoImg
const trophy = trophyImg

// Function to update countdown
const updateCountdown = () => {
  // Usa la variable eventDateTime como fecha objetivo
  const now = new Date()
  const targetDate = new Date(eventDateTime)
  
  // Update event date display
  const monthNames = ['JAN', 'FEB', 'MAR', 'APR', 'MAY', 'JUN', 
                     'JUL', 'AUG', 'SEP', 'OCT', 'NOV', 'DEC']
  const eventDay = targetDate.getDate()
  eventDate.value = {
    day1: String(Math.floor(eventDay / 10)),
    day2: String(eventDay % 10),
    month: monthNames[targetDate.getMonth()],
    year: String(targetDate.getFullYear())
  }
  
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
  grid-template-rows: auto auto auto auto;
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
    grid-template-rows: auto auto auto auto auto auto;
    gap: 12px 0;
    justify-items: center;
  }
  .date-card {
    grid-column: 1;
    grid-row: 1;
    margin-bottom: 0.5rem;
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
  .countdown-grid {
    grid-column: 1;
    grid-row: 4;
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

.date-card:hover > div {
  transform: scale(1.05);
  box-shadow: 0 12px 40px rgba(39, 196, 121, 0.5) !important;
  transition: all 0.3s ease;
}

.subtitle {
  grid-column: 2;
  grid-row: 1;
  display: flex;
  align-items: center;
}

.main-title {
  grid-column: 2;
  grid-row: 2;
  display: flex;
  align-items: center;
}

.description {
  grid-column: 2;
  grid-row: 3;
  display: flex;
  align-items: center;
}

.action-buttons {
  grid-column: 2;
  grid-row: 4;
  display: flex;
  align-items: center;
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
</style>
