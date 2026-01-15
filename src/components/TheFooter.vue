<script setup lang="ts">
const showDonateModal = ref(false)
</script>

<template>
  <div class="flex items-center justify-center gap-2">
    <a
      href="https://hamradio.my"
      target="_blank"
      class="p-2.5 rounded-lg bg-white/5 border border-white/10 hover:bg-white/10 text-white/50 hover:text-white transition-all"
      title="Visit hamradio.my"
    >
      <div i-carbon-home class="text-xs"></div>
    </a>
    
    <!-- Donate Button -->
    <button
      @click="showDonateModal = true"
      class="p-2.5 rounded-lg bg-white/5 border border-white/10 hover:border-[#ff006e]/50 text-white/50 hover:text-[#ff006e] transition-all"
      title="Support this project"
    >
      <div i-carbon-favorite class="text-xs"></div>
    </button>
  </div>

  <!-- Donate Modal -->
  <Teleport to="body">
    <div
      v-if="showDonateModal"
      class="fixed inset-0 z-50 flex items-center justify-center bg-slate-900/80 backdrop-blur-sm"
      @click.self="showDonateModal = false"
    >
      <div class="glass-card p-8 max-w-[340px] mx-4 text-center shadow-2xl animate-fade-in">
        <div class="flex justify-between items-center mb-6">
          <h3 class="text-sm font-bold tracking-widest uppercase text-white">Project Support</h3>
          <button
            @click="showDonateModal = false"
            class="p-1 rounded-md hover:bg-white/10 text-white/40 hover:text-white transition-all"
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

