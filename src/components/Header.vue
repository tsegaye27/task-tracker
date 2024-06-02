<script setup lang="ts">
import Button from "./Button.vue";
defineProps<{
  title: string;
  showAddTask: boolean;
  setShowAddTask: () => void;
}>();
</script>

<template>
  <header>
    <h1>{{ title }}</h1>
    <Button
      :text="showAddTask ? 'Close' : 'Add Task'"
      :color="showAddTask ? '#ff1113' : '#56cd56'"
      :setShowAddTask="setShowAddTask"
    />
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
