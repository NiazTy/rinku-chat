<template>
  <div
    class="max-w-xs px-4 py-3 rounded-xl text-white text-sm shadow-lg"
    :class="position === 'left'
      ? 'bg-slate-800'
      : 'bg-slate-800 ml-auto'"
  >
    {{ text }}
  </div>
</template>

<script setup>
defineProps({
  text: String,
  position: {
    type: String,
    default: 'left'
  }
})
</script>
