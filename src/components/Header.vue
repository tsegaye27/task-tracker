<script setup lang="ts">
import Button from "./Button.vue";
defineProps<{ title?: string }>();
</script>

<template>
  <header>
    <h1>{{ title }}</h1>
    <Button text="Add Task" />
  </header>
</template>

<style scoped>
header {
  display: flex;
  align-items: center;
  padding: 16px;
  justify-content: space-between;
}
</style>
