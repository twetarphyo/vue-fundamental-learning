<template>
  <header>
    <h1>{{ title }}</h1>
    <Button @toggle-add-task="this.$emit('toggle-add-task')"
    :text="showAddTaskProp ? 'Close' :'Add Task' " :color="showAddTaskProp ? '#F55050' : '#54B435'" />
  </header>
</template>

<script>
  import Button from './ButtonComponent.vue'
  export default {
    name: 'Header',
    props: {
      title : String,
      showAddTaskProp: Boolean
    },
    components: {
      Button
    } 
  }
</script>

<style scoped>
  header {
    display: flex;
    justify-content: center;
    align-items: center;
    margin-bottom: 20px;
  }

</style>