<script setup lang="ts">
import type { TaskProps } from "@/types/TaskProps";
import Task from "./Task.vue";
defineProps({
  tasks: {
    type: Array as () => TaskProps[],
    required: true,
  },
  onDelete: {
    type: Function as unknown as () => (id: number) => void,
    required: true,
  },
  toggleReminder: {
    type: Function as unknown as () => (id: number) => void,
    required: true,
  },
});
</script>

<template>
  <div v-for="task in tasks">
    <Task
      :task="task as TaskProps"
      :onDelete="onDelete"
      :toggleReminder="toggleReminder"
    />
  </div>
</template>

<style></style>
