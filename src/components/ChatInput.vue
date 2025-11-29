<template>
  <footer
    class="fixed left-1/2 -translate-x-1/2 bottom-4 w-full px-4 md:px-10 pointer-events-none z-20"
  >
    <div class="max-w-xl mx-auto pointer-events-auto">
      <div class="relative">
        <input
          type="text"
          :value="modelValue"
          :disabled="sending"
          @input="$emit('update:modelValue', $event.target.value)"
          @keypress="onKeyPress"
          placeholder="Ketikan pesan kamu disini"
          class="w-full px-8 pr-16 py-4 rounded-full bg-emerald-300/70 border border-emerald-300/80
                 placeholder-white/80 text-white text-sm md:text-base font-medium
                 shadow-md outline-none focus:ring-2 focus:ring-emerald-500/70
                 disabled:opacity-70 disabled:cursor-not-allowed"
        />

        <button
          @click="emitSend"
          :disabled="sending"
          class="absolute right-3 top-1/2 -translate-y-1/2 w-9 h-9 flex items-center justify-center
                 rounded-full bg-emerald-400 shadow-md hover:bg-emerald-500 active:scale-95
                 transition-transform disabled:opacity-70 disabled:cursor-not-allowed"
        >
          <Send class="w-4 h-4 text-white" />
        </button>
      </div>
    </div>
  </footer>
</template>

<script setup>
import { Send } from 'lucide-vue-next'

const props = defineProps({
  modelValue: {
    type: String,
    default: ''
  },
  sending: {
    type: Boolean,
    default: false
  }
})

const emit = defineEmits(['update:modelValue', 'send'])

const emitSend = () => {
  if (!props.modelValue.trim() || props.sending) return
  emit('send')
}

const onKeyPress = (e) => {
  if (e.key === 'Enter' && !e.shiftKey) {
    e.preventDefault()
    emitSend()
  }
}
</script>
