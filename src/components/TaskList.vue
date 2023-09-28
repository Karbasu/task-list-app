<template>
    <div class="container_task_list">
      <h2>Pending Task List</h2>
      <ul class="task_list">
        <li v-for="task in filteredTasks" :key="task.id">
          {{ task.title }}
          <button class="delete_button" @click="deleteTask(task.id)">Delete</button>
          <button class="complete_button" @click="markAsCompleted(task)" v-if="!task.completed">Complete</button>
          <button class="complete_button" @click="markAsProgress(task)" v-if="!task.status">InProgress</button>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    props: ['tasks'],
    methods: {
      deleteTask(taskId) {
        this.$emit('remove-task', taskId);
      },
      markAsCompleted(task) {
        if (!task.completed) {
          task.status = true;
          task.completed = true;
          task.completionTime = new Date().toLocaleString();
        }
      },
      markAsProgress(task) {
        if (!task.completed && !task.status) {
          task.status = true;
          
        }
      },
    },
    computed: {
      filteredTasks() {
        return this.tasks; 
      },
    },
  };
  </script>
  <style>
    .container_task_list{
        display:flex;
        flex-direction: column;
        padding:10px;
        margin-top:20px;
        width:fit-content;
        max-height:450px;
        overflow-y: scroll;
        border:1px solid whitesmoke;
        border-radius:15px;
        box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.2);
    }
    .task_list{
        display: flex;
        flex-direction: column;
        align-self: center;
    }
    .task_list >li{
        padding:10px;
        font-size: 18px;
    }
    .complete_button{
        float:right;
        padding:5px;
        border-radius:15px;
        border:0px;
        margin-left:10px;
        background-color: #007bff;
        color:white;
    }

    .delete_button{
        float:right;
        padding:5px;
        border-radius:15px;
        border:0px;
        margin-left:10px;
        background-color: rgb(225, 62, 62);
        color:white;
    }
    .task_list >li > button:hover{
        transform: scale(1.05);
    }
</style>
  