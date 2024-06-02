<script setup lang="ts">
defineProps<{
  text: string;
  setShowAddTask: () => void;
  color?: string;
}>();
</script>

<template>
  <button
    :style="{
      background: color,
    }"
    class="btn"
    v-on:click="setShowAddTask()"
  >
    {{ text }}
  </button>
</template>

<style scoped>
.btn {
  background-color: #56cd56;
  color: white;
  border: none;
  padding: 0.5rem 0.85rem;
  border-radius: 0.35rem;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.201);
  cursor: pointer;
}
</style>
