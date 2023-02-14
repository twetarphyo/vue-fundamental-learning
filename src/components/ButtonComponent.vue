<template>
  <button @click="onClick()" :style="{background: color}">
    {{ text }}
  </button>
</template>

<script>
  export default {
    name: 'Button',
    props: {
      text: String,
      color: String
    },
    methods: {
      onClick() {
        this.$emit('toggle-add-task');
      }
    }
  }
</script>

<style>
  button {
    color: white;
    padding: 10px;
    margin: 10px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }
  
</style>