<template>
<div :key="task.id" v-for="task in tasks">
 <Task :task="task" @delete-task="$emit('delete-task',task.id)"/>
</div>
</template>

<script>
import Task from './Task'
export default {
  name: 'Tasks',
  components: {
     Task
   },
  props:{
   tasks: Array
 },
 emits:['delete-task']
}
</script>
<style scoped>

</style>
