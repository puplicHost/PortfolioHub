<template>
  <article
    class="group relative bg-card rounded-2xl overflow-hidden border border-zinc-800/60 card-hover p-4 md:p-6 flex flex-col"
    ref="cardRef"
  >
    <div
      class="absolute top-0 left-0 right-0 h-32 opacity-60 group-hover:opacity-100 transition-opacity duration-500 pointer-events-none"
      :class="bgGradientClass"
    ></div>

    <div class="absolute top-0 right-0 w-48 h-48 rounded-full blur-3xl opacity-20 group-hover:opacity-40 transition-opacity duration-500 pointer-events-none"
      :class="bgBlurClass"
    ></div>

    <div class="relative flex items-start justify-between gap-2 md:gap-3 mb-3 md:mb-4">
      <div class="inline-flex items-center justify-center w-10 h-10 md:w-12 md:h-12 rounded-xl bg-card-light border border-zinc-800/60 group-hover:border-primary/40 transition-colors duration-300 shrink-0">
        <svg class="w-5 h-5 md:w-6 md:h-6 text-primary" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5">
          <path stroke-linecap="round" stroke-linejoin="round" :d="categoryIcon" />
        </svg>
      </div>

      <span
        class="inline-flex items-center gap-1.5 px-2 md:px-2.5 py-0.5 md:py-1 rounded-full text-[9px] md:text-[10px] font-semibold uppercase tracking-wider backdrop-blur-md"
        :class="badgeClass"
      >
        <span class="w-1.5 h-1.5 rounded-full" :class="badgeDotClass"></span>
        {{ badgeLabel }}
      </span>
    </div>

    <div class="relative flex-1 space-y-1.5 md:space-y-2 mb-4 md:mb-5">
      <h3 class="text-sm md:text-xl font-semibold text-white group-hover:text-primary-light transition-colors duration-300 line-clamp-1">
        {{ project.title }}
      </h3>
      <p class="text-xs md:text-sm text-gray-400 leading-relaxed line-clamp-2 md:line-clamp-3">
        {{ project.description }}
      </p>
    </div>

    <a
      :href="project.url"
      target="_blank"
      rel="noopener noreferrer"
      :aria-label="`Visit ${project.title} website`"
      class="relative inline-flex items-center justify-center gap-1.5 md:gap-2 px-3 md:px-4 py-2 md:py-2.5 rounded-xl text-xs md:text-sm font-semibold transition-all duration-300
             bg-zinc-800/60 text-gray-300 border border-zinc-700/60
             hover:bg-primary hover:text-white hover:border-primary hover:shadow-lg hover:shadow-primary/30 hover:-translate-y-0.5"
    >
      <span class="hidden sm:inline">Visit Project</span>
      <span class="sm:hidden">Visit</span>
      <svg class="w-3 h-3 md:w-3.5 md:h-3.5 transition-transform duration-300 group-hover:translate-x-0.5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
        <path stroke-linecap="round" stroke-linejoin="round" d="M13.5 6H5.25A2.25 2.25 0 003 8.25v10.5A2.25 2.25 0 005.25 21h10.5A2.25 2.25 0 0018 18.75V10.5m-10.5 6L21 3m0 0h-5.25M21 3v5.25" />
      </svg>
    </a>
  </article>
</template>

<script setup>
import { computed, ref, onMounted } from 'vue'

const props = defineProps({
  project: {
    type: Object,
    required: true,
  },
})

const badgeLabels = {
  portfolios: 'Portfolio',
  business: 'Business',
  ecommerce: 'E-Commerce',
}

const badgeStyles = {
  portfolios: {
    bg: 'bg-purple-500/15 text-purple-300 border border-purple-500/20',
    dot: 'bg-purple-400',
    gradient: 'bg-gradient-to-br from-purple-500/10 via-transparent to-transparent',
    blur: 'bg-purple-500',
  },
  business: {
    bg: 'bg-blue-500/15 text-blue-300 border border-blue-500/20',
    dot: 'bg-blue-400',
    gradient: 'bg-gradient-to-br from-blue-500/10 via-transparent to-transparent',
    blur: 'bg-blue-500',
  },
  ecommerce: {
    bg: 'bg-emerald-500/15 text-emerald-300 border border-emerald-500/20',
    dot: 'bg-emerald-400',
    gradient: 'bg-gradient-to-br from-emerald-500/10 via-transparent to-transparent',
    blur: 'bg-emerald-500',
  },
}

const categoryIcons = {
  portfolios: 'M9.75 17L9 20l-1 1h8l-1-1-.75-3M3 13h18M5 17h14a2 2 0 002-2V5a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z',
  business: 'M19 21V5a2 2 0 00-2-2H7a2 2 0 00-2 2v16m14 0h2m-2 0h-5m-9 0H3m2 0h5M9 7h1m-1 4h1m4-4h1m-1 4h1m-5 10v-5a1 1 0 011-1h2a1 1 0 011 1v5m-4 0h4',
  ecommerce: 'M3 3h2l.4 2M7 13h10l4-8H5.4M7 13L5.4 5M7 13l-2.293 2.293c-.63.63-.184 1.707.707 1.707H17m0 0a2 2 0 100 4 2 2 0 000-4zm-8 2a2 2 0 11-4 0 2 2 0 014 0z',
}

const badgeLabel = computed(() => badgeLabels[props.project.category] || props.project.category)
const badgeClass = computed(() => badgeStyles[props.project.category]?.bg || 'bg-zinc-700/50 text-gray-300 border border-zinc-600')
const badgeDotClass = computed(() => badgeStyles[props.project.category]?.dot || 'bg-gray-400')
const bgGradientClass = computed(() => badgeStyles[props.project.category]?.gradient || 'bg-gradient-to-br from-zinc-700/10 via-transparent to-transparent')
const bgBlurClass = computed(() => badgeStyles[props.project.category]?.blur || 'bg-zinc-500')
const categoryIcon = computed(() => categoryIcons[props.project.category] || categoryIcons.portfolios)

const cardRef = ref(null)

onMounted(() => {
  if (typeof IntersectionObserver === 'undefined' || !cardRef.value) return
  const observer = new IntersectionObserver(
    ([entry]) => {
      if (entry.isIntersecting) {
        entry.target.classList.add('animate-fade-in-up')
        observer.unobserve(entry.target)
      }
    },
    { threshold: 0.1 }
  )
  observer.observe(cardRef.value)
})
</script>
