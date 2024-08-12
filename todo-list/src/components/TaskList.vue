<template>
  <section class="task-list">
    <div>
      <h3>A Fazer</h3>
      <div v-if="tasksToDo.length === 0" class="empty-message">
        Seu tempo é valioso, organize sua lista de tarefas.
      </div>
      <ul>
        <li v-for="task in tasksToDo" :key="task.id">
          <TaskItem :task="task" @toggle-done="toggleDone" @edit-task="editTask" @delete-task="deleteTask" />
        </li>
      </ul>
    </div>
    <div>
      <h3>Feito</h3>
      <div v-if="tasksDone.length === 0" class="empty-message">
        Selecione uma tarefa para concluí-la!
      </div>
      <ul>
        <li v-for="task in tasksDone" :key="task.id">
          <TaskItem :task="task" @toggle-done="toggleDone" @edit-task="editTask" @delete-task="deleteTask" />
        </li>
      </ul>
    </div>
  </section>
</template>

<script>
import TaskItem from './TaskItem.vue';

export default {
  name: 'TaskList',
  components: { TaskItem },
  props: ['tasks'],
  computed: {
    tasksToDo() {
      return this.tasks.filter(task => !task.done);
    },
    tasksDone() {
      return this.tasks.filter(task => task.done);
    }
  },
  methods: {
    toggleDone(taskId) {
      this.$emit('toggle-done', taskId);
    },
    editTask(taskId) {
      this.$emit('edit-task', taskId);
    },
    deleteTask(taskId) {
      this.$emit('delete-task', taskId);
    }
  }
};
</script>

<style scoped>
section {
  margin: 0 16px 32px;
  display: flex;
  flex-direction: column;
  gap: 16px;
}

h3 {
  color: #006A6A;
  text-transform: uppercase;
  margin: 16px 0 8px;
}

.empty-message {
  font-style: italic;
  color: #36AFD1;
  margin-bottom: 10px;
}

ul {
  list-style-type: none;
  margin: 0;
}

li {
  margin-left: -40px;
  border-bottom: 1px solid #dddddd;
}

li:last-child {
  border-bottom: none;
}
</style>