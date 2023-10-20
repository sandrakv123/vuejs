<template>
    <div class="todo-list">
      <h1>To Do List</h1>
      <div class ="back">
      <ul>
        <li v-for="task in filteredTasks" :key="task.id">
          <input type="checkbox" v-model="task.completed">
          <span>{{ task.description }}</span>
        <input type="text" v-model="task.description" @blur="editTask(task)">
          <button @click="removeTask(task.id)">Remove</button>
        </li>
      </ul>
      <h1><input type="text" v-model="newTask" placeholder="Enter a new task" required></h1>
      <button @click="addTask">Add Task</button>
    
  
      <select v-model="filter">
        <option value="all">All</option>
        <option value="active">Active</option>
        <option value="completed">Completed</option>
      </select>
    </div>
  </div>
  </template>
  
  <script>
  export default {
    name: 'TodoList',
    data() {
      return {
        tasks: [],
        newTask: '',
        filter: 'all'
      }
    },
    computed: {
      filteredTasks() {
        if (this.filter === 'all') {
          return this.tasks
        } else if (this.filter === 'active') {
          return this.tasks.filter(task => !task.completed)
        } else {
          return this.tasks.filter(task => task.completed)
        }
      }
    },
    methods: {
      addTask() {
        this.tasks.push({
          id: Math.random().toString(36).substring(7),
          description: this.newTask,
          completed: false
        })
  
        this.newTask = ''
      },
      removeTask(id) {
        this.tasks = this.tasks.filter(task => task.id !== id)
      },
      editTask(index) {
        const newDescription = prompt('Enter a new description:', this.tasks[index].description);
        if (newDescription !== null && newDescription.trim() !== '') {
          this.tasks[index].description = newDescription;
        }
      },
      }
      
    }

  </script>
  
  <style scoped>
  .todo-list {
    padding: 1rem;
    background-color: lightgray;
    text-align: center;
    width: 40%;
    top: 50%;
    left: 50%;
    font-family: Georgia,Serif;
    min-width: 450px;
    position: absolute;
    min-height: 100px;
    transform: translate(-50%,-50%);
    border-style: solid;
    border-width: 2px;
  }
  
  .todo-list h1 {
    font-size: 2rem;
    font-weight: bold;
  }
  


  .todo-list ul {
    list-style-type: none;
    padding: 0;
  }
  
  .todo-list li {
    margin-bottom: 1rem;
  }
  
  .todo-list input[type="checkbox"] {
    margin-right: 1rem;
  }
  
  .todo-list button {
    margin-left: 1rem;
    margin-right: 1rem;
    font-family: Arial, Helvetica, sans-serif;
  }
  
  .todo-list input[type="text"] {
    width: 100%;

  }

  
</style>