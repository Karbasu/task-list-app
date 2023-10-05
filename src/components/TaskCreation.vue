<template>
  <div class="task_creation">
    <h2>Create New Task</h2>
    <input v-model="newTaskTitle" placeholder="Task title" />
    
    <button @click="addTask">Add Task</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTaskTitle: "",
       
    };
  },
  methods: {
    
    addTask() {
      if (this.newTaskTitle.trim() === "") {
        alert("Task title cannot be empty.");
        return;
      }
      

      const newTask = {
        id: Date.now(),
        title: this.newTaskTitle,
        completionTime:
          this.selectedStatus === "completed"
            ? new Date().toLocaleString()
            : null,
      };

      this.$emit("add-task", newTask);
      this.newTaskTitle = "";
     
    },
  },
};
</script>
<style>
.task_creation {
  display: flex;
  flex-direction: column;
  padding: 10px;
  width: 500px;
  align-items: center;
  border-radius: 15px;
  box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.2);
}
.task_creation > input {
  width: 250px;
  padding: 10px;
  margin-bottom: 10px;
  align-self: center;
  border-radius: 15px;
  border: 1px solid whitesmoke;
  background-color: white;
  box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.5);
}
.task_creation > button {
  width: 80px;
  padding: 6px;
  align-self: center;
  margin-top: 10px;
  border-radius: 15px;
  border: 0px;
  background-color: #007bff;
  color: white;
}
.task_creation > button:hover {
  transform: scale(1.05);
}
</style>
<style>
.task_creation {
  display: flex;
  flex-direction: column;
  padding: 10px;
  width: 500px;
  align-items: center;
  border-radius: 15px;
  box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.2);
}
.task_creation > input {
  width: 250px;
  padding: 10px;
  margin-bottom: 10px;
  align-self: center;
  border-radius: 15px;
  border: 1px solid whitesmoke;
  background-color: white;
  box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.5);
}
.task_creation > button {
  width: 80px;
  padding: 6px;
  align-self: center;
  margin-top: 10px;
  border-radius: 15px;
  border: 0px;
  background-color: #007bff;
  color: white;
}
.task_creation > button:hover {
  transform: scale(1.05);
}
.status_boutton {
  display: flex;
  flex-direction: row;
}
.status_boutton > button {
  padding: 2px;
  margin-left: 5px;
  border-radius: 10px;
  border: 1px solid whitesmoke;
}
</style>
