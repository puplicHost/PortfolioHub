<template>
  <button
    v-show="visible"
    @click="scrollToTop"
    aria-label="Back to top"
    class="fixed bottom-6 left-6 z-50 w-11 h-11 rounded-xl glass flex items-center justify-center
           text-white transition-all duration-300 hover:scale-110 hover:border-primary/40 hover:text-primary
           hover:shadow-lg hover:shadow-primary/30 animate-fade-in"
  >
    <svg class="w-5 h-5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
      <path stroke-linecap="round" stroke-linejoin="round" d="M4.5 15.75l7.5-7.5 7.5 7.5" />
    </svg>
  </button>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const visible = ref(false)

function handleScroll() {
  visible.value = window.scrollY > 400
}

function scrollToTop() {
  window.scrollTo({ top: 0, behavior: 'smooth' })
}

onMounted(() => window.addEventListener('scroll', handleScroll))
onUnmounted(() => window.removeEventListener('scroll', handleScroll))
</script>
