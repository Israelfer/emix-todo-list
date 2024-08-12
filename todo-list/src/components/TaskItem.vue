<template>
  <div class="task-item">
    <div>
      <label class="custom-checkbox">
        <input type="checkbox" :checked="task.done" @change="toggleDone">
        <span></span>
      </label>
      <span :class="{ done: task.done }">{{ task.name }}</span>
    </div>
    <div class="task-buttons">
      <button @click="editTask" title="Editar">✏️</button>
      <button @click="deleteTask" title="Excluir">🗑️</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TaskItem',
  props: ['task'],
  methods: {
    toggleDone() {
      this.$emit('toggle-done', this.task.id);
    },
    editTask() {
      this.$emit('edit-task', this.task.id);
    },
    deleteTask() {
      this.$emit('delete-task', this.task.id);
    }
  }
};
</script>

<style scoped>
.task-item {
  list-style-type: none;
  display: flex;
  align-items: center;
  justify-content: space-between;
  color: #999;
  margin-bottom: 4px;
}

.task-buttons {
  display: flex;
}

.done {
  text-decoration: line-through;
}

button {
  margin-left: 5px;
  cursor: pointer;
  background-color: transparent;
}

input[type="checkbox"] {
  margin-right: 10px;
  cursor: pointer;
}

.custom-checkbox {
  position: relative;
  display: inline-block;
  width: 16px;
  height: 16px;
  margin: 8px 8px 8px 0;
  cursor: pointer;
}

.custom-checkbox input[type="checkbox"] {
  opacity: 0;
  width: 0;
  height: 0;
}

.custom-checkbox span {
  position: absolute;
  top: 0;
  left: 0;
  height: 13px;
  width: 13px;
  border: 2px solid #7B7B7B;
  background-color: transparent;
  border-radius: 4px;
}

.custom-checkbox input[type="checkbox"]:checked + span {
  background-color: #7B7B7B;
}

.custom-checkbox input[type="checkbox"]:checked + span::after {
  content: "";
  position: absolute;
  left: 4px;
  top: 1px;
  width: 4px;
  height: 9px;
  border: solid white;
  border-width: 0 2px 2px 0;
  transform: rotate(45deg);
}
</style>