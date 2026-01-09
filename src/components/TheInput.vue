<script setup lang="ts">
import type { ConfigKey } from '~/types'
import { tooltips } from '~/const'

const { property } = defineProps<{
  property: ConfigKey
}>()

const { value } = defineModels<{
  value: string | number | boolean
}>()
</script>

<template>
  <div class="flex items-center justify-between py-1.5">
    <!-- Label -->
    <label 
      :for="property"
      class="text-xs text-gray-400 capitalize"
      :title="tooltips[property]"
    >
      {{ property }}
    </label>
    
    <!-- Switch for saveConfig -->
    <template v-if="property === 'saveConfig'">
      <TheSwitch :value="value" @update:value="(val: boolean) => $emit('update:value', val)" />
    </template>
    
    <!-- Text input for words -->
    <template v-else-if="property === 'words'">
      <input
        :id="property"
        v-model="value"
        type="text"
        class="w-32 sm:w-36 px-2 py-1 text-xs bg-slate-700/50 border border-slate-600 rounded text-white focus:border-violet-500 focus:outline-none"
        placeholder="Watermark text"
      >
    </template>
    
    <!-- Range for compression -->
    <template v-else-if="property === 'compression'">
      <div class="flex items-center gap-2">
        <input 
          type="range" 
          min="0" 
          max="1" 
          step="0.1"
          v-model="value"
          class="w-20 sm:w-24 h-1 bg-slate-600 rounded appearance-none cursor-pointer accent-violet-500"
        >
        <span class="text-[10px] text-gray-500 w-6">{{ value }}</span>
      </div>
    </template>
    
    <!-- Number input -->
    <template v-else-if="typeof value === 'number'">
      <input
        :id="property"
        v-model="value"
        type="number"
        class="w-32 sm:w-36 px-2 py-1 text-xs text-center bg-slate-700/50 border border-slate-600 rounded text-white focus:border-violet-500 focus:outline-none"
      >
    </template>
    
    <!-- Text input (color, etc) -->
    <template v-else>
      <input
        :id="property"
        v-model="value"
        type="text"
        class="w-32 sm:w-36 px-2 py-1 text-xs text-center bg-slate-700/50 border border-slate-600 rounded text-white focus:border-violet-500 focus:outline-none"
      >
    </template>
  </div>
</template>
