<template>
  <div class="container">
  <Header title="Task Tracker" @toggle-add-task="toggleAddTask"/>
  <hr>
  <div v-if="showAddTask">
  <AddTask @add-task="addTask"/>
  </div>

  <hr>
  <Tasks :tasks="tasks" @delete-task="deleteTask"/>
  </div>
</template>
<script>
import Header from './components/Header'
import Tasks from './components/Tasks'
import AddTask from './components/AddTask'
export default {
  name: 'App',
  components: {
  Header,Tasks,AddTask
},
 data(){
   return{
     tasks: [],
     showAddTask:false
   }
 },
 methods:{
    toggleAddTask(){
     this.showAddTask = !this.showAddTask
   },
   addTask(task){
     this.tasks = [...this.tasks, task]
   },
   deleteTask(id){
     this.tasks = this.tasks.filter((task)=>task.id !== id)
   },

   async fetchTasks(){
     const res = await fetch('http://localhost:5000/tasks')
     const data = await res.json()
     return data
   },
 },
 async created(){
  this.tasks = await this.fetchTasks()
},
}
</script>

<style>
@import url('<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Crimson+Pro&family=Literata">');
*{
  margin:0;
  padding:0;
  box-sizing: border-box;
}
body{
  font-family: 'Crimson Pro', serif;
}
.container{
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.btn{
  display: inline-block;
  background: #000;
  color: #fff;
  padding:10px 20px;
  margin:5px;
  border-radius : 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family:inherit;

}
</style>
