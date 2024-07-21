<script setup>
import {computed, onMounted, ref} from "vue";

const props = defineProps({
  fish: {
    type: Object,
    required: true
  }
})

onMounted(() => {
  console.log(props.fish)
})
// Assume that it will never start with 0, 0 coords
const xPosition = ref(props.fish?.xPosition)
const yPosition = ref(props.fish?.yPosition)
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
  <img
      :src="`../public/${fish.image}`"
      :alt="fish.name"
      :class="`w-[${fish.fishWidth}px] absolute`"
      :style="positionStyle"
  />
</template>