<script setup>

import FishForm from "@/FishForm.vue";
import Aquarium from "@/Aquarium.vue";
</script>

<template>
<div class="flex w-screen h-screen">
  <div class="basis-1/4">
    <FishForm />
  </div>
  <div class="basis-3/4">
    <Aquarium />
  </div>
</div>
</template>
