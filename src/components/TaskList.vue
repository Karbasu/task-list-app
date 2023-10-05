<template>
    <div class="container_task_list">
      <h2>User Task List</h2>
      <div class="filter-status">
        <label for="status-filter">Filter by Status:</label>
        <select  id="status-filter" v-model="selectedStatus">
          <option value="all">All</option>
          <option v-for="option in statusOptions" :key="option" :value="option">{{ option }}</option>
        </select>
      </div>
      
      <ul class="task_list">
        <li v-for="task in filteredTasks" :key="task.id">
          {{ task.title }}
          <button @click="addCustomStatus(task)">Add Status</button>
          <select name="status-names" v-model="task.status">
            
            <option v-for="option in statusOptions" :key="option" :value="option">{{ option }}</option>
          </select>
          <input class='new-status' v-model="newTaskStatus" placeholder="Add Extra Status" />
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    props: ['tasks', 'statusOptions'],
    data() {
      return {
        newTaskStatus: "",
        selectedStatus: "all", 
      };
    },
    methods: {
      addCustomStatus(task) {
        if (this.newTaskStatus.trim() === "") {
          alert("Status name cannot be empty.");
          return;
        }
        task.status = this.newTaskStatus;
        this.$emit("add-custom-status", this.newTaskStatus);
        this.newTaskStatus = "";
      },
    },
    computed: {
      filteredTasks() {
        if (this.selectedStatus === "all") {
          return this.tasks;
        } else {
          return this.tasks.filter(task => task.status === this.selectedStatus);
        }
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
    .task_list >li > button{
      margin-left: 10px;
      margin-right:5px ;
      border:1px solid #b4d5f8;
      background-color: #d5e1ef;
      border-radius:10px;
      flex:1;
    }
    .task_list >li > select{
      margin-right:5px;
      height:21px;
      border-radius:10px;
      flex:1;
    }
    .task_list >li > button:hover{
        transform: scale(1.05);
    }
    .status-list{
      display:flex;
      flex-direction: row;
      
    }
    .new-status{
      margin-left:5px;
      border-radius:10px;
      flex:1;
    }
    #status-filter{
      margin-left:10px;
      border-radius: 8px;
      background-color: #d5e1ef;
    }
</style>
