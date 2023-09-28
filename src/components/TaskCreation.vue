<template>
  <div class="task_creation">
    <h2>Create New Task</h2>
    <input v-model="newTaskTitle" placeholder="Task title" />
    <div class="status_boutton">
      <button @click="selectStatus('pending')" :class="{ active: selectedStatus === 'pending' }">Pending</button>
      <button @click="selectStatus('progress')" :class="{ active: selectedStatus === 'progress' }">Progress</button>
      <button @click="selectStatus('completed')" :class="{ active: selectedStatus === 'completed' }">Completed</button>
    </div>
    <button @click="addTask">Add Task</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTaskTitle: '',
      selectedStatus: '', // No default status selected initially
    };
  },
  methods: {
    selectStatus(status) {
      this.selectedStatus = status;
    },
    addTask() {
      if (this.newTaskTitle.trim() === '') {
        alert('Task title cannot be empty.');
        return;
      }
      if (this.selectedStatus === '') {
        alert('Please choose a status for the task.');
        return;
      }
      const newTask = {
        id: Date.now(),
        title: this.newTaskTitle,
        completed: this.selectedStatus === 'completed',
        status: this.selectedStatus === 'progress',
        completionTime: this.selectedStatus === 'completed' ? new Date().toLocaleString() : null,
      };
      this.$emit('add-task', newTask);
      this.newTaskTitle = '';
      this.selectedStatus = ''; // Reset status after adding the task
    },
  },
};
</script>
<style>
.task_creation{
  display:flex;
  flex-direction: column;
  padding:10px;
  width:500px;
  align-items: center;
  border-radius:15px;
  box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.2);
}
.task_creation > input{
  width:250px;
  padding:10px;
  margin-bottom:10px;
  align-self:center;
  border-radius:15px;
  border:1px solid whitesmoke;
  background-color: white;
  box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.5);
}
.task_creation > button{
   width:80px;
   padding:6px;
   align-self: center;
   margin-top:10px;
   border-radius: 15px;
   border:0px;
   background-color:#007bff;
   color:white;
}
.task_creation > button:hover{
  transform: scale(1.05);
}
</style>
<style>
.task_creation{
  display:flex;
  flex-direction: column;
  padding:10px;
  width:500px;
  align-items: center;
  border-radius:15px;
  box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.2);
}
.task_creation > input{
  width:250px;
  padding:10px;
  margin-bottom:10px;
  align-self:center;
  border-radius:15px;
  border:1px solid whitesmoke;
  background-color: white;
  box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.5);
}
.task_creation > button{
   width:80px;
   padding:6px;
   align-self: center;
   margin-top:10px;
   border-radius: 15px;
   border:0px;
   background-color:#007bff;
   color:white;
}
.task_creation > button:hover{
  transform: 
  scale(1.05);
}
.status_boutton{
  display: flex;
  flex-direction: row;
}
.status_boutton > button{
  padding :2px;
  margin-left:5px;
  border-radius: 10px;
  border:1px solid whitesmoke;
}
</style>
