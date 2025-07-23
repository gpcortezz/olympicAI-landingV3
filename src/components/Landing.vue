<template>
  <div class="h-screen relative overflow-hidden flex flex-col">
    <!-- Futuristic circular background -->
    <div class="absolute inset-0 z-0 bg-black">
      <!-- Base gradient -->
      <div class="absolute inset-0" style="background: radial-gradient(circle at 30% 50%, rgba(39, 196, 121, 0.15) 0%, rgba(27, 112, 117, 0.08) 30%, rgba(5, 24, 23, 0.95) 70%, #000000 100%);"></div>
      
      <!-- Large background circles -->
      <div class="absolute inset-0">
        <!-- Main large circle -->
        <div class="absolute" style="top: -20%; right: -10%; width: 80%; height: 80%; background: radial-gradient(circle, rgba(39, 196, 121, 0.1) 0%, rgba(39, 196, 121, 0.05) 30%, transparent 70%); border-radius: 50%; transform: scale(1.2); animation: rotate-slow 60s linear infinite;"></div>
        
        <!-- Secondary circle -->
        <div class="absolute" style="top: 30%; left: -15%; width: 60%; height: 60%; background: radial-gradient(circle, rgba(27, 112, 117, 0.08) 0%, rgba(27, 112, 117, 0.03) 40%, transparent 70%); border-radius: 50%; animation: pulse-glow 8s ease-in-out infinite;"></div>
        
        <!-- Small accent circles -->
        <div class="absolute" style="top: 10%; right: 20%; width: 200px; height: 200px; background: radial-gradient(circle, rgba(39, 196, 121, 0.15) 0%, transparent 60%); border-radius: 50%; animation: float 6s ease-in-out infinite;"></div>
        <div class="absolute" style="bottom: 20%; left: 10%; width: 150px; height: 150px; background: radial-gradient(circle, rgba(52, 160, 89, 0.12) 0%, transparent 60%); border-radius: 50%; animation: pulse-glow 10s ease-in-out infinite reverse;"></div>
        <div class="absolute" style="top: 60%; right: 5%; width: 100px; height: 100px; background: radial-gradient(circle, rgba(39, 196, 121, 0.2) 0%, transparent 50%); border-radius: 50%; animation: float 8s ease-in-out infinite;"></div>
      </div>
      
      <!-- Floating particles/dots -->
      <div class="absolute inset-0">
        <div class="absolute animate-pulse" style="top: 15%; left: 25%; width: 3px; height: 3px; background: #27c479; border-radius: 50%; box-shadow: 0 0 10px rgba(39, 196, 121, 0.8);"></div>
        <div class="absolute animate-pulse" style="top: 40%; right: 30%; width: 2px; height: 2px; background: #34a059; border-radius: 50%; box-shadow: 0 0 8px rgba(52, 160, 89, 0.6); animation-delay: 1s;"></div>
        <div class="absolute animate-pulse" style="bottom: 30%; left: 40%; width: 4px; height: 4px; background: #27c479; border-radius: 50%; box-shadow: 0 0 12px rgba(39, 196, 121, 0.9); animation-delay: 2s;"></div>
        <div class="absolute animate-pulse" style="top: 70%; right: 45%; width: 2px; height: 2px; background: #1b7075; border-radius: 50%; box-shadow: 0 0 6px rgba(27, 112, 117, 0.7); animation-delay: 0.5s;"></div>
        <div class="absolute animate-pulse" style="top: 25%; right: 60%; width: 3px; height: 3px; background: #27c479; border-radius: 50%; box-shadow: 0 0 10px rgba(39, 196, 121, 0.8); animation-delay: 1.5s;"></div>
      </div>
      
      <!-- Overlay texture pattern -->
      <div class="absolute inset-0 opacity-20" style="background-image: radial-gradient(circle at 1px 1px, rgba(39, 196, 121, 0.15) 1px, transparent 0); background-size: 20px 20px;"></div>
      
      <!-- Content area fade -->
      <div class="absolute inset-0" style="background: linear-gradient(to right, rgba(0,0,0,0.3) 0%, rgba(0,0,0,0.1) 40%, transparent 80%);"></div>
    </div>
    
    <!-- Main content with custom grid -->
    <main class="relative z-10 px-3 flex-1 flex items-center justify-center">
      <div class="max-w-7xl mx-auto w-full h-full flex items-center justify-center">
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

          <!-- Subtitle - div5 -->
          <div class="subtitle">
            <div class="text-sm font-medium tracking-wider uppercase" style="color: #34a059; text-shadow: 0 0 10px rgba(52, 160, 89, 0.5);">
              #FoF PRESENTE
            </div>
          </div>

          <!-- Main title - div6 -->
          <div class="main-title">
            <h1 class="text-4xl lg:text-5xl xl:text-6xl font-black leading-tight">
              <span style="color: #ffffff; text-shadow: 0 0 20px rgba(255, 255, 255, 0.3);">Africa</span><br>
              <span style="color: #27c479; text-shadow: 0 0 30px rgba(39, 196, 121, 0.8);">Product</span> <span style="color: #ffffff; text-shadow: 0 0 20px rgba(255, 255, 255, 0.3);">Keynote</span>
            </h1>
          </div>

          <!-- Description - div7 -->
          <div class="description">
            <p class="text-base lg:text-lg leading-relaxed max-w-md" style="color: #ffffff; opacity: 0.9; text-shadow: 0 0 15px rgba(255, 255, 255, 0.1);">
              Travaillez ensemble en temps réel et offrez aux designers de nouvelles 
              façons de créer. Maintenez l'efficacité des workflows grâce à
            </p>
          </div>

          <!-- Action buttons - div8 -->
          <div class="action-buttons">
            <div class="flex items-center space-x-3">
              <button class="text-white px-6 py-3 rounded-lg font-medium transition-colors text-base" 
                      style="background-color: #27c479; border: 2px solid #27c479;"
                      @mouseover="$event.target.style.backgroundColor='#34a059'"
                      @mouseout="$event.target.style.backgroundColor='#27c479'">
                INSCRIPTION
              </button>
              <button class="px-6 py-3 rounded-lg font-medium transition-colors text-base" 
                      style="background-color: rgba(39, 196, 121, 0.1); color: #27c479; border: 2px solid #27c479;"
                      @mouseover="$event.target.style.backgroundColor='rgba(39, 196, 121, 0.2)'"
                      @mouseout="$event.target.style.backgroundColor='rgba(39, 196, 121, 0.1)'">
                À PROPOS
              </button>
            </div>
          </div>

          <!-- Countdown timer - div9 -->
          <div class="countdown-timer">
            <div class="flex items-center space-x-2">
              <div class="text-center">
                <div class="text-2xl lg:text-3xl xl:text-4xl font-bold font-mono" style="color: #27c479; text-shadow: 0 0 25px rgba(39, 196, 121, 0.7);">
                  {{ countdown.days }}
                </div>
                <div class="text-xs text-white opacity-70 mt-1">DÍAS</div>
              </div>
              <div class="text-2xl lg:text-3xl xl:text-4xl font-bold" style="color: #34a059;">:</div>
              <div class="text-center">
                <div class="text-2xl lg:text-3xl xl:text-4xl font-bold font-mono" style="color: #27c479; text-shadow: 0 0 25px rgba(39, 196, 121, 0.7);">
                  {{ countdown.hours }}
                </div>
                <div class="text-xs text-white opacity-70 mt-1">HRS</div>
              </div>
              <div class="text-2xl lg:text-3xl xl:text-4xl font-bold" style="color: #34a059;">:</div>
              <div class="text-center">
                <div class="text-2xl lg:text-3xl xl:text-4xl font-bold font-mono" style="color: #27c479; text-shadow: 0 0 25px rgba(39, 196, 121, 0.7);">
                  {{ countdown.minutes }}
                </div>
                <div class="text-xs text-white opacity-70 mt-1">MIN</div>
              </div>
              <div class="text-2xl lg:text-3xl xl:text-4xl font-bold" style="color: #34a059;">:</div>
              <div class="text-center">
                <div class="text-2xl lg:text-3xl xl:text-4xl font-bold font-mono" style="color: #27c479; text-shadow: 0 0 25px rgba(39, 196, 121, 0.7);">
                  {{ countdown.seconds }}
                </div>
                <div class="text-xs text-white opacity-70 mt-1">SEG</div>
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

// Countdown timer state
const countdown = ref({
  days: '00',
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

// Function to update countdown
const updateCountdown = () => {
  // Set target date to 30 days from now for demo purposes
  // You can change this to your actual event date
  const now = new Date()
  const targetDate = new Date(now.getTime() + (30 * 24 * 60 * 60 * 1000)) // 30 days from now
  
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

.grid-container {
  display: grid;
  grid-template-columns: auto 1fr;
  grid-template-rows: auto auto auto auto auto;
  gap: 16px 24px;
  height: fit-content;
  width: 80%;
  align-items: center;

}

.date-card {
  grid-column: 1;
  grid-row: 1 / -1;
  display: flex;
  align-items: center;
  justify-self: center;

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

.countdown-timer {
  grid-column: 2;
  grid-row: 5;
  display: flex;
  align-items: center;
}
</style>
