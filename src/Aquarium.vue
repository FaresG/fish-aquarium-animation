<script setup>
import Fish from "@/Fish.vue";

defineProps(['fishInTheAquarium', 'fishWidth'])
</script>

<template>
  <div class="aquarium">
    <Fish
      v-for="(fish, key) in fishInTheAquarium"
      :key="key"
      :fish="fish"
    />
  </div>
</template>

<style scoped>

.aquarium {
  @apply w-full h-full bg-center bg-no-repeat relative;
  background-image: url('../public/bg.jpg');
}
</style>
