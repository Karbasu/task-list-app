<template>
    <div class="completed-task-container">
      <h2>Completed Tasks</h2>
      <ul class="completed-task-list">
        <li v-for="task in completedTasks" :key="task.id">
          {{ task.title }} (Completed at: {{ task.completionTime }})
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    props: ['tasks'],
    computed: {
      completedTasks() {
        return this.tasks.filter(task => task.completed);
      },
    },
  };
  </script>
  
  <style>
  .completed-task-container {
    display:flex;
    flex-direction: column;
    padding:10px;
        margin-top:20px;
        margin-left:30px;
        width:fit-content;
        max-height:450px;
        overflow-y: scroll;
        border:1px solid whitesmoke;
        border-radius:15px;
        box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.2);
  }
  
  .completed-task-list {
    display: flex;
        flex-direction: column;
        align-self: center;
        font-size: 18px;
        
  }
  .completed-task-list > li{
    padding:10px;
  }
  </style>
  