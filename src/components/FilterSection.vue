<template>
  <section class="px-4 pb-8">
    <div class="max-w-2xl mx-auto">
      <div class="relative mb-6">
        <svg class="absolute left-4 top-1/2 -translate-y-1/2 w-5 h-5 text-gray-500" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5">
          <path stroke-linecap="round" stroke-linejoin="round" d="M21 21l-5.197-5.197m0 0A7.5 7.5 0 105.196 5.196a7.5 7.5 0 0010.607 10.607z" />
        </svg>
        <input
          v-model="searchQuery"
          type="text"
          placeholder="Search projects by name or description..."
          aria-label="Search projects"
          class="w-full pl-12 pr-4 py-3.5 rounded-2xl glass text-white placeholder-gray-500
                 focus:outline-none focus:border-primary focus:ring-2 focus:ring-primary/20 transition-all duration-300"
        />
      </div>

      <div class="flex flex-wrap justify-center gap-2">
        <button
          v-for="filter in filtersWithCounts"
          :key="filter.value"
          :aria-label="`Filter by ${filter.label}`"
          @click="activeFilter = filter.value"
          class="group relative inline-flex items-center gap-2 px-4 py-2.5 rounded-xl text-sm font-medium transition-all duration-300 cursor-pointer border"
          :class="activeFilter === filter.value
            ? 'bg-primary text-white border-primary shadow-lg shadow-primary/30'
            : 'bg-card/50 text-gray-400 border-zinc-800/60 hover:text-white hover:border-zinc-700 hover:bg-card'"
        >
          <span v-html="filter.icon" class="w-4 h-4 transition-transform duration-300 group-hover:scale-110"></span>
          <span>{{ filter.label }}</span>
          <span
            class="text-[10px] font-bold px-1.5 py-0.5 rounded-full transition-colors duration-300"
            :class="activeFilter === filter.value
              ? 'bg-white/20 text-white'
              : 'bg-zinc-800 text-gray-500 group-hover:bg-zinc-700 group-hover:text-gray-300'"
          >
            {{ filter.count }}
          </span>
        </button>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, watch, computed } from 'vue'
import { projects } from '../data/projects.js'

const emit = defineEmits(['update:filter'])

const filterDefs = [
  { label: 'All', value: 'all', icon: '<svg fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M4 6a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2H6a2 2 0 01-2-2V6zM14 6a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2h-2a2 2 0 01-2-2V6zM4 16a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2H6a2 2 0 01-2-2v-2zM14 16a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2h-2a2 2 0 01-2-2v-2z" /></svg>' },
  { label: 'Portfolios', value: 'portfolios', icon: '<svg fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M9.75 17L9 20l-1 1h8l-1-1-.75-3M3 13h18M5 17h14a2 2 0 002-2V5a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" /></svg>' },
  { label: 'Business', value: 'business', icon: '<svg fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M19 21V5a2 2 0 00-2-2H7a2 2 0 00-2 2v16m14 0h2m-2 0h-5m-9 0H3m2 0h5M9 7h1m-1 4h1m4-4h1m-1 4h1m-5 10v-5a1 1 0 011-1h2a1 1 0 011 1v5m-4 0h4" /></svg>' },
  { label: 'E-Commerce', value: 'ecommerce', icon: '<svg fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M3 3h2l.4 2M7 13h10l4-8H5.4M7 13L5.4 5M7 13l-2.293 2.293c-.63.63-.184 1.707.707 1.707H17m0 0a2 2 0 100 4 2 2 0 000-4zm-8 2a2 2 0 11-4 0 2 2 0 014 0z" /></svg>' },
]

const filtersWithCounts = computed(() =>
  filterDefs.map((f) => ({
    ...f,
    count: f.value === 'all'
      ? projects.length
      : projects.filter((p) => p.category === f.value).length,
  }))
)

const activeFilter = ref('all')
const searchQuery = ref('')

function emitFilter() {
  emit('update:filter', {
    category: activeFilter.value,
    search: searchQuery.value.toLowerCase(),
  })
}

watch(activeFilter, emitFilter)
watch(searchQuery, emitFilter)
</script>
