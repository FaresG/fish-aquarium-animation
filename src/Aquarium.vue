<script setup>
import Fish from "@/Fish.vue";

defineProps(['fishInTheAquarium'])
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
  @apply w-full h-full bg-center bg-no-repeat relative overflow-hidden;
  background-image: url('/bg.jpg');
}
</style>
