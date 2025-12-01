<template>
  <section class="relative w-full flex flex-col items-center text-center mb-20">

    <!-- Background pattern -->
    <div
      class="absolute inset-0 -z-10 bg-[url('/grid.svg')] opacity-[0.18]
             bg-repeat mask-[linear-gradient(to_bottom,black,transparent)]">
    </div>

    <!-- Soft spotlight -->
    <div class="absolute inset-0 -z-10">
      <div class="absolute w-[280px] h-[280px] bg-emerald-300/30 rounded-full blur-[120px] top-10 left-10"></div>
      <div class="absolute w-[260px] h-[260px] bg-emerald-400/20 rounded-full blur-[130px] bottom-10 right-10"></div>
    </div>

    <!-- NAVIGATION (tab sudah ada dari ChatHeader) -->
    <div class="pt-8"></div>

    <!-- Character + bubbles -->
    <div class="relative flex flex-col items-center mt-14">
      
      <!-- Diana Character -->
      <img
        :src="diana"
        alt="Diana"
        class="w-[260px] md:w-[300px] drop-shadow-[0_8px_25px_rgba(0,0,0,0.25)] select-none"
      />

      <!-- LEFT bubble -->
      <div
        class="absolute -left-4 md:-left-20 top-4 md:top-10 bg-slate-900 text-white 
               text-[13px] md:text-[15px] rounded-2xl px-5 py-3 max-w-[210px]
               shadow-lg border-emerald-300 border-2"
      >
        Kamu gagal? Aman, selama kamu masih bisa membaca kamu berhasil!
      </div>

      <!-- RIGHT bubble -->
      <div
        class="absolute -right-4 md:-right-20 top-24 md:top-20 bg-slate-900 text-white 
               text-[13px] md:text-[15px] rounded-2xl px-5 py-3 max-w-[210px]
               shadow-lg border-emerald-300 border-2"
      >
        Nggak apa-apa jatuh, yang penting kamu nggak berhenti.
      </div>
    </div>

    <!-- Title -->
    <h1 class="mt-10 text-4xl md:text-5xl font-extrabold tracking-wide text-emerald-700 drop-shadow-sm">
      NAMAKU DIANA
    </h1>

    <!-- Input name -->
    <div
      class="mt-6 w-full max-w-xs bg-emerald-200/90 backdrop-blur rounded-full px-5 py-3 flex items-center gap-3 shadow-md border border-emerald-300"
    >
      <span class="text-yellow-500 text-xl">✦</span>
      <input
        v-model="username"
        type="text"
        placeholder="Siapa Nama Kamu?"
        class="flex-1 bg-transparent outline-none text-sm text-emerald-900 placeholder-emerald-700/70"
      />
      <button
        @click="emitSendName"
        class="w-8 h-8 rounded-full bg-emerald-500 hover:bg-emerald-600 flex items-center justify-center text-white transition"
      >
        <Send class="w-4 h-4" />
      </button>
    </div>

  </section>
</template>

<script setup>
import { ref } from 'vue'
import { Send } from 'lucide-vue-next'

const diana = new URL('../assets/img/aimoto-rinku/aimoto-rinku.png', import.meta.url).href

const username = ref('')
const emit = defineEmits(['submit-name'])

const emitSendName = () => {
  if (!username.value.trim()) return
  emit('submit-name', username.value.trim())
}
</script>
