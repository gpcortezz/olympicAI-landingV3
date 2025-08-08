<template>
  <div class="landing min-h-screen relative page-bg">
    <div id="light"></div>

    <main class="relative z-10 py-16 md:py-24 lg:py-28">
      <div class="container">
        <!-- Left: Hero -->
        <section class="hero">
          <img :src="newLogoImg" alt="Olimpiadas Universitarias de IA" class="logo logo-appear" />
          <h1 class="title title-appear text-4xl md:text-5xl lg:text-6xl leading-tight">
            <span>OLIMPIADAS </span>
            <span class="highlight">UNIVERSITARIAS</span><br />
            <span>DE </span> <span class="highlight">IA</span> <span>2025</span>
          </h1>
          <p class="subtitle subtitle-appear text-lg md:text-xl lg:text-2xl leading-relaxed max-w-2xl">
            Compite con los mejores estudiantes en desafíos de IA: agentes, multi-agentes, RAG y vibe coding.
          </p>
          <div v-if="showCountdown" :class="['badge badge-appear', { 'fade-out': fadeOutBadge }]">PRÓXIMAMENTE</div>
        </section>

        <!-- Right: Countdown -->
        <section aria-label="Cuenta regresiva" class="flex flex-col items-center justify-center">
          <div v-if="showCountdown" :class="['countdown transition-all', { 'fade-out': fadeOutCountdown }]">
            <div class="time-card">
              <div class="value font-extrabold">{{ countdown.days }}</div>
              <div class="label">Días</div>
            </div>
            <div class="time-card">
              <div class="value font-extrabold">{{ countdown.hours }}</div>
              <div class="label">Horas</div>
            </div>
            <div class="time-card">
              <div class="value font-extrabold">{{ countdown.minutes }}</div>
              <div class="label">Min</div>
            </div>
            <div class="time-card">
              <div class="value font-extrabold">{{ countdown.seconds }}</div>
              <div class="label label--seconds">Seg</div>
            </div>
          </div>
          <div v-else class="flex items-center justify-center">
            <a class="cta-button cta-appear" href="" target="_blank" rel="noopener noreferrer">
              <span>Visita el sitio oficial</span>
              <span aria-hidden>→</span>
            </a>
          </div>
        </section>
      </div>
    </main>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import newLogoImg from '../assets/img/newLogo.png'
import '../newLanding.css'
import { tsParticles } from "https://cdn.jsdelivr.net/npm/@tsparticles/engine@3.0.3/+esm";
import { loadAll } from "https://cdn.jsdelivr.net/npm/@tsparticles/all@3.0.3/+esm";

const eventDateTime = '2025-08-30T15:52:20'

const countdown = ref({ days: '10', hours: '00', minutes: '00', seconds: '00' })
const showCountdown = ref(true)
const fadeOutCountdown = ref(false)
const fadeOutBadge = ref(false)
let fireworksLaunched = false
let timer = null

const updateCountdown = () => {
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
    fireworksLaunched = false
  } else {
    countdown.value = { days: '00', hours: '00', minutes: '00', seconds: '00' }
    if (!fireworksLaunched) {
      fireworksLaunched = true
      fadeOutCountdown.value = true
      fadeOutBadge.value = true
      setTimeout(() => { showCountdown.value = false }, 600)
      createFirework()
      const steps = Array.from({ length: 40 }, (_, i) => i * 500)
      steps.forEach((t) => setTimeout(createFirework, t))
      setTimeout(() => {
        document.querySelectorAll('.firework-particle').forEach((fw) => fw.remove())
      }, 20000)
    }
  }
}

const createFirework = () => {
  const colors = ['#27c479', '#4ade80', '#1b7069', '#34d4a7', '#ffffff']
  const container = document.body
  const x = Math.random() * window.innerWidth
  const y = Math.random() * (window.innerHeight / 2) + 100
  const particleCount = 20 + Math.random() * 10

  for (let i = 0; i < particleCount; i++) {
    const particle = document.createElement('div')
    particle.className = 'firework-particle'
    particle.style.cssText = `left:${x}px;top:${y}px;width:4px;height:4px;background:${colors[Math.floor(Math.random()*colors.length)]};`
    container.appendChild(particle)

    const angle = (Math.PI * 2 * i) / particleCount
    const velocity = 100 + Math.random() * 100
    const life = 3 + Math.random() * 3
    const dx = Math.cos(angle) * velocity
    const dy = Math.sin(angle) * velocity

    particle.animate([
      { transform: 'translate(0, 0) scale(1)', opacity: 1 },
      { transform: `translate(${dx}px, ${dy + 100}px) scale(0)`, opacity: 0 }
    ], { duration: life * 1000, easing: 'cubic-bezier(0.25, 0.46, 0.45, 0.94)' }).onfinish = () => particle.remove()
  }
}

onMounted(async () => {
  // Inicializa lógica como antes: si ya pasó, muestra el botón de inmediato
  const nowInit = new Date()
  const targetInit = new Date(eventDateTime)
  const diffInit = targetInit.getTime() - nowInit.getTime()
  if (diffInit <= 0) {
    showCountdown.value = false
    // Lanza fuegos artificiales si el evento ya pasó al cargar
    createFirework()
    const stepsInit = Array.from({ length: 40 }, (_, i) => i * 500)
    stepsInit.forEach((t) => setTimeout(createFirework, t))
    setTimeout(() => {
      document.querySelectorAll('.firework-particle').forEach((fw) => fw.remove())
    }, 20000)
  } else {
    updateCountdown()
    timer = setInterval(updateCountdown, 1000)
  }

  await loadAll(tsParticles)
  await tsParticles.addPreset('lightdark', {
    fullScreen: { enable: true, zIndex: 1 },
    particles: {
      links: { enable: true },
      move: { enable: true },
      number: { value: 100, density: { enable: true, area: 150 } },
      opacity: { value: { min: 0.005, max: 0.005 } },
      shape: { type: 'text', options: { text: { value: ['*'], weight: '1000', font: 'Arial' } } },
      size: { value: { min: 1, max: 1 } }
    }
  })

  await tsParticles.load({
    id: 'light',
    options: {
      preset: 'lightdark',
      particles: {
        color: { value: ['#27c479', '#4ade80', '#1b7069'] },
        links: { color: '#27c479', opacity: 0.03, width: 2 },
        size: { value: { min: 7, max: 7 } },
        opacity: { value: { min: 0.3, max: 0.55 } }
      }
    }
  })
})

onUnmounted(() => { if (timer) clearInterval(timer) })
</script>