<template>
  <footer class="fixed left-1/2 -translate-x-1/2 bottom-4 w-full px-4 md:px-6 pointer-events-none z-40">
    <div class="max-w-xl mx-auto pointer-events-auto">
      <div class="rounded-3xl bg-white/85 backdrop-blur-xl shadow-[0_18px_40px_rgba(15,118,110,0.28)] border border-emerald-100/80 px-3 py-2">
        <div class="relative flex items-center gap-2">
          <input
            type="text"
            :value="modelValue"
            :disabled="sending"
            @input="$emit('update:modelValue', $event.target.value)"
            @keypress="onKeyPress"
            placeholder="Ketikan pesan kamu di sini..."
            class="w-full bg-transparent border-none outline-none px-4 pr-14 py-2 text-sm md:text-base text-slate-800 placeholder-slate-400 font-medium"
          />

          <button
            @click="emitSend"
            :disabled="sending"
            class="absolute right-2.5 top-1/2 -translate-y-1/2 w-9 h-9 flex items-center justify-center rounded-full bg-emerald-500 shadow-md hover:bg-emerald-600 active:scale-95 transition-transform disabled:opacity-60 disabled:cursor-not-allowed"
          >
            <Send class="w-4 h-4 text-white" />
          </button>
        </div>
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