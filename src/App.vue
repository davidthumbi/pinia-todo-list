<template>
  <main>
    <header>
      <img src="./assets/pinia.svg" alt="pinia logo" />
      🍍
      <h1>Pinia Tasks</h1>
    </header>

    <div class="new-task-form">
      <TaskForm />
    </div>

    <nav class="filter">
      <button @click="filter = 'all'">All tasks</button>
      <button @click="filter = 'favs'">Fav tasks</button>
    </nav>

    <div class="loading" v-if="taskStore.loading">Loading...</div>

    <div class="task-list" v-if="filter === 'all'">
      <p>You have {{ taskStore.totalCount }} tasks left to do</p>
      <div v-for="task in taskStore.tasks">
        <TaskDetails :task="task"/>
      </div>
    </div>

    <div class="task-list" v-if="filter === 'favs'">
      <p>You have {{ taskStore.favCount }} favorite tasks</p>
      <div v-for="task in taskStore.favs">
        <TaskDetails :task="task"/>
      </div>
    </div>

    <div class="reset">
      <button class="btn" @click="taskStore.$reset">Reset Tasks</button>
    </div>
  </main>
</template>

<script>
import { ref } from 'vue'
import TaskForm from './components/TaskForm.vue'
import TaskDetails from './components/TaskDetails.vue'
import { useTaskStore } from "./stores/TaskStore";

export default {
  components: { TaskForm,TaskDetails },
  setup() {
    const taskStore = useTaskStore();



    taskStore.getTasks()

    const filter = ref('all')

    return { taskStore, filter };
  },
};
</script>
