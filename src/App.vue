<script setup lang="ts">
import { ref } from "vue";
import AddTask from "./components/AddTask.vue";
import Header from "./components/Header.vue";
import Tasks from "./components/Tasks.vue";
import type { TaskProps } from "./types/TaskProps";
const tasks = ref<TaskProps[]>([]);

const onDelete = (id: number) => {
  if (confirm("Are you sure?")) {
    tasks.value = tasks.value.filter((task) => task.id !== id);
  }
};

const toggleReminder = (id: number) => {
  tasks.value = tasks.value.map((task) =>
    task.id === id ? { ...task, reminder: !task.reminder } : task
  );
};

const handleTaskAddition = (newTask: TaskProps) => {
  tasks.value.push(newTask);
};
</script>
<template>
  <div class="container">
    <Header title="Task Tracker" />
    <AddTask @taskAdded="handleTaskAddition" />
    <Tasks
      :tasks="tasks"
      :onDelete="onDelete"
      :toggleReminder="toggleReminder"
    />
  </div>
</template>

<style scoped>
.container {
  padding: 0.7rem 1.5rem;
  border: 2px solid #7474db;
  border-radius: 0.65rem;
  margin: 2rem 1rem;
  width: 30rem;
}
</style>
