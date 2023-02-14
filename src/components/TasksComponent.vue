<template>
  <div v-for="task in tasks" :key='task.id'>
    <Task 
    @toggle-reminder="$emit('toggle-reminder',task.id)"
    @delete-t="onDeleteParent(task.id)" :task="task"></Task>
  </div>
</template>

<script>
  import Task from './TaskComponent.vue'
  export default {
    name: "Tasks",
    props: {
      tasks: Array
    },
    components: {
      Task
    },
    emits: ['delete-t','toggle-reminder'],
    methods: {
      onDeleteParent(id) {
        this.$emit('delete-t', id)
      }
    }

  }
</script>