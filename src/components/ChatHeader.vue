<template>
  <header class="pt-6 flex justify-center">
    <div class="w-full flex justify-center">
      <div
        class="w-full max-w-xl bg-emerald-300 fixed rounded-full px-8 py-3 flex items-center justify-center gap-10 shadow-md"
      >
        <button
          v-for="tab in tabs"
          :key="tab"
          @click="$emit('change-tab', tab)"
          class="text-sm md:text-base font-semibold transition-all"
          :class="tab === activeTab
            ? 'text-white opacity-100 scale-105'
            : 'text-emerald-950/80 opacity-80 hover:opacity-100'
          "
        >
          {{ tab }}
        </button>
      </div>
    </div>
  </header>
</template>

<script setup>
defineProps({
  activeTab: {
    type: String,
    required: true
  }
})

const tabs = ['Beranda', 'Chat', 'Tentang Rinku']
</script>
