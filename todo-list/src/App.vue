<template>
  <div id="app">
    <AppHeader />
    <main>
      <div class="type-task">
        <input v-model="newTask" placeholder="Digite aqui uma nova tarefa..." @keyup.enter="addTask">
        <button @click="addTask" title="Adicionar tarefa">Adicionar</button>
      </div>
      <TaskList :tasks="tasks" @toggle-done="toggleDone" @edit-task="editTask" @delete-task="deleteTask"/>
    </main>
  </div>
</template>

<script>
import AppHeader from './components/AppHeader.vue';
import TaskList from './components/TaskList.vue';

export default {
  name: 'App',
  components: {
    AppHeader,
    TaskList
  },
  data() {
    return {
      newTask: '',
      tasks: JSON.parse(localStorage.getItem('tasks')) || []
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim() === '') return;
      this.tasks.push({
        id: Date.now(),
        name: this.newTask,
        done: false
      });
      this.newTask = '';
      this.saveTasks();
    },
    toggleDone(taskId) {
      const task = this.tasks.find(task => task.id === taskId);
      if (task) task.done = !task.done;
      this.saveTasks();
    },
    editTask(taskId) {
      const taskName = prompt('Edite a tarefa:', this.tasks.find(task => task.id === taskId).name);
      if (taskName) {
        const task = this.tasks.find(task => task.id === taskId);
        task.name = taskName;
        this.saveTasks();
      }
    },
    deleteTask(taskId) {
      this.tasks = this.tasks.filter(task => task.id !== taskId);
      this.saveTasks();
    },
    saveTasks() {
      localStorage.setItem('tasks', JSON.stringify(this.tasks));
    }
  }
};
</script>

<style>
body {
  background-color: cadetblue;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 800px;
  background-color: #F5F5F5;
  padding-bottom: 8px;
  margin: 16px auto 0;
}

.type-task {
  margin: 0 16px;
}

.type-task input,
button {
  padding: 8px;
  border: none;
}

.type-task input {
  width: 636px;
  font-style: italic;
  padding-left: 16px;
}

.type-task button {
  background-color: #36AFD1;
  color: #fff;
  border: none;
  text-transform: uppercase;
  font-weight: bold;
  padding: 8px 16px;
  cursor: pointer;
  border-radius: 4px;
}

.type-task button:hover {
  opacity: 0.7;
  transition: 1s
}
</style>