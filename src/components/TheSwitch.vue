<script setup lang="ts">
const { value } = defineProps<{
  value: boolean
}>()

const emit = defineEmits(['update:value'])
</script>

<template>
  <button 
    type="button"
    class="relative w-9 h-5 rounded-full transition-colors"
    :class="value ? 'bg-violet-600' : 'bg-slate-600'"
    @click="emit('update:value', !value)"
  >
    <span 
      class="absolute top-0.5 w-4 h-4 bg-white rounded-full shadow transition-transform"
      :class="value ? 'left-[18px]' : 'left-0.5'"
    ></span>
  </button>
</template>
