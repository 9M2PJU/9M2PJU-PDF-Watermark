<script setup lang="ts">
import type { Config, ConfigKey } from '~/types';
import { basicSettings, advancedSettings } from '~/const';

const { config } = defineProps<{
  config: Config
}>()

const showAdvanced = ref(false)
</script>

<template>
  <div class="glass-card p-6 lg:sticky lg:top-4 animate-fade-in shadow-2xl">
    <!-- Header -->
    <div class="text-center pb-6 mb-6 border-b border-border-subtle">
      <div class="flex items-center justify-center gap-4 mb-4">
        <div class="p-2.5 rounded-xl bg-white/5 border border-white/10">
          <span i-material-symbols-add-photo-alternate-rounded class="text-2xl text-white/80"></span>
        </div>
        <div class="p-2.5 rounded-xl bg-white/5 border border-white/10">
          <span i-material-symbols:picture-as-pdf class="text-2xl text-white/80"></span>
        </div>
      </div>
      <h1 class="text-xl font-bold tracking-tight text-white mb-1">9M2PJU WATERMARK</h1>
      <p class="text-[11px] font-medium tracking-[0.2em] text-text-muted uppercase">Premium Security Utility</p>
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
        Remake by <a href="https://hamradio.my" target="_blank" class="text-violet-400 hover:text-violet-300 underline">9M2PJU</a>
      </p>
      <TheFooter />
    </div>
  </div>
</template>