<script>
  export default {
    data() {
      return {
        name: 'John Doe',
        status: 'active',
        tasks: ['Task One', 'Task Two', 'Task Three'],
        link: 'https://google.com'
      }
    },
    methods: {
      toggleStatus() {
        switch (this.status) {
          case 'active':
            this.status = 'pending'
            break
          case 'pending':
            this.status = 'inactive'
            break
          default:
            this.status = 'active'
        }
      }
    }
  }
</script>

<template>
  <h1>{{ name }}</h1>
  <p v-if="status === 'active'">User is active</p>
  <p v-else-if="status == 'pending'">User is pending</p>
  <p v-else="status">User is inactive</p>

  <h3>Tasks:</h3>
  <ul>
    <li v-for="task in tasks" :key="task">{{ task }}</li>
  </ul>
  <!-- <a v-bind:href="link">Click for Google</a> -->
  <a :href="link">Click for Google</a>
  <br/>
  <!-- <button v-on:click="toggleStatus">Change Status</button> -->
  <button @click="toggleStatus">Change Status</button>
</template>