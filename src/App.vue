<template>
  <div class="min-h-screen bg-dark text-white">
    <main>
      <LogoSection />
      <SocialLinks />
      <DividerSection />
      <FilterSection @update:filter="onFilterChange" />
      <ProjectsGrid :filters="currentFilters" />
      <ContactSection />
    </main>
    <FooterSection />
    <FloatingWhatsapp />
    <BackToTop />
  </div>
</template>

<script setup>
import { ref } from 'vue'
import LogoSection from './components/LogoSection.vue'
import SocialLinks from './components/SocialLinks.vue'
import DividerSection from './components/DividerSection.vue'
import FilterSection from './components/FilterSection.vue'
import ProjectsGrid from './components/ProjectsGrid.vue'
import ContactSection from './components/ContactSection.vue'
import FooterSection from './components/FooterSection.vue'
import FloatingWhatsapp from './components/FloatingWhatsapp.vue'
import BackToTop from './components/BackToTop.vue'

const currentFilters = ref({ category: 'all', search: '' })

function onFilterChange(filters) {
  currentFilters.value = { ...filters }
}
</script>
