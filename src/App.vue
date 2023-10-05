<template>
  <div class="task_container">
    <h1>Task List WebApp</h1>
    <task-creation @add-task="addTask" />
    <div class="task_pending_completed">
      <task-list :tasks="tasks" :statusOptions="statusOptions" @add-custom-status="addGlobalStatus" @remove-task="removeTask" /> 
    </div>
  </div>
</template>

<script>
import TaskCreation from "./components/TaskCreation.vue";
import TaskList from "./components/TaskList.vue";

export default {
  data() {
    return {
      tasks: [],
      statusOptions: ["pending", "progress", "completed"],
    };
  },
  methods: {
    addTask(task) {
      this.tasks.push(task);
    },
    removeTask(id) {
      this.tasks = this.tasks.filter(task => task.id !== id);
    },
    addGlobalStatus(newStatus) {
      if (!this.statusOptions.includes(newStatus)) {
        this.statusOptions.push(newStatus);
      }
    },
  },
  components: {
    TaskCreation,
    TaskList,
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
.task_container {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.task_pending_completed {
  display: flex;
  flex-direction: row;
  flex: 1;
  padding: 10px;
}
</style>