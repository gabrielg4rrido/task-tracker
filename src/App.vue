<template>
  <div class="container">
    <Header @show-add-task="toggleAddTask" title="Task Tracker" :showAddTask="showAddTask"/>
    <div v-if="showAddTask">
      <AddTask @add-task="addTask" /> 
    </div>
    <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks"/>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Tasks from './components/Tasks.vue'
import AddTask from './components/AddTask.vue'

export default {
  name: 'App',
  components: {
      Header,
      Tasks,
      AddTask
   },

   methods: {
     addTask(task){
       this.tasks.push(task)
     },

     deleteTask(id) {
       if(confirm('Are you sure?')){
         this.tasks = this.tasks.filter(task => task.id !==  id)
       }
     },

     toggleAddTask(){
       this.showAddTask = !this.showAddTask
     },

     toggleReminder(id){
       this.tasks = this.tasks.map(task => task.id === id ? {...task, reminder: !task.reminder} : task)
     }
   },

   data() {
     return {
       tasks: [],
       showAddTask: false
     }

   },

   created() {
     this.tasks = [
       {
         id: 1,
         text: 'Dentist',
         day: 'March 1st at 2:30pm',
         reminder: true
       },
       {
         id: 2,
         text: 'Class',
         day: 'March 2st at 2:30pm',
         reminder: true
       },
       {
         id: 3,
         text: 'Football',
         day: 'March 7st at 2:30pm',
         reminder: false
       },
     ]
   }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Poppins', sans-serif;
  background-color: black;
}

h1, label {
  color: white;
}

.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
  border: 1px solid steelblue;

}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>
