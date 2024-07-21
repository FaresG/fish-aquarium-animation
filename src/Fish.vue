<script setup>
import { computed, ref } from "vue";

const fishWidth = 120
// Assume that it will never start with 0, 0 coords
const xPosition = ref(0)
const yPosition = ref(20)
const positionStyle = computed(() => {
  return `top: ${yPosition.value}%; left: ${xPosition.value}%;`
})

const forwardX = ref(true)
const forwardY = ref(true)
const updateX = () => {
  switch (xPosition.value) {
    case 0:
      forwardX.value = true
      break
    case 100:
      forwardX.value = false
      break
  }

  forwardX.value ? xPosition.value++ : xPosition.value--
}
const updateY = () => {
  switch (yPosition.value) {
    case 0:
      forwardY.value = true
      break
    case 100:
      forwardY.value = false
      break
  }
  forwardY.value ? yPosition.value++ : yPosition.value--
}
const updateCoords = () => {
  updateX()
  updateY()
}

setInterval(() => {
  updateCoords()
}, 50)
</script>

<template>
  <Transition>
    <img
        src="../public/golden-purple-fish.png"
        alt="goldfish"
        :class="`w-[${fishWidth}px] absolute`"
        :style="positionStyle"
    />
  </Transition>
</template>

<style scoped>
.v-enter-active,
.v-leave-active {
  transition: opacity 0.5s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}
</style>
