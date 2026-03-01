<template>
  <header class="fixed top-4 left-1/2 -translate-x-1/2 z-30 w-full px-4">
    <div class="w-full flex justify-center">
      <div class="w-full max-w-xl bg-white/85 backdrop-blur-xl rounded-full px-2 py-2 flex items-center justify-between shadow-[0_12px_30px_rgba(15,118,110,0.25)] border border-emerald-100/80">
        <div class="flex-1 flex items-center justify-center gap-2 md:gap-4">
          <button
            v-for="tab in tabs"
            :key="tab"
            @click="$emit('change-tab', tab)"
            class="px-3 md:px-4 py-1.5 rounded-full text-xs md:text-sm font-semibold transition-all"
            :class="tab === activeTab
              ? 'bg-emerald-500 text-white shadow-md scale-[1.02]'
              : 'text-emerald-900/80 hover:bg-emerald-50'"
          >
            {{ tab }}
          </button>
        </div>
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
