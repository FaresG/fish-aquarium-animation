<script setup>
import FishForm from "@/FishForm.vue";
import Aquarium from "@/Aquarium.vue";
import {ref} from "vue";

const fishInTheAquarium = ref([])
const fishWidth = 120
const addNewFish = (newFish) => {
  newFish.id = fishInTheAquarium.value.length + 1
  newFish.xPosition = Math.round(Math.random() * 100)
  newFish.yPosition = Math.round(Math.random() * 100)
  newFish.fishWidth = fishWidth

  fishInTheAquarium.value.push({
    id: newFish.id,
    name: newFish.name,
    xPosition: newFish.xPosition,
    yPosition: newFish.yPosition,
    fishWidth: newFish.fishWidth,
    isHungry: newFish.isHungry,
    image: newFish.image
  })
}
const removeFish = (deadFishId) => {
  setTimeout(() => {
    fishInTheAquarium.value = fishInTheAquarium.value.filter((fish) => fish.id !== deadFishId)
  }, 3000)
}
</script>

<template>
<div class="flex w-screen h-screen">
  <div class="basis-1/4">
    <FishForm  @new-fish="addNewFish"/>
  </div>
  <div class="basis-3/4">
    <Aquarium
        :fish-in-the-aquarium="fishInTheAquarium"
        @dead-fish="removeFish"
    />
  </div>
</div>
</template>
