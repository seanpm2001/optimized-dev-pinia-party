<template>
  <section class="partyArea">
    <!-- Party content -->
    <h1>Pinia's Party</h1>
    <h2>{{ clicker.balance }} confetti</h2>
    <button @click="onClick">
      <div class="inner">✨</div>
    </button>
    <!-- Confetti canvas -->
    <canvas ref="canvas"></canvas>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import Confetti from 'js-confetti'

import { useClicker } from '../stores/clicker'

const clicker = useClicker()

// Setup confetti canvas
const canvas = ref(null)
let confetti = null
const addConfetti = (amount = 1) => {
  confetti?.addConfetti({
    emojis: ['✨'],
    emojiSize: 80,
    confettiNumber: amount
  })
}
onMounted(() => {
  confetti = new Confetti({
    canvas: canvas.value
  })
})

const onClick = () => {
  clicker.balance++
  addConfetti()
}
</script>