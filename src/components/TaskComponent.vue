<template>
  <div @dblclick="$emit('toggle-reminder', task.id)"
  :class="['task', task.remainder ? 'reminder' : 'set-reminder']">
    <h3>{{ task.text }}
      <i @click="$emit('delete-t',task.id)" class="fas fa-times"></i>
    </h3>
    <p>{{ task.day }}</p>
  </div>
</template>

<script>
  export default {
    name: 'Task',
    props: {
      task: Object
    },
    // emits: ["delete-t"],
    // methods: {
    //   onDelete(id) {
    //     this.$emit('delete-t', id)
    //   }
    // }
  }
</script>

<style scoped>
  .fas {
    color: red;
  }
  .task {
    background: #f4f4f4;
    margin: 5px;
    padding: 10px 20px;
    cursor: pointer;
  }

  .task.reminder {
    border-left: 5px solid palevioletred
  }

  .task h3 {
    display: flex;
    align-items: center;
    justify-content: space-between;

  }

  .task.set-reminder {
    border-left:  5px solid greenyellow
  }
</style>