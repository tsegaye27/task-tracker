<script setup lang="ts">
import type { TaskProps } from "@/types/TaskProps";
defineProps({
  task: {
    type: Object as () => TaskProps,
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
  <div
    @dblclick="toggleReminder(task.id)"
    :class="[task?.reminder ? 'reminder' : '', 'task']"
  >
    <h3>
      {{ task.text }}
      <i @click="onDelete(task.id)" class="fas fa-times"></i>
    </h3>
    <h5>{{ task.day }}</h5>
  </div>
</template>

<style>
.task {
  background: #f4f4f4;
  margin: 5px;
  padding: 2px 10px;
  border-radius: 4px;
  cursor: pointer;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
}

.fas {
  color: red;
  cursor: pointer;
}

h3 {
  font-weight: normal;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.task.reminder {
  border-left: 5px solid green;
}
</style>
