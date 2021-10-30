<template>
  <form class="add-form" @submit="OnSubmit">
   <div class="form-control">
   <label for="task">Task</label>
   <input type="text" name="text" v-model="text" placeholder="Add task" class="form-control">
   </div>
   <div class="form-control">
   <label for="day">Day And Time</label>
   <input type="text" name="day" v-model="day" placeholder="Add Day And Time" class="form-control">
   </div>
   <div class="form-control form-control-check">
   <label for="reminder">Set Reminder</label>
   <input type="checkbox" name="reminder" v-model="reminder" class="form-control">
   </div>
   <div class="form-control">
    <input type="submit" class="btn btn-block" value="Submit Task">
   </div>
 </form>
</template>
<script>

export default {
  name: 'AddTask',
  data(){
    return{
      text:'',
      day:'',
      reminder:false
    }
  },
  methods:{
    OnSubmit(e){
      e.preventDefault()
      if(!this.text){
        alert('Please add a task')
        return
      }

      const newTask = {
        id: Math.floor(Math.random()*100000),
        text: this.text,
        day: this.day,
        reminder: this.reminder
      }
      this.$emit('add-task',newTask)

      this.text = ''
      this.day = ''
      this.reminder = false
    }
  }
}
</script>
<style scoped>
.add-form{
  margin:40px;
}
.form-control{
  margin:20px 0;
}
.form-control label{
  display: block;
}
.form-control input{
  width:100%;
  height:40px;
  margin:5px;
  padding:3px 7px;
  font-size:14px;
}
.form-control-check{
  display:flex;
  align-items:center;
  justify-content:space-between;
}
.form-control-check label{
  flex: 1;
}
.form-control-check input{
  flex: 2;
  height: 20px;
}
button{
  width:350px;
}
</style>
