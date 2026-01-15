<script setup lang="ts">
import type { Config, ConfigKey } from '~/types';
import { basicSettings, advancedSettings } from '~/const';

const { config } = defineProps<{
  config: Config
}>()

const showAdvanced = ref(false)
</script>

<template>
    
    <div class="px-2 pb-2">
      <!-- Old Header Removed for classic toolbox look -->
      <div class="text-center py-2 mb-2 border-b border-gray-400 border-b-white">
        <h1 class="text-base font-bold">PDF Watermark</h1>
      </div>

    <!-- Basic Settings -->
    <div class="space-y-2">
      <TheInput 
        v-for="key in basicSettings" 
        :key="key"
        :property="key as ConfigKey" 
        :value="config[key as keyof Config]" 
        @update:value="(val: string | number | boolean) => $emit('update', key, val)"
      />
    </div>

    <!-- Advanced Settings Toggle -->
    <button 
      @click="showAdvanced = !showAdvanced"
      class="w-full mt-3 py-2 flex items-center justify-center gap-2 text-xs text-gray-400 hover:text-white transition-colors"
    >
      <span>{{ showAdvanced ? 'Hide' : 'Show' }} Advanced Settings</span>
      <span 
        :class="showAdvanced ? 'rotate-180' : ''" 
        class="transition-transform duration-200"
        i-carbon-chevron-down
      ></span>
    </button>

    <!-- Advanced Settings (Collapsible) -->
    <div 
      v-show="showAdvanced"
      class="mt-2 pt-2 border-t border-slate-700/30 space-y-2"
    >
      <TheInput 
        v-for="key in advancedSettings" 
        :key="key"
        :property="key as ConfigKey" 
        :value="config[key as keyof Config]" 
        @update:value="(val: string | number | boolean) => $emit('update', key, val)"
      />
    </div>

    <!-- Save Config Toggle -->
    <div class="mt-3 pt-3 border-t border-slate-700/50">
      <TheInput 
        property="saveConfig" 
        :value="config.saveConfig" 
        @update:value="(val: string | number | boolean) => $emit('update', 'saveConfig', val)"
      />
    </div>

    <!-- Footer -->
    <div class="mt-3 pt-3 border-t border-slate-700/50">
      <p class="text-[10px] text-gray-500 text-center mb-2">
        Remake by <a href="https://hamradio.my" target="_blank" rel="noopener noreferrer" class="text-blue-800 hover:text-blue-600 underline">9M2PJU</a>
      </p>
      <TheFooter />
    </div>
  </div>
</template>