<template>
    <div class="todo-list">
      <input
        type="text"
        v-model="newTask"
        placeholder="Add a new task"
      >
      <button @click="addTask">Add</button>
  
      <ul>
        <li v-for="task in tasks" :key="task.id">
          <input
            type="checkbox"
            v-model="task.completed"
          >
          <span :class="{ 'completed-task': task.completed }">{{ task.description }}</span>
          <button @click="removeTask(task.id)">Delete</button>
        </li>
      </ul>
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
          const task = {
            id: this.tasks.length + 1,
            description: this.newTask,
            completed: false
          };
  
          this.tasks.push(task);
          this.newTask = '';
        }
      },
      removeTask(id) {
        this.tasks = this.tasks.filter(task => task.id !== id);
      }
    }
  };
  </script>
  
  <style scoped>
  .todo-list {
    max-width: 400px;
    margin: 0 auto;
    padding: 20px;
  }
  
  .todo-list input[type="text"] {
    width: 100%;
    margin-bottom: 10px;
    padding: 5px;
  }
  
  .todo-list button {
    margin-left: 5px;
  }
  
  .completed-task {
    text-decoration: line-through;
  }
  </style>
  