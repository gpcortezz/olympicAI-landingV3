<template>
  <div class="relative min-h-screen overflow-auto" style="  background-image: linear-gradient(to right bottom, #8ed6fa, #addcfe, #c8e2ff, #deeaff, #eff2ff, #f4f2ff, #f9f2ff, #fff2ff, #ffe6f6, #ffddcb, #ffe592, #f5fb6f);">
    <!-- Imagen de fondo con opacidad -->
    <div 
      class="absolute inset-0 invert opacity-25 pointer-events-none"
      :style="{ backgroundImage: `url(${backgroundImageSrc})`, backgroundSize: 'cover', backgroundPosition: 'center', backgroundRepeat: 'no-repeat' }"
    ></div>
    
    <!-- Efecto de luz que se propaga desde el trofeo -->
    <div 
      ref="lightEffect"
      class="absolute inset-0 opacity-0 pointer-events-none"
      :style="{ background: lightGradient }"
    ></div>
    
    <!-- Contenido inicial (se oculta cuando aparece el contenido final) -->
    <div 
      ref="initialContent"
      class="absolute inset-0 z-10 text-gray-800 text-center flex flex-col items-center justify-center"
    >
      <h1 class="text-6xl font-bold mb-8 opacity-80">Olympic AI</h1>
      <p class="text-xl opacity-60 max-w-2xl mx-auto px-4">
        Observa cómo el trofeo se transforma automáticamente
      </p>
    </div>

    <!-- Imagen del trofeo con animación automática -->
    <div 
      ref="trophyContainer" 
      class="fixed inset-0 flex items-center justify-center pointer-events-none z-20"
    >
      <img 
        ref="trophyImage"
        :src="trophyImageSrc" 
        alt="Trophy"
        class="w-64 h-64 object-contain filter drop-shadow-2xl"
      />
    </div>

    <!-- Contenido final que aparece después de la animación -->
    <div 
      ref="finalContent"
      class="relative opacity-0 z-30 min-h-screen flex flex-col"
    >
      <!-- Título principal con glassmorphism -->
      <div class="text-center pt-3 pb-2 px-4 lg:px-6">
        <div class="relative max-w-6xl mx-auto">
          <!-- Glassmorphism container -->
          <div class="absolute inset-0 backdrop-blur-sm bg-white/20 rounded-3xl border border-white/30 shadow-2xl"></div>
          
          <!-- Content inside glass container -->
          <div class="relative px-6 py-6 lg:px-10 lg:py-10">
            <h1 class="text-2xl lg:text-5xl font-bold mb-4 lg:mb-6 leading-tight relative">
              <span class="relative inline-block">
                <span class="relative text-transparent bg-clip-text bg-gradient-to-r from-blue-600 via-purple-600 to-red-600">
                  ¡Vive la Revolución de
                </span>
              </span>
              <br>
              <span class="relative inline-block">
                <span class="relative text-transparent bg-clip-text bg-gradient-to-r from-red-500 via-yellow-500 to-orange-500 font-bold">
                  la Inteligencia Artificial!
                </span>
              </span>
            </h1>
            
            <!-- Subtitle -->
            <div class="mb-3 lg:mb-4">
              <p class="text-base lg:text-xl font-semibold mb-3 lg:mb-4">
                Participa en las 
                <span class="text-transparent bg-clip-text bg-gradient-to-r from-blue-600 to-purple-600 font-bold">Olimpiadas de IA</span>
                para estudiantes visionarios
              </p>
              <p class="text-sm lg:text-lg text-gray-700">
                Demuestra tu creatividad, ingenio y pasión por la tecnología.
                <span class="text-transparent bg-clip-text bg-gradient-to-r from-orange-500 to-red-500 font-semibold">
                  ¡Desafía tus límites y sé parte del futuro!
                </span>
              </p>
            </div>
          </div>
        </div>
      </div>

      <!-- Layout principal más compacto -->
      <div class="flex-1 flex items-center justify-center px-3 lg:px-6 py-4">
        <div class="w-full max-w-6xl mx-auto grid grid-cols-1 lg:grid-cols-3 gap-4 lg:gap-8 items-start">
          <!-- Sección izquierda - Tags del evento -->
          <div class="space-y-3 lg:space-y-4 order-2 lg:order-1 flex flex-col h-full">
            <div class="text-left flex-1">
              <h3 class="text-lg lg:text-xl font-bold text-gray-800 mb-3 lg:mb-4 text-center">Información del evento</h3>
              <div class="grid grid-cols-1 gap-2 lg:gap-3">
                <!-- Card: Universidades -->
                <div ref="eventCard1" class="card-animate p-3 lg:p-4 backdrop-blur-sm bg-gradient-to-br from-blue-50/50 to-blue-100/50 rounded-xl border border-blue-200/60 shadow-sm hover:shadow-md hover:from-blue-50/60 hover:to-blue-100/60 transition-all duration-300">
                  <div class="flex items-center space-x-3">
                    <div class="w-9 h-9 lg:w-10 lg:h-10 bg-blue-600 rounded-lg flex items-center justify-center">
                      <svg class="w-4 h-4 lg:w-5 lg:h-5 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 21V5a2 2 0 00-2-2H7a2 2 0 00-2 2v16m14 0h2m-2 0h-5m-9 0H3m2 0h5M9 7h1m-1 4h1m4-4h1m-1 4h1m-5 10v-5a1 1 0 011-1h2a1 1 0 011 1v5m-4 0h4"></path>
                      </svg>
                    </div>
                    <div>
                      <p class="text-blue-800 font-bold text-sm lg:text-base">8+ Universidades</p>
                      <p class="text-blue-600 text-xs lg:text-sm">Participantes</p>
                    </div>
                  </div>
                </div>

                <!-- Card: Categorías -->
                <div ref="eventCard2" class="card-animate p-3 lg:p-4 backdrop-blur-sm bg-gradient-to-br from-yellow-50/50 to-yellow-100/50 rounded-xl border border-yellow-200/60 shadow-sm hover:shadow-md hover:from-yellow-50/60 hover:to-yellow-100/60 transition-all duration-300">
                  <div class="flex items-center space-x-3">
                    <div class="w-9 h-9 lg:w-10 lg:h-10 bg-yellow-500 rounded-lg flex items-center justify-center">
                      <svg class="w-4 h-4 lg:w-5 lg:h-5 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4M7.835 4.697a3.42 3.42 0 001.946-.806 3.42 3.42 0 014.438 0 3.42 3.42 0 001.946.806 3.42 3.42 0 013.138 3.138 3.42 3.42 0 00.806 1.946 3.42 3.42 0 010 4.438 3.42 3.42 0 00-.806 1.946 3.42 3.42 0 01-3.138 3.138 3.42 3.42 0 00-1.946.806 3.42 3.42 0 01-4.438 0 3.42 3.42 0 00-1.946-.806 3.42 3.42 0 01-3.138-3.138 3.42 3.42 0 00-.806-1.946 3.42 3.42 0 010-4.438 3.42 3.42 0 00.806-1.946 3.42 3.42 0 713.138-3.138z"></path>
                      </svg>
                    </div>
                    <div>
                      <p class="text-yellow-800 font-bold text-sm lg:text-base">5 Categorías</p>
                      <p class="text-yellow-600 text-xs lg:text-sm">De competencia</p>
                    </div>
                  </div>
                </div>

                <!-- Card: Fecha -->
                <div ref="eventCard3" class="card-animate p-3 lg:p-4 backdrop-blur-sm bg-gradient-to-br from-green-50/50 to-green-100/50 rounded-xl border border-green-200/60 shadow-sm hover:shadow-md hover:from-green-50/60 hover:to-green-100/60 transition-all duration-300">
                  <div class="flex items-center space-x-3">
                    <div class="w-9 h-9 lg:w-10 lg:h-10 bg-green-600 rounded-lg flex items-center justify-center">
                      <svg class="w-4 h-4 lg:w-5 lg:h-5 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z"></path>
                      </svg>
                    </div>
                    <div>
                      <p class="text-green-800 font-bold text-sm lg:text-base">Agosto 2025</p>
                      <p class="text-green-600 text-xs lg:text-sm">Próximamente</p>
                    </div>
                  </div>
                </div>

                <!-- Card: Ubicación -->
                <div ref="eventCard4" class="card-animate p-3 lg:p-4 backdrop-blur-sm bg-gradient-to-br from-red-50/50 to-red-100/50 rounded-xl border border-red-200/60 shadow-sm hover:shadow-md hover:from-red-50/60 hover:to-red-100/60 transition-all duration-300">
                  <div class="flex items-center space-x-4">
                    <div class="w-10 h-10 lg:w-12 lg:h-12 bg-red-600 rounded-lg flex items-center justify-center">
                      <svg class="w-5 h-5 lg:w-6 lg:h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"></path>
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"></path>
                      </svg>
                    </div>
                    <div>
                      <p class="text-red-800 font-bold text-base lg:text-lg">Baja California</p>
                      <p class="text-red-600 text-sm lg:text-base">México</p>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <!-- Sección central (trofeo) -->
          <div class="flex items-center justify-center order-1 lg:order-2 mb-3 lg:mb-0">
            <!-- El trofeo aparecerá aquí después de la animación -->
            <div class="w-28 h-28 lg:w-56 lg:h-56"></div>
          </div>

          <!-- Sección derecha - Tecnologías objetivo -->
          <div class="space-y-3 lg:space-y-4 order-3 flex flex-col h-full">
            <div class="text-left flex-1">
              <h3 class="text-lg lg:text-xl font-bold text-gray-800 mb-3 lg:mb-4 text-center">Tecnologías objetivo</h3>
              <div class="grid grid-cols-2 gap-2 lg:gap-3">
                <!-- Tech Card: LLM -->
                <div ref="techCard1" class="card-animate p-2 lg:p-3 backdrop-blur-sm bg-gradient-to-br from-blue-50/50 to-blue-100/50 rounded-lg border border-blue-200/60 shadow-sm hover:shadow-md hover:from-blue-50/60 hover:to-blue-100/60 transition-all duration-300">
                  <div class="text-center">
                    <div class="w-7 h-7 lg:w-8 lg:h-8 bg-blue-600 rounded-md flex items-center justify-center mx-auto mb-1">
                      <svg class="w-3 h-3 lg:w-4 lg:h-4 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9.663 17h4.673M12 3v1m6.364 1.636l-.707.707M21 12h-1M4 12H3m3.343-5.657l-.707-.707m2.828 9.9a5 5 0 117.072 0l-.548.547A3.374 3.374 0 0014 18.469V19a2 2 0 11-4 0v-.531c0-.895-.356-1.754-.988-2.386l-.548-.547z"></path>
                      </svg>
                    </div>
                    <p class="text-blue-800 font-semibold text-xs lg:text-sm">LLM</p>
                  </div>
                </div>

                <!-- Tech Card: Agentic AI -->
                <div ref="techCard2" class="card-animate p-2 lg:p-3 backdrop-blur-sm bg-gradient-to-br from-yellow-50/50 to-yellow-100/50 rounded-lg border border-yellow-200/60 shadow-sm hover:shadow-md hover:from-yellow-50/60 hover:to-yellow-100/60 transition-all duration-300">
                  <div class="text-center">
                    <div class="w-7 h-7 lg:w-8 lg:h-8 bg-yellow-500 rounded-md flex items-center justify-center mx-auto mb-1">
                      <svg class="w-3 h-3 lg:w-4 lg:h-4 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19.428 15.428a2 2 0 00-1.022-.547l-2.387-.477a6 6 0 00-3.86.517l-.318.158a6 6 0 01-3.86.517L6.05 15.21a2 2 0 00-1.806.547M8 4h8l-1 1v5.172a2 2 0 00.586 1.414l5 5c1.26 1.26.367 3.414-1.415 3.414H4.828c-1.782 0-2.674-2.154-1.414-3.414l5-5A2 2 0 009 10.172V5L8 4z"></path>
                      </svg>
                    </div>
                    <p class="text-yellow-800 font-semibold text-xs lg:text-sm">Agentic AI</p>
                  </div>
                </div>

                <!-- Tech Card: SMA -->
                <div ref="techCard3" class="card-animate p-2 lg:p-3 backdrop-blur-sm bg-gradient-to-br from-green-50/50 to-green-100/50 rounded-lg border border-green-200/60 shadow-sm hover:shadow-md hover:from-green-50/60 hover:to-green-100/60 transition-all duration-300">
                  <div class="text-center">
                    <div class="w-7 h-7 lg:w-8 lg:h-8 bg-green-600 rounded-md flex items-center justify-center mx-auto mb-1">
                      <svg class="w-3 h-3 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 20h5v-2a3 3 0 00-5.356-1.857M17 20H7m10 0v-2c0-.656-.126-1.283-.356-1.857M7 20H2v-2a3 3 0 015.356-1.857M7 20v-2c0-.656.126-1.283.356-1.857m0 0a5.002 5.002 0 019.288 0M15 7a3 3 0 11-6 0 3 3 0 016 0zm6 3a2 2 0 11-4 0 2 2 0 014 0zM7 10a2 2 0 11-4 0 2 2 0 014 0z"></path>
                      </svg>
                    </div>
                    <p class="text-green-800 font-semibold text-xs">SMA</p>
                  </div>
                </div>

                <!-- Tech Card: RAG -->
                <div ref="techCard4" class="card-animate p-2 lg:p-3 backdrop-blur-sm bg-gradient-to-br from-red-50/50 to-red-100/50 rounded-lg border border-red-200/60 shadow-sm hover:shadow-md hover:from-red-50/60 hover:to-red-100/60 transition-all duration-300">
                  <div class="text-center">
                    <div class="w-7 h-7 lg:w-8 lg:h-8 bg-red-600 rounded-md flex items-center justify-center mx-auto mb-1">
                      <svg class="w-3 h-3 lg:w-4 lg:h-4 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"></path>
                      </svg>
                    </div>
                    <p class="text-red-800 font-semibold text-xs lg:text-sm">RAG</p>
                  </div>
                </div>

                <!-- Tech Card: VibeCoding (spans 2 columns) -->
                <div ref="techCard5" class="card-animate p-2 lg:p-3 backdrop-blur-sm bg-gradient-to-br from-purple-50/50 to-purple-100/50 rounded-lg border border-purple-200/60 shadow-sm hover:shadow-md hover:from-purple-50/60 hover:to-purple-100/60 transition-all duration-300 col-span-2">
                  <div class="text-center">
                    <div class="w-7 h-7 lg:w-8 lg:h-8 bg-purple-600 rounded-md flex items-center justify-center mx-auto mb-1">
                      <svg class="w-3 h-3 lg:w-4 lg:h-4 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 20l4-16m4 4l4 4-4 4M6 16l-4-4 4-4"></path>
                      </svg>
                    </div>
                    <p class="text-purple-800 font-semibold text-xs lg:text-sm">VibeCoding</p>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, computed } from 'vue'
import { gsap } from 'gsap'

// Referencias a los elementos
const trophyContainer = ref(null)
const trophyImage = ref(null)
const initialContent = ref(null)
const finalContent = ref(null)
const lightEffect = ref(null)

// Referencias a las cartas de eventos
const eventCard1 = ref(null)
const eventCard2 = ref(null)
const eventCard3 = ref(null)
const eventCard4 = ref(null)

// Referencias a las cartas de tecnologías
const techCard1 = ref(null)
const techCard2 = ref(null)
const techCard3 = ref(null)
const techCard4 = ref(null)
const techCard5 = ref(null)

// Importar las imágenes
const trophyImageSrc = new URL('../assets/img/trophy-ex.png', import.meta.url).href
const backgroundImageSrc = new URL('../assets/img/background.png', import.meta.url).href

// Gradiente de luz responsive
const lightGradient = computed(() => {
  const centerY = window.innerWidth >= 1024 ? '65%' : '60%'
  return `radial-gradient(circle at 50% ${centerY}, rgba(255, 235, 180, 0.25) 0%, rgba(255, 235, 180, 0.15) 30%, rgba(255, 235, 180, 0.08) 50%, rgba(255, 235, 180, 0.03) 70%, transparent 85%)`
})

onMounted(() => {
  // Obtener el tamaño de la ventana para ajustar la animación
  const isLargeScreen = window.innerWidth >= 1024
  const finalScale = isLargeScreen ? 3 : 2
  const finalY = isLargeScreen ? "15vh" : "10vh"

  // Configurar posición inicial del trofeo
  gsap.set(trophyImage.value, {
    scale: 1.5,
    y: 0,
    x: 0,
    rotation: 0,
    filter: "brightness(1) contrast(1) drop-shadow(0 0 10px rgba(255, 215, 0, 0.3))"
  })

  // Ocultar el contenido final y efecto de luz inicialmente
  gsap.set(finalContent.value, {
    opacity: 0
  })
  
  gsap.set(lightEffect.value, {
    opacity: 0
  })

  // Configurar posición inicial de las cartas (tipo Framer Motion)
  const allCards = [
    eventCard1.value, eventCard2.value, eventCard3.value, eventCard4.value,
    techCard1.value, techCard2.value, techCard3.value, techCard4.value, techCard5.value
  ]
  
  gsap.set(allCards, {
    y: -50,
    opacity: 0,
    scale: 0.9
  })

  // Crear timeline para la animación
  const tl = gsap.timeline({ 
    delay: 0.5
  })

  // Fase 1: Mover y agrandar el trofeo (2 segundos)
  tl.to(trophyImage.value, {
    y: finalY,
    scale: finalScale,
    filter: "brightness(1.1) contrast(1.1) drop-shadow(0 0 40px rgba(255, 215, 0, 1))",
    ease: "power2.inOut",
    duration: 2
  })
  // Fase 2: Comenzar el efecto de luz gradual mientras el trofeo llega
  .to(lightEffect.value, {
    opacity: 0.3,
    duration: 1,
    ease: "power1.out"
  }, "-=1")
  // Fase 3: Ocultar contenido inicial y mostrar contenido final
  .to(initialContent.value, {
    opacity: 0,
    duration: 0.5,
    ease: "power2.out"
  }, "-=0.5")
  .to(finalContent.value, {
    opacity: 1,
    duration: 1,
    ease: "power2.out"
  }, "-=0.5")
  // Fase 4: Intensificar gradualmente el efecto de luz
  .to(lightEffect.value, {
    opacity: 1,
    duration: 2,
    ease: "power1.inOut"
  }, "-=1")
  // Fase 5: Animar cartas de evento (justo cuando el trofeo termina de crecer)
  .to([eventCard1.value, eventCard2.value, eventCard3.value, eventCard4.value], {
    y: 0,
    opacity: 1,
    scale: 1,
    duration: 0.6,
    ease: "back.out(1.4)",
    stagger: 0.1
  }, 2.2)
  // Fase 6: Animar cartas de tecnología (inmediatamente después)
  .to([techCard1.value, techCard2.value, techCard3.value, techCard4.value, techCard5.value], {
    y: 0,
    opacity: 1,
    scale: 1,
    duration: 0.6,
    ease: "back.out(1.4)",
    stagger: 0.08
  }, 2.4)
})
</script>

<style scoped>
/* Asegurar que el contenedor tenga altura mínima de viewport */
.min-h-screen {
  min-height: 100vh;
}

/* Suavizar las transiciones */
html {
  scroll-behavior: smooth;
}

/* Optimizar el rendimiento de las animaciones */
img {
  will-change: transform, filter;
}

/* Optimizar animaciones de cartas */
.card-animate {
  will-change: transform, opacity;
}
</style>
