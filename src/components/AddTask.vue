<script setup lang="ts">
import { ref } from "vue";
import { useToast } from "vue-toastification";
import { format } from "date-fns";

const toast = useToast();
const emit = defineEmits(["taskAdded"]);
const text = ref("");
const day = ref(null);
const reminder = ref(false);

const onSubmit = () => {
  if (!text.value || !day.value) {
    toast.error("Please fill in all fields");
  } else {
    const formattedDay = format(day.value, "MMMM do', at' h:mma"); // Format datetime

    const newTask = {
      id: Math.floor(Math.random() * 10000) + 1,
      text: text.value,
      day: formattedDay,
      reminder: reminder.value,
    };
    toast.success("Task added successfully");
    emit("taskAdded", newTask);

    text.value = "";
    day.value = null;
    reminder.value = false;
  }
};
</script>

<template>
  <form @submit.prevent="onSubmit" class="add-form">
    <h2>Add Task</h2>
    <div class="form-control">
      <label>Task</label>
      <input
        type="text"
        name="text"
        v-model="text"
        placeholder="Enter the Task here..."
      />
    </div>
    <div class="form-control">
      <label>Day & Time</label>
      <input
        type="datetime-local"
        v-model="day"
        name="day"
        placeholder="Add Day & Time"
      />
    </div>
    <div class="form-control-check">
      <input type="checkbox" name="reminder" v-model="reminder" />
      <label>Set Reminder</label>
    </div>
    <input type="submit" value="Save Task" class="btn btn-block" />
  </form>
</template>

<style scoped>
.add-form {
  width: 28rem;
  margin: 20px 0;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

h2 {
  text-align: center;
}

.form-control {
  margin: 10px 0;
}

.form-control label {
  display: block;
  font-weight: bold;
}

.form-control input {
  width: 100%;
  padding: 5px;
  border: 1px solid #ccc;
  border-radius: 4px;
  outline: none;
}

.form-control-check input {
  width: auto;
  margin-right: 10px;
}

.btn {
  display: block;
  width: 100%;
  padding: 10px;
  margin-top: 10px;
  background: #333;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
</style>
