<script setup lang="ts">
import type { Config, HTMLInputEvent } from '~/types'
import { generateCanvas, downloadImage, loadPdf, img2Pdf } from '~/util';

const { config } = defineProps<{
  config: Config
}>()

// Refs - declare early so watchers can use them
let img: HTMLImageElement | null
const canvas = ref()
const preview = ref()
const url = ref('')
const pdfUrl = ref('')
const loading = ref(false)
const wrap = ref() as Ref<HTMLElement>

// Flag to prevent duplicate PDF loads during initial load
let isLoadingPdf = false

watch(config, configChange)

// Reset the loading flag when PDF loading completes
watch(loading, (newVal) => {
  if (!newVal && isLoadingPdf) {
    isLoadingPdf = false
  }
})

function configChange() {
  loadInit = false
  if(img)
    preview.value.src = generateCanvas(config, img, loadInit).src
  // Only reload PDF if not currently in initial load process
  if(pdfUrl.value && !isLoadingPdf)
    loadPdf(pdfUrl.value, config, wrap, loading, loadInit)
}

let loadInit = false
let type = ''
let name = ''

function load(e: Event) {
  loadInit = true
  reLoad()
  const files = (e as HTMLInputEvent).target.files
  if (files && files.length > 0) {
    const file = files[0]
    type = file.type
    name = file.name
    if(type.startsWith("image/")) 
      resolveImage(file)
    if(type === "application/pdf") {
      loading.value = true
      isLoadingPdf = true
      resolvePDF(file)
    }
  }
}

function reLoad(){
  if(img) img = null
  if(url.value) url.value = ''
  if(pdfUrl.value) pdfUrl.value = ''
  if(wrap.value) wrap.value.innerHTML = ''
}

function resolveImage(file: Blob){
  const reader = new FileReader()
  reader.readAsDataURL(file)
  reader.onload = () => {
    const image = new Image()
    image.src = reader.result as string
    img = image
    image.onload = () => {
      config.width = image.width
      config.height = image.height
      preview.value.src = generateCanvas(config, image, loadInit).src
    }
  }
  reader.onloadend = () => {
    url.value = reader.result as string
  }
}

function resolvePDF(file: Blob){
  const reader = new FileReader()
  reader.readAsDataURL(file)
  reader.onloadend = () => {
    pdfUrl.value = reader.result as string
    loadPdf(pdfUrl.value, config, wrap, loading, loadInit)
  }
}

function download() {
  if(url.value === '' && pdfUrl.value === '') return
  
  if(type.startsWith("image/") && img) {
    const src = generateCanvas(config, img, loadInit).src
    downloadImage(src, config, name)
  }
  if(type === "application/pdf") {
    img2Pdf(name, loading)
  }
}
</script>

<template>
  <div>
    <!-- Buttons -->
    <div class="flex gap-2 mb-4">
      <button class="btn-gradient relative overflow-hidden">
        <span class="mr-2">📂</span>
        <span>Open...</span>
        <input type="file" accept="image/*, application/pdf" class="absolute inset-0 opacity-0 cursor-pointer" @change="load">
      </button>
      
      <button
        class="btn-secondary flex items-center"
        :disabled="url === '' && pdfUrl === ''"
        @click="download"
      >
        <span class="mr-2">💾</span>
        <span>Save As...</span>
      </button>
    </div>

    <!-- Preview Area -->
    <div class="glass-card p-6 min-h-[300px] flex items-center justify-center animate-fade-in">
      <!-- Image Preview -->
      <div v-if="url" class="flex items-center justify-center">
        <img 
          ref="preview" 
          :src="url" 
          class="max-w-full h-auto rounded-lg shadow-xl"
          style="max-height: 70vh;"
        >
        <canvas ref="canvas" class="hidden"></canvas>
      </div>
      
      <!-- PDF Preview -->
      <div v-else-if="pdfUrl" class="overflow-auto w-full">
        <div ref="wrap" class="flex flex-wrap gap-3 justify-center [&>canvas]:rounded-lg [&>canvas]:shadow-xl [&>canvas]:max-w-full [&>canvas]:h-auto"></div>
      </div>
      
      <!-- Upload Zone -->
      <label 
        v-else 
        class="upload-zone w-full p-12 cursor-pointer group"
      >
        <div class="mb-4">
          <!-- Classic Windows Icon Simulation -->
          <div class="w-16 h-20 bg-white border-2 border-black relative mx-auto shadow-[2px_2px_0_0_rgba(0,0,0,0.5)]">
             <div class="absolute top-0 right-0 border-l-2 border-b-2 border-black w-4 h-4 bg-gray-200"></div>
             <div class="absolute bottom-2 left-2 right-2 h-1 bg-black"></div>
             <div class="absolute bottom-4 left-2 right-2 h-1 bg-black"></div>
             <div class="absolute bottom-6 left-2 right-2 h-1 bg-black"></div>
          </div>
        </div>
        <p class="text-sm font-bold text-black mb-1">Drag file here to open</p>
        <input type="file" accept="image/*, application/pdf" class="hidden" @change="load">
      </label>
    </div>
    
    <!-- Loading Overlay -->
    <div v-if="loading" class="fixed inset-0 z-50 flex items-center justify-center bg-slate-900/80 backdrop-blur-sm">
      <div class="text-center">
        <div class="w-10 h-10 border-3 border-violet-500 border-t-transparent rounded-full animate-spin mx-auto mb-3"></div>
        <p class="text-sm text-gray-300">Processing...</p>
      </div>
    </div>
  </div>
</template>
