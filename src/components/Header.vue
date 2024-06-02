<script setup lang="ts">
import Button from "./Button.vue";
defineProps<{
  title: string;
}>();
const emit = defineEmits(["btn-click"]);
</script>

<template>
  <header>
    <h1>{{ title }}</h1>
    <Button @btn-click="emit('btn-click')" text="Add Task" />
  </header>
</template>

<style scoped>
header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin: 2rem 0;
}
h1 {
  font-weight: 500;
}
</style>
