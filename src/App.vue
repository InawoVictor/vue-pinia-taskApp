<template>
  <main>

  <header>
    <img src="./assets/pinia-logo.svg" alt="Pinia Logo">
    <h1>Pinia Store</h1>
  </header>


  <!-- Add Task -->
  <div class="new-task-form">
    <TaskForm />
  </div>


  <!-- Filter Buttons -->
  <nav class="filter">
    <button @click="filter = 'all'">View All Tasks</button>
    <button @click="filter = 'favs'">View Favourite Tasks</button>
  </nav>

<!-- Loading -->
<div class="loading" v-if="isLoading">Loading tasks...</div>

  <!-- Task List -->
  <div class="task-list" v-if="filter === 'all'">
    <p>You have {{ totalCount }} tasks left to do.</p>
    <div v-for="task in tasks" :key="task.id">
      <TaskCardVue :task="task"/>
    </div>
  </div>

  <div class="task-list" v-if="filter === 'favs'">
    <p>You have {{ favCount }} favs left to do.</p>
    <div v-for="task in favs" :key="task.id">
      <TaskCardVue :task="task"/>
    </div>
  </div>

  <button @click="taskStore.$reset">reset state</button>
  </main>  
</template>
 

<script setup>
import { ref } from "vue";
import TaskCardVue from "./components/TaskCard.vue";
import {useTaskStore} from "./stores/TaskStore";
import TaskForm from "./components/TaskForm.vue";
import { storeToRefs } from "pinia";

const taskStore = useTaskStore();
const {totalCount,favCount, favs, isLoading, tasks } = storeToRefs(taskStore)

taskStore.getTasks()
  
  
  const filter = ref("all")

</script>


