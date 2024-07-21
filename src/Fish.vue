<script setup>
import {computed, ref, watch} from "vue";

const fishWidth = 120
const xPosition = ref(0)
const yPosition = ref(0)
const position = computed(() => {
  return `top: ${yPosition.value}%; left: ${xPosition.value}%;`
})

watch(xPosition, (newValue) => {
  // deduct fish width
  newValue -= fishWidth
})
</script>

<template>
  <Transition>
    <img
        src="../public/golden-purple-fish.png"
        alt="goldfish"
        :class="`w-[${fishWidth}px] absolute`"
        :style="position"
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
