<script setup lang="ts">
import { onMounted, ref } from "vue";
import AddTask from "./components/AddTask.vue";
import Header from "./components/Header.vue";
import Tasks from "./components/Tasks.vue";
import type { TaskProps } from "./types/TaskProps";
import { useToast } from "vue-toastification";

const tasks = ref<TaskProps[]>([]);
const toast = useToast();

const saveToLocalStorage = () => {
  localStorage.setItem("task", JSON.stringify(tasks.value));
};

const onDelete = (id: number) => {
  if (confirm("Are you sure?")) {
    tasks.value = tasks.value.filter((task) => task.id !== id);
    saveToLocalStorage();
    toast.success("Task deleted successfully!");
  }
};

onMounted(() => {
  const loadFromLocalStorage = localStorage.getItem("task");
  if (loadFromLocalStorage) {
    tasks.value = JSON.parse(loadFromLocalStorage);
  }
});

const toggleReminder = (id: number) => {
  tasks.value = tasks.value.map((task) =>
    task.id === id ? { ...task, reminder: !task.reminder } : task
  );
};

const handleTaskAddition = (newTask: TaskProps) => {
  tasks.value.push(newTask);
  saveToLocalStorage();
};

let showAddTask = false;

const handleToggle = () => {
  showAddTask = !showAddTask;
};
</script>
<template>
  <div class="container">
    <Header @btn-click="handleToggle" title="Task Tracker" />
    <div v-if="showAddTask">
      <AddTask @taskAdded="handleTaskAddition" />
    </div>
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
