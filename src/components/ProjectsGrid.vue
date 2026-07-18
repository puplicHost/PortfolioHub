<template>
  <section id="projects" class="px-4 pb-20">
    <div class="max-w-6xl mx-auto">
      <div class="text-center mb-10">
        <h2 class="text-2xl md:text-3xl font-bold text-white mb-2">Featured Work</h2>
        <p class="text-sm md:text-base text-gray-400">A curated selection of projects showcasing modern design and development</p>
      </div>

      <div v-if="filteredProjects.length === 0" class="text-center py-20 animate-fade-in">
        <div class="inline-flex items-center justify-center w-20 h-20 rounded-2xl bg-card/50 border border-zinc-800 mb-5">
          <svg class="w-10 h-10 text-zinc-600" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1">
            <path stroke-linecap="round" stroke-linejoin="round" d="M20.25 7.5l-.625 10.632a2.25 2.25 0 01-2.247 2.118H6.622a2.25 2.25 0 01-2.247-2.118L3.75 7.5m6 4.125l2.25 2.25m0 0l2.25-2.25M12 13.875l2.25-2.25M12 13.875l-2.25 2.25M3.375 7.5h17.25c.621 0 1.125-.504 1.125-1.125v-1.5c0-.621-.504-1.125-1.125-1.125H3.375c-.621 0-1.125.504-1.125 1.125v1.5c0 .621.504 1.125 1.125 1.125z" />
          </svg>
        </div>
        <h3 class="text-xl font-semibold text-gray-200 mb-2">No projects found</h3>
        <p class="text-gray-500">Try a different search term or filter</p>
      </div>

      <div v-else class="grid grid-cols-2 md:grid-cols-2 lg:grid-cols-3 gap-3 md:gap-6">
        <ProjectCard
          v-for="project in filteredProjects"
          :key="project.id"
          :project="project"
        />
      </div>
    </div>
  </section>
</template>

<script setup>
import { computed } from 'vue'
import { projects } from '../data/projects.js'
import ProjectCard from './ProjectCard.vue'

const props = defineProps({
  filters: {
    type: Object,
    default: () => ({ category: 'all', search: '' }),
  },
})

const filteredProjects = computed(() => {
  return projects.filter((project) => {
    const matchCategory =
      props.filters.category === 'all' || project.category === props.filters.category
    const matchSearch =
      !props.filters.search ||
      project.title.toLowerCase().includes(props.filters.search) ||
      project.description.toLowerCase().includes(props.filters.search)
    return matchCategory && matchSearch
  })
})
</script>
