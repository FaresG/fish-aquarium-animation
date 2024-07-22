<script setup>
import {computed, onMounted, ref, watch} from "vue";

const props = defineProps({
  fish: {
    type: Object,
    required: true
  }
})
const emit = defineEmits(['fishDead'])

const xPosition = ref(props.fish?.xPosition)
const yPosition = ref(props.fish?.yPosition)
const positionStyle = computed(() => {
  return `top: ${yPosition.value}%; left: ${xPosition.value}%;`
})

const forwardX = ref(true)
const forwardY = ref(true)
const baseStep = 0.5
const step = computed(() => {
  return fishIsDead.value ? baseStep / 2: baseStep
})
const updateX = () => {
  switch (xPosition.value) {
    case 0:
      forwardX.value = true
      break
    case 100:
      forwardX.value = false
      break
  }

  forwardX.value ? xPosition.value+= step.value : xPosition.value-= step.value
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
  forwardY.value ? yPosition.value+= step.value : yPosition.value-= step.value
}
const updateCoords = () => {
  updateX()
  updateY()
}

const hungryTimerCadence = 1
const hungryTimerWidth = ref(0)
const hungryTimerWidthParse = computed(() => {
  let color = '#FF5500'
  if (hungryTimerWidth < 20) color = '#00FF00'
  else if (hungryTimerWidth < 40) color = '#55FF00'
  else if (hungryTimerWidth < 60) color = '#AAFF00'
  else if (hungryTimerWidth < 80) color = '#FFAA00'
  return `width: ${hungryTimerWidth.value}%; background-color:${color}`
})

const updateHungryMeter = () => {
  if (hungryTimerWidth.value < 100)
    hungryTimerWidth.value += hungryTimerCadence
}
setInterval(() => {
  updateCoords()
  updateHungryMeter()
}, 40)

const feedFish = () => {
  if (props.fish.isHungry && !fishIsDead.value) {
    hungryTimerWidth.value = 0
    clearTimeout(timer)
  }
}

watch(hungryTimerWidth, (newValue) => {
  props.fish.isHungry = newValue === 100
  if (props.fish.isHungry) startDeathTimer()
})

const deathTimer = 10
// to retrieve the original image
let timer
const fishIsDead = ref(false)
const startDeathTimer = () => {
  timer = setTimeout(() => {
    if (props.fish.isHungry) {
      emit('fishDead', props.fish.id)
      fishIsDead.value = true
    }
  }, deathTimer * 1000)
}
</script>


<template>
  <div
      :style="positionStyle"
      :class="[{'hover:cursor-pointer': props.fish.isHungry}, `min-w-[120px]`]"
      class="absolute flex flex-col gap-2"
      @click="feedFish"
  >
    <p
        v-show="props.fish.isHungry && !fishIsDead"
        class="py-2 bg-white text-black text-center w-full border rounded-xl border-white opacity-90 mb-1"
    >Feed Me!</p>
    <p
        v-show="fishIsDead"
        class="py-2 bg-white text-red-500 text-center w-full border rounded-xl border-white opacity-90 mb-1"
    >Fish died!</p>
    <img
        :src="fishIsDead ? 'dead.png' : `/${fish.image}.png`"
        :alt="fish.name"
        :class="`w-[${fish.fishWidth}px]`"
    />
    <div>
      <p class="text-white text-center bg-gray-800 p-3 border rounded-xl border-gray-800">{{ fish.name }}</p>
      <div class="w-full h-[10px] bg-transparent ">
        <div
            class="w-0 h-full border-2 mt-1 rounded-xl"
            :style="hungryTimerWidthParse"
        ></div>
      </div>
    </div>
  </div>
</template>