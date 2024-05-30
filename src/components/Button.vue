<script setup lang="ts">
import { onMounted, ref } from "vue";
defineProps<{
  text?: string;
  color?: string;
}>();
type TaskProps = {
  id: number;
  text: string;
  day: string;
  reminder: boolean;
};
const tasks = ref<TaskProps[]>([]);
onMounted(() => {
  tasks.value = [
    {
      id: 1,
      text: "Doctor's Appointment",
      day: "May 5th at 2:30pm",
      reminder: true,
    },
    {
      id: 2,
      text: "Meeting at School",
      day: "May 6th at 1:30pm",
      reminder: true,
    },
    {
      id: 3,
      text: "Food Shopping",
      day: "May 7th at 12:30pm",
      reminder: false,
    },
  ];
});
</script>

<template>
  <button :style="{ background: color }" class="btn">
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
