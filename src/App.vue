<script setup lang="ts">
import Index from '~/pages/index.vue';
</script>

<template>
  <main class="min-h-screen bg-slate-900 text-gray-200 font-sans">
    <!-- Background gradient -->
    <div class="fixed inset-0 bg-gradient-to-br from-slate-900 via-violet-950/30 to-slate-900 pointer-events-none"></div>
    
    <!-- Content -->
    <div class="relative z-10 p-3 sm:p-4 lg:p-6">
      <Index />
    </div>
  </main>
</template>
