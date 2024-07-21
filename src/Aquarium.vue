<script setup>

import Fish from "@/Fish.vue";
</script>

<template>
  <div class="aquarium">
    <Fish />
  </div>
</template>

<style scoped>

.aquarium {
  @apply w-full h-full bg-center bg-no-repeat relative;
  background-image: url('../public/bg.jpg');
}
</style>
