<script setup lang="ts">
import Index from '~/pages/index.vue';
</script>

<template>
  <main 
    class="font-sans min-h-screen text-gray-200 dark bg-gradient-to-br from-slate-950 via-violet-950/20 to-slate-950"
  >
    <div class="fixed inset-0 pointer-events-none" style="background: radial-gradient(ellipse at top, rgba(124,58,237,0.15), transparent 50%)"></div>
    <div class="relative z-10 p-4 md:p-6 lg:p-8">
      <Index />
    </div>
  </main>
</template>
