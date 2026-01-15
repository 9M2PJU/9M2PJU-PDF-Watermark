<script setup lang="ts">
const showDonateModal = ref(false)
</script>

<template>
  <div class="flex items-center justify-center gap-2">
    <a
      href="https://hamradio.my"
      target="_blank"
      class="p-2 rounded-lg bg-slate-700/50 hover:bg-slate-600 text-gray-400 hover:text-white transition-colors"
      title="Visit hamradio.my"
    >
      <div i-carbon-home class="text-sm"></div>
    </a>
    
    <a
      href="https://github.com/9M2PJU/9M2PJU-PDF-Watermark"
      target="_blank"
      class="p-2 rounded-lg bg-slate-700/50 hover:bg-slate-600 text-gray-400 hover:text-white transition-colors"
      title="View on GitHub"
    >
      <div i-carbon-logo-github class="text-sm"></div>
    </a>

    <!-- Donate Button -->
    <button
      @click="showDonateModal = true"
      class="p-2 rounded-lg bg-pink-600/70 hover:bg-pink-500 text-white transition-colors"
      title="Support this project"
    >
      <div i-carbon-favorite class="text-sm"></div>
    </button>
  </div>

  <!-- Donate Modal -->
  <Teleport to="body">
    <div
      v-if="showDonateModal"
      class="fixed inset-0 z-50 flex items-center justify-center bg-slate-900/80 backdrop-blur-sm"
      @click.self="showDonateModal = false"
    >
      <div class="bg-slate-800 border border-slate-700 rounded-2xl p-6 max-w-sm mx-4 text-center shadow-2xl">
        <div class="flex justify-between items-center mb-4">
          <h3 class="text-lg font-bold text-white">Support This Project</h3>
          <button
            @click="showDonateModal = false"
            class="p-1 rounded-lg hover:bg-slate-700 text-gray-400 hover:text-white transition-colors"
          >
            <div i-carbon-close class="text-lg"></div>
          </button>
        </div>
        
        <div class="bg-white rounded-xl p-3 mb-4">
          <img
            src="https://lh3.googleusercontent.com/d/1lf1zgIN1Kx5cduZM79n3boGDJQ68uSJ_=w1000?authuser=0"
            alt="DuitNow QR Code"
            class="w-full max-w-[250px] mx-auto"
          />
        </div>
        
        <p class="text-sm text-gray-300 mb-2">
          Scan with eWallet or Banking App
        </p>
        <p class="text-xs text-gray-500">
          Thank you for your support! 💜
        </p>
      </div>
    </div>
  </Teleport>
</template>

