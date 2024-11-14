<script setup>
import { onMounted, ref } from "vue";


const url = "https://jsonplaceholder.typicode.com/todos"

const name = ref("John Doe");
const status = ref("active");
const tasks = ref(["Task One", "Task Two", "Task Three"]);
const newTask = ref("");
const toggleStatus = () => {
  switch (status.value) {
    case "active":
      status.value = "pending";
      break;
    case "pending":
      status.value = "inactive";
      break;
    default:
      status.value = "active";
  }
};

const addTask = () => {
  if (newTask.value) {
    tasks.value.push(newTask.value);
    newTask.value = "";
  }
};

const deleteTask = (index) => {
  tasks.value.splice(index, 1);
};

onMounted(async () => {
  try {
    const response = await fetch(url);
    const data = await response.json();
    tasks.value = data.map((task) => task.title);
  } catch (error) {
    console.error(error);
  }
})
</script>


<template>
  <h1>{{ name }}</h1>
  <p v-if="status === 'active'">User is active</p>
  <p v-else-if="status == 'pending'">User is pending</p>
  <p v-else>User is inactive</p>

  <form @submit.prevent="addTask">
    <label for="newTask">Add Task</label>
    <input type="text" id="newTask" name="newTask" v-model="newTask" />
    <button type="submit">Submit</button>
  </form>

  <h3>Tasks:</h3>
  <ul>
    <li v-for="(task, index) in tasks" :key="task">
      <span>
        {{ task }}
      </span>
      <button @click="deleteTask(index)">Delete</button>
    </li>
  </ul>
  <br />
  <!-- <button v-on:click="toggleStatus">Change Status</button> -->
  <button @click="toggleStatus">Change Status</button>
</template>
