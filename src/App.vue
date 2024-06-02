<script setup lang="ts">
import { onMounted, ref } from "vue";
import AddTask from "./components/AddTask.vue";
import Header from "./components/Header.vue";
import Tasks from "./components/Tasks.vue";
import type { TaskProps } from "./types/TaskProps";
import { useToast } from "vue-toastification";

const tasks = ref<TaskProps[]>([]);
const toast = useToast();
const showAddTask = ref(false);

const saveToLocalStorage = () => {
  localStorage.setItem("task", JSON.stringify(tasks.value));
};

onMounted(() => {
  const loadFromLocalStorage = localStorage.getItem("task");
  if (loadFromLocalStorage) {
    tasks.value = JSON.parse(loadFromLocalStorage);
  }
});

const onDelete = (id: number) => {
  if (confirm("Are you sure?")) {
    tasks.value = tasks.value.filter((task) => task.id !== id);
    saveToLocalStorage();
    toast.success("Task deleted successfully!");
  }
};

const toggleReminder = (id: number) => {
  tasks.value = tasks.value.map((task) =>
    task.id === id ? { ...task, reminder: !task.reminder } : task
  );
};

const handleTaskAddition = (newTask: TaskProps) => {
  tasks.value.push(newTask);
  saveToLocalStorage();
};

const setShowAddTask = () => {
  showAddTask.value = !showAddTask.value;
};
</script>
<template>
  <div class="container">
    <Header
      :showAddTask="showAddTask"
      :setShowAddTask="setShowAddTask"
      title="Task Tracker"
    />
    <AddTask v-show="showAddTask" @taskAdded="handleTaskAddition" />
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
