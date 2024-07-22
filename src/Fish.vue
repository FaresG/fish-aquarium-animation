<script setup>
import {computed, onMounted, ref, watch} from "vue";

const props = defineProps({
  fish: {
    type: Object,
    required: true
  }
})

const xPosition = ref(props.fish?.xPosition)
const yPosition = ref(props.fish?.yPosition)
const positionStyle = computed(() => {
  return `top: ${yPosition.value}%; left: ${xPosition.value}%;`
})

const forwardX = ref(true)
const forwardY = ref(true)
const step = 0.5
const updateX = () => {
  switch (xPosition.value) {
    case 0:
      forwardX.value = true
      break
    case 100:
      forwardX.value = false
      break
  }

  forwardX.value ? xPosition.value+= step : xPosition.value-= step
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
  forwardY.value ? yPosition.value+= step : yPosition.value-= step
}
const updateCoords = () => {
  updateX()
  updateY()
}

setInterval(() => {
  updateCoords()
}, 40)
</script>


<template>
  <div
      :style="positionStyle"
      class="absolute flex flex-col items-center justify-center gap-2"
  >
    <img
        :src="`/${fish.image}.png`"
        :alt="fish.name"
        :class="`w-[${fish.fishWidth}px]`"
    />
    <p class=" text-white bg-gray-800 p-3 border rounded-xl border-gray-800">{{ fish.name }}</p>
  </div>
</template>