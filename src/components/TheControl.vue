<script setup lang="ts">
import type { Config } from '~/types';

const { config } = defineProps<{
  config: Config
}>()
</script>

<template>
  <div class="bg-slate-800/50 backdrop-blur border border-slate-700/50 rounded-xl p-4 lg:sticky lg:top-4">
    <!-- Header -->
    <div class="text-center pb-3 mb-3 border-b border-slate-700/50">
      <div class="flex items-center justify-center gap-2 mb-2">
        <span i-material-symbols-add-photo-alternate-rounded class="text-xl text-violet-400"></span>
        <span i-material-symbols:picture-as-pdf class="text-xl text-cyan-400"></span>
      </div>
      <h1 class="text-base font-bold text-white">9M2PJU Watermark PDF</h1>
      <p class="text-xs text-gray-400">Add watermark to image/pdf</p>
    </div>

    <!-- Settings Grid -->
    <div class="space-y-2">
      <TheInput 
        v-for="(val, key) in config" 
        :key="key"
        :property="key" 
        :value="val" 
        @update:value="(val: string | number | boolean) => $emit('update', key, val)"
      />
    </div>

    <!-- Footer -->
    <div class="mt-3 pt-3 border-t border-slate-700/50">
      <p class="text-[10px] text-gray-500 text-center mb-2">
        Host on GitHub, your files will be safe
      </p>
      <TheFooter />
    </div>
  </div>
</template>