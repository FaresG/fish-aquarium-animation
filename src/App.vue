<script setup>

import FishForm from "@/FishForm.vue";
import Aquarium from "@/Aquarium.vue";
import {ref} from "vue";

const fishInTheAquarium = ref([])
const fishWidth = 120
const addNewFish = (newFish) => {
  if (newFish.name)
  fishInTheAquarium.value.push({

    name: newFish.name,
    isHungry: false,
    xPosition: newFish.xPosition,
    yPosition: newFish.yPosition,
    fishWidth: fishWidth,
    image: newFish.image
  })
}
</script>

<template>
<div class="flex w-screen h-screen">
  <div class="basis-1/4">
    <FishForm :fish-width="fishWidth" @new-fish="addNewFish"/>
  </div>
  <div class="basis-3/4">
    <Aquarium :fish-width="fishWidth" :fish-in-the-aquarium="fishInTheAquarium"/>
  </div>
</div>
</template>
