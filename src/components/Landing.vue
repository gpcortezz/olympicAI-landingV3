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
    
    <!-- Main content with two containers -->
    <main class="relative z-10 px-6 flex-1 flex items-center justify-center">
      <div class="max-w-screen-xl mx-auto w-full h-full flex items-center justify-center">
        
        <!-- Content Container -->
        <div class="content-container">
          <!-- Logo - arriba de los textos -->
          <div class="logo-container">
            <img :src="newLogoImg" alt="Logo" class="logo-image" />
          </div>

          <!-- Main title -->
          <div class="main-title">
            <h1 class="text-5xl lg:text-6xl xl:text-7xl font-extrabold leading-tight">
              <span style="color: #ffffff; text-shadow: 0 0 20px rgba(255, 255, 255, 0.3);">OLIMPIADAS </span>
              <span style="color: #27c479; text-shadow: 0 0 30px rgba(39, 196, 121, 0.8);">UNIVERSITARIAS</span><br>
              <span style="color: #ffffff; text-shadow: 0 0 20px rgba(255, 255, 255, 0.3);">DE </span>
              <span style="color: #27c479; text-shadow: 0 0 30px rgba(39, 196, 121, 0.8);">IA </span>
              <span style="color: #ffffff; text-shadow: 0 0 20px rgba(255, 255, 255, 0.3);">2025</span>
            </h1>
          </div>

          <!-- Description -->
          <div class="description">
            <p class="text-xl lg:text-2xl leading-relaxed max-w-3xl" style="color: #ffffff; opacity: 0.9; text-shadow: 0 0 15px rgba(255, 255, 255, 0.1);">
              Compite con los mejores estudiantes universitarios en desafíos de 
              inteligencia artificial. Demuestra tus habilidades en machine learning,
              algoritmos y soluciones innovadoras.
            </p>
          </div>
        </div>

        <!-- Globe positioned at bottom -->
        <div class="globe-container">
          <canvas 
            ref="el"
            @pointerdown="onPointerDown"
            @pointerup="onPointerUp"
            @pointerout="onPointerOut"
            @mousemove="onMouseMove"
            @touchmove="onTouchMove"
            :style="{ 
              width: '100%', 
              height: '100%', 
              cursor: pointerInteracting ? 'grabbing' : 'grab',
              contain: 'layout paint size',
              opacity: 0,
              transition: 'opacity 1s ease'
            }"
          ></canvas>
        </div>
        <!-- Countdown Container -->
        <div class="countdown-wrapper">
          <div v-if="showCountdown" class="countdown-container">
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
          <div v-else class="registration-container">
            <div class="registration-button-container">
              <button class="registration-button">
                <a href="" target="_blank" class="registration-link">
                  <span class="button-text">Visita el sitio oficial</span>
                  <span class="button-icon">→</span>
                </a>
              </button>
            </div>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted, reactive } from 'vue'
import backgroundTextureImg from '../assets/img/background-no-texture.png'
import newLogoImg from '../assets/img/newLogo.png'
import '../landingCss.css'
import { tsParticles } from "https://cdn.jsdelivr.net/npm/@tsparticles/engine@3.0.3/+esm";
import { loadAll } from "https://cdn.jsdelivr.net/npm/@tsparticles/all@3.0.3/+esm";
import createGlobe from 'cobe';

const el = ref();
const phi = ref(0);

// Draggable interaction state
const pointerInteracting = ref(null);
const pointerInteractionMovement = ref(0);

// Spring animation state
const springState = reactive({
  r: 0,
  velocity: 0
});

// Spring configuration
const springConfig = {
  mass: 1,
  tension: 280,
  friction: 40,
  precision: 0.001,
};

// Spring animation function
const updateSpring = () => {
  const target = springState.r;
  const current = phi.value;
  const delta = target - current;
  
  // Simple spring physics
  const spring = springConfig.tension / 1000;
  const damping = springConfig.friction / 1000;
  
  springState.velocity += delta * spring;
  springState.velocity *= (1 - damping);
  
  phi.value += springState.velocity;
  
  // Continue animation
  requestAnimationFrame(updateSpring);
};

// Pointer event handlers
const onPointerDown = (e) => {
  pointerInteracting.value = e.clientX - pointerInteractionMovement.value;
};

const onPointerUp = () => {
  pointerInteracting.value = null;
};

const onPointerOut = () => {
  pointerInteracting.value = null;
};

const onMouseMove = (e) => {
  if (pointerInteracting.value !== null) {
    const delta = e.clientX - pointerInteracting.value;
    pointerInteractionMovement.value = delta;
    springState.r = delta / 200;
  }
};

const onTouchMove = (e) => {
  if (pointerInteracting.value !== null && e.touches[0]) {
    const delta = e.touches[0].clientX - pointerInteracting.value;
    pointerInteractionMovement.value = delta;
    springState.r = delta / 100;
  }
};

// FECHA Y HORA DEL EVENTO (ajusta aquí)
const eventDateTime = '2025-08-30T12:00:00'

// Countdown timer state
const countdown = ref({
  days: '10',
  hours: '00',
  minutes: '00',
  seconds: '00'
})

// Estado para los fuegos artificiales
const showFireworks = ref(false)
const showCountdown = ref(true)
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
  
  // Agregar transición de salida al countdown
  const countdownContainer = document.querySelector('.countdown-container')
  if (countdownContainer) {
    countdownContainer.classList.add('fade-out')
  }
  
  // Ocultar countdown después de la transición
  setTimeout(() => {
    showCountdown.value = false
  }, 600) // 600ms para que coincida con la duración de la transición CSS

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

onMounted(() => {
  // Get responsive dimensions with scaling
  const getGlobeDimensions = () => {
    let width = 0;
    if (el.value) {
      width = el.value.offsetWidth;
    }
    
    if (window.innerWidth <= 480) {
      return { width: 400 * 2, height: 200 * 2, scale: 1.5 };
    } else if (window.innerWidth <= 768) {
      return { width: 500 * 2, height: 250 * 2, scale: 1.8 };
    } else if (window.innerWidth <= 1200) {
      return { width: 600 * 2, height: 300 * 2, scale: 2.2 };
    } else {
      return { width: 800 * 2, height: 400 * 2, scale: 2.5 };
    }
  };

  const onResize = () => {
    const dimensions = getGlobeDimensions();
    if (globeInstance) {
      globeInstance.destroy();
    }
    createGlobeInstance(dimensions);
  };

  let globeInstance = null;

  const createGlobeInstance = (dimensions) => {
    globeInstance = createGlobe(el.value, {
      devicePixelRatio: 2,
      width: dimensions.width,
      height: dimensions.height,
      phi: 0,
      theta: 0.3,
      dark: 1,
      diffuse: 3,
      mapSamples: 16000,
      mapBrightness: 1.2,
      baseColor: [0.15, 0.77, 0.47],
      markerColor: [0.29, 0.83, 0.65],
      glowColor: [0.21, 0.44, 0.41],
      markers: [
        { location: [32.5247, -117.0149], size: 0.1 },
      ],
      scale: dimensions.scale,
      offset: [0, dimensions.height * 0.6],
      onRender: (state) => {
        state.phi = phi.value;
        state.width = dimensions.width;
        state.height = dimensions.height;
      },
    });
  };

  // Initial setup
  const dimensions = getGlobeDimensions();
  createGlobeInstance(dimensions);
  
  // Start spring animation
  updateSpring();
  
  // Show canvas with fade-in effect
  setTimeout(() => {
    if (el.value) {
      el.value.style.opacity = '1';
    }
  }, 100);

  // Add resize listener
  window.addEventListener('resize', onResize);
  
  // Cleanup on unmount
  onUnmounted(() => {
    if (globeInstance) {
      globeInstance.destroy();
    }
    window.removeEventListener('resize', onResize);
  });
});
</script>