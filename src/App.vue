<template>
  <div class="task_container">
    <h1>Task List WebApp</h1>
    <task-creation @add-task="addTask" />
    <div class="task_pending_completed">
      <task-list :tasks="tasks" @remove-task="removeTask" /> 
    <TaskCompleted :tasks="tasks" />
    <StatusProgress :tasks="tasks"/>
  </div>
      
  </div>
</template>

<script>
import TaskCompleted from "./components/TaskCompleted.vue";
import TaskCreation from "./components/TaskCreation.vue";
import TaskList from "./components/TaskList.vue";
import StatusProgress from "./components/StatusProgress.vue";


export default {
  data() {
    return {
      tasks: [],
    };
  },
  methods: {
    addTask(task) {
      this.tasks.push(task);
    },
    removeTask(id) {
      this.tasks = this.tasks.filter(task => task.id !== id);
    },
  },
  components: {
    TaskCreation,
    TaskList,
    TaskCompleted,
    StatusProgress
},
};
</script>





<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.task_container{
  display:flex;
  flex-direction: column;
  align-items: center;
}
.task_pending_completed{
  display:flex;
  flex-direction: row;
  flex:1;
  padding:10px;
}
</style>
