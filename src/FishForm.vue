<script setup>
import {reactive, ref} from "vue";

const props = defineProps(['fishWidth'])
const emit = defineEmits(['newFish'])
const fishImages= [
    'golden-purple-fish',
    'goldfish',
    'guppie',
    'tropical-fish',
    'tuna'
]
const fish = reactive({
  name: '',
  isHungry: false,
  xPosition: 0,
  yPosition: 0,
  fishWidth: 0,
  image: ''
})
const selectedFishImg = ref('')
const fishName = ref()
const addFish = () => {
  if (!fishName.value.value || !selectedFishImg.value) return

  fish.name = fishName.value.value
  fish.xPosition = Math.random() * 100
  fish.yPosition = Math.random() * 100
  fish.fishWidth = props.fishWidth
  fish.image = selectedFishImg.value

  emit('newFish', fish)

  resetForm()
}
const resetForm = () => {
  selectedFishImg.value = ''
  fishName.value.value = ''
}
</script>

<template>
<div class="text-white p-5 flex flex-col gap-5">
  <h3 class="text-xl">Fish Type</h3>
  <div class="flex gap-2 flex-wrap">
    <img
      v-for="fishImg in fishImages"
      :src="`../public/${fishImg}.png`"
      alt="{{ fishImg }}"
      class="w-[120px] hover:cursor-pointer border border-transparent hover:border-blue-400"
      :class="{'border-blue-400': fishImg === selectedFishImg}"
      @click="selectedFishImg = fishImg"
    />
  </div>

  <h3 class="text-xl">Name</h3>
  <input
      class="p-2 border rounded text-black"
      placeholder="Type fish name"
      ref="fishName"
  />
  <button
      class="w-full py-5 text-center text-3xl bg-red-600 border rounded border-red-600 hover:opacity-80"
      @click="addFish"
  >Add Fish</button>
</div>
</template>

<style scoped>
</style>
