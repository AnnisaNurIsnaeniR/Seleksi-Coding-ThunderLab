<template>
  <div class="app">
    <h1 class="title">To-Do List</h1>
    <div class="todo-container">
      <div class="input-container">
        <input
          type="text"
          v-model="newTask"
          placeholder="Add a new task"
          @keydown.enter="addTask"
        />
        <button @click="addTask">Add</button>
      </div>
      <ul class="todo-list">
        <li v-for="(task, index) in tasks" :key="index" class="todo-item">
          <input
            type="checkbox"
            v-model="task.completed"
            @change="updateTask(index)"
          />
          <span :class="{ 'completed-task': task.completed }">{{ task.description }}</span>
          <button @click="removeTask(index)" class="delete-button">Delete</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tasks: [],
      newTask: ''
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim() !== '') {
        this.tasks.push({
          description: this.newTask,
          completed: false
        });
        this.newTask = '';
      }
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
    },
    updateTask(index) {
      this.tasks[index].completed = !this.tasks[index].completed;
    }
  }
};
</script>

<style scoped>
.app {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;
}

.title {
  font-size: 24px;
  margin-bottom: 20px;
}

.todo-container {
  width: 100%;
  max-width: 400px;
  background-color: #9AC5F4;
  border-radius: 8px;
  padding: 20px;
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
}

.input-container {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
}

.input-container input {
  flex-grow: 1;
  padding: 10px;
  border: none;
  border-radius: 4px;
  box-shadow: 0px 1px 2px rgba(0, 0, 0, 0.1);
}

.input-container button {
  margin-left: 10px;
  background-color: #94db96;
  color: #131212;
  border: none;
  border-radius: 4px;
  padding: 10px 16px;
  cursor: pointer;
}

.todo-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.todo-item {
  display: flex;
  align-items: center;
  padding: 10px;
  border-bottom: 1px solid #7c94c7;
}

.todo-item:last-child {
  border-bottom: none;
}

.todo-item input[type="checkbox"] {
  margin-right: 10px;
}

.completed-task {
  text-decoration: line-through;
  color: #888;
}

.delete-button {
  background-color: #c46f69;
  color: #fff;
  border: none;
  border-radius: 10px;
  padding: 10px 16px;
  cursor: pointer;
  margin-left: 10px;
}
</style>
