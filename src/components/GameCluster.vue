<template>
  <div></div>
</template>

<script setup lang="ts">
// @ts-ignore
import DinoGame from '../lib/game/DinoGame.js'
const game = new DinoGame(600, 150)
const isTouchDevice =
  // @ts-ignore
  'ontouchstart' in window || navigator.maxTouchPoints > 0 || navigator.msMaxTouchPoints > 0

if (isTouchDevice) {
  document.addEventListener('touchstart', ({ touches }) => {
    if (touches.length === 1) {
      game.onInput('jump')
    } else if (touches.length === 2) {
      game.onInput('duck')
    }
  })

  document.addEventListener('touchend', () => {
    game.onInput('stop-duck')
  })
} else {
  const keycodes = {
    JUMP: { 38: 1, 32: 1 },
    DUCK: { 40: 1 }
  }

  document.addEventListener('keydown', ({ keyCode }) => {
    // @ts-ignore
    if (keycodes.JUMP[keyCode]) {
      game.onInput('jump')
      // @ts-ignore
    } else if (keycodes.DUCK[keyCode]) {
      game.onInput('duck')
    }
  })

  document.addEventListener('keyup', ({ keyCode }) => {
    // @ts-ignore
    if (keycodes.DUCK[keyCode]) {
      game.onInput('stop-duck')
    }
  })
}
game.start().catch(console.error)
</script>
