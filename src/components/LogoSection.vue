<template>
  <section class="relative overflow-hidden pt-20 pb-16 md:pt-28 md:pb-20 px-4">
    <div
      v-if="heroBgUrl"
      class="absolute inset-0 bg-cover bg-center bg-no-repeat opacity-30"
      :style="{ backgroundImage: `url(${heroBgUrl})` }"
    >
      <div class="absolute inset-0 bg-gradient-to-b from-[#0F0F11] via-[#0F0F11]/85 to-[#0F0F11]"></div>
    </div>

    <div class="hero-orb orb-1 w-[420px] h-[420px] -top-20 -right-20 md:w-[600px] md:h-[600px]"></div>
    <div class="hero-orb orb-2 w-[380px] h-[380px] -bottom-20 -left-20 md:w-[500px] md:h-[500px]"></div>
    <div class="hero-orb orb-3 w-[320px] h-[320px] top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 hidden md:block"></div>

    <div
      class="absolute inset-0 opacity-[0.04] pointer-events-none"
      style="background-image: linear-gradient(rgba(255,255,255,0.5) 1px, transparent 1px), linear-gradient(90deg, rgba(255,255,255,0.5) 1px, transparent 1px); background-size: 60px 60px;"
    ></div>

    <div class="relative max-w-4xl mx-auto text-center">
      <div class="inline-flex items-center gap-2 px-4 py-2 rounded-full glass-light mb-6 animate-fade-in-up opacity-0" style="animation-delay: 0.05s">
        <span class="relative flex h-2 w-2">
          <span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-green-400 opacity-75"></span>
          <span class="relative inline-flex rounded-full h-2 w-2 bg-green-500"></span>
        </span>
        <span class="text-xs font-medium text-gray-300 tracking-wide">Available for new projects</span>
      </div>

      <div class="flex justify-center mb-8 animate-fade-in-up opacity-0" style="animation-delay: 0.15s">
        <div class="relative group">
          <div class="absolute inset-0 rounded-full bg-primary opacity-30 blur-2xl group-hover:opacity-50 transition-opacity duration-500"></div>
          <div class="relative inline-flex items-center justify-center w-32 h-32 md:w-40 md:h-40 rounded-full glass overflow-hidden ring-2 ring-primary/30 ring-offset-2 ring-offset-[#0F0F11]">
            <img
              :src="logoUrl"
              :alt="`${name} logo`"
              class="w-20 h-20 md:w-24 md:h-24 object-contain transition-transform duration-500 group-hover:scale-110"
            />
          </div>
        </div>
      </div>

      <h1 class="text-4xl sm:text-5xl md:text-6xl lg:text-7xl font-bold tracking-tight mb-5 animate-fade-in-up opacity-0" style="animation-delay: 0.25s">
        <span class="text-white">{{ name }}</span>
      </h1>

      <p class="text-base md:text-lg text-gray-400 max-w-2xl mx-auto mb-10 leading-relaxed animate-fade-in-up opacity-0" style="animation-delay: 0.35s">
        {{ description }}
      </p>

      <div class="flex flex-col sm:flex-row items-center justify-center gap-3 mb-12 animate-fade-in-up opacity-0" style="animation-delay: 0.45s">
        <a
          href="#projects"
          @click.prevent="scrollToProjects"
          class="group inline-flex items-center gap-2 px-6 py-3 rounded-xl bg-primary text-white text-sm font-semibold shadow-lg shadow-primary/30 hover:bg-primary-light hover:shadow-primary/50 transition-all duration-300 hover:scale-105"
        >
          View Projects
          <svg class="w-4 h-4 transition-transform duration-300 group-hover:translate-x-1" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
            <path stroke-linecap="round" stroke-linejoin="round" d="M13 7l5 5m0 0l-5 5m5-5H6" />
          </svg>
        </a>
        <a
          href="#contact"
          @click.prevent="scrollToContact"
          class="group inline-flex items-center gap-2 px-6 py-3 rounded-xl glass text-white text-sm font-semibold hover:bg-card-light transition-all duration-300"
        >
          Get in Touch
          <svg class="w-4 h-4 transition-transform duration-300 group-hover:translate-x-1" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
            <path stroke-linecap="round" stroke-linejoin="round" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
          </svg>
        </a>
      </div>

      <div class="flex flex-wrap items-center justify-center gap-x-8 gap-y-4 text-xs uppercase tracking-wider text-gray-500 animate-fade-in-up opacity-0" style="animation-delay: 0.55s">
        <div class="flex items-center gap-2">
          <span class="text-2xl md:text-3xl font-bold gradient-text">3+</span>
          <span class="text-gray-500">Years</span>
        </div>
        <span class="hidden sm:inline w-px h-8 bg-zinc-700"></span>
        <div class="flex items-center gap-2">
          <span class="text-2xl md:text-3xl font-bold gradient-text">20+</span>
          <span class="text-gray-500">Projects</span>
        </div>
        <span class="hidden sm:inline w-px h-8 bg-zinc-700"></span>
        <div class="flex items-center gap-2">
          <span class="text-2xl md:text-3xl font-bold gradient-text">15+</span>
          <span class="text-gray-500">Clients</span>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { siteConfig } from '../config/config.js'

const { name, description, logoUrl, heroBgUrl } = siteConfig

function scrollToProjects() {
  document.getElementById('projects')?.scrollIntoView({ behavior: 'smooth' })
}

function scrollToContact() {
  document.getElementById('contact')?.scrollIntoView({ behavior: 'smooth' })
}
</script>
