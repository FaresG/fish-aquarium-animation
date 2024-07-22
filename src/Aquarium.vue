<script setup>
import Fish from "@/Fish.vue";

defineProps(['fishInTheAquarium'])
defineEmits(['deadFish'])
</script>

<template>
  <div class="aquarium">
    <Fish
      v-for="fish in fishInTheAquarium"
      :key="fish?.id"
      :fish="fish"
      @fish-dead="(deadFishId) => $emit('deadFish', deadFishId)"
    />
  </div>
</template>

<style scoped>

.aquarium {
  @apply w-full h-full bg-center bg-no-repeat relative overflow-hidden;
  background-image: url('/bg.jpg');
}
</style>
