<template>
<form @submit.prevent="onSubmit">
  <div class="input-form">
    <div class="input">
      <span class="label">Add Task</span>
      <input type="text" class="type-1" name="text" v-model="text" />
    </div>
    <div class="input">
      <span class="label">Day and Time</span>
      <input type="text" class="type-1" name="day" v-model="day" />
    </div>
    
  </div>
  <div class="chbox-form">
    <label class="chbox-label">Set reminder
    <input type="checkbox" name="reminder" v-model="reminder"/>
    <span></span>
    </label>
  </div>

  <input type="submit" class="button-62" role="button" value="submit">
  <!-- HTML !-->
  

  
</form>

    
</template>

<script>
  export default {
    name: 'AddTask',
    data() {
      return {
        text: '',
        day: '',
        reminder: false,
      }
    },
    methods: {
      onSubmit() {
        
        if(!this.text){
          alert('Please add a task')
          return
        }

        const newTask = {
          id : Math.floor(Math.random() * 100000),
          text : this.text,
          day : this.day,
          remainder : this.reminder
        }

        console.log(newTask);

        this.$emit('add-task', newTask)

        this.text = ''
        this.day  = ''
        this.reminder = false

      }
    },

  }
</script>

<style scoped>
.input {
  margin-bottom: 10px;
}
  * {
    box-sizing: border-box;
  }
  input {
    display:block;
    margin:(0,10,50,10);
    padding:10px;
  }
  .type-1 {
    border-radius:10px;
    border: 1px solid #eee;
    transition: .3s border-color;
  }
  .type-1:hover {
    border: 1px solid #aaa;
  }
  .label {
    margin-top: 100px;
    font-weight: 600;
  }
  label {
    position: relative; /* to contain absolute elements */
    padding-left:30px; /* free space for custom checkbox */
    cursor: pointer;
  }
  /* hide default checkbox  */
  label input[type=checkbox] {
    position: absolute; /* prevent taking any space */
    /* cross-browser hidingg */
    opactiy: 0;
    width:0; 
    height:0;
  }
  /* custom checkbox */
  label span {
    position: absolute;
    /* position to the free space in <label> */
    top:0;
    left:0;
    width:20px; 
    height:20px;
    background-color: #ddd;
    transition: .3s background-color; /* slight transition */
  }
  /* the check icon */
  label span:after {
    content: "";
    position: absolute;
    display: none;
  
    /* check icon */
    left: 6px;
    top: 2px;
    width: 4px;
    height: 10px;
    border: solid white;
    border-width: 0 3px 3px 0;
    transform: rotate(45deg);
  }
  label:hover span {
    background-color: #ccc;
  }

  /**** Here's the trick ***/
  label input:checked ~ span {
    background-color: #2eaadc;
  }
  label input:checked ~ span:after {
    display:block;
  }
  .input-form,.chbox-form {
    margin-bottom: 10px;
    
  }
  /* CSS */
  .button-62 {
    background: linear-gradient(to bottom right, #EF4765, #FF9A5A);
    border: 0;
    border-radius: 12px;
    color: #FFFFFF;
    cursor: pointer;
    display: inline-block;
    font-family: -apple-system,system-ui,"Segoe UI",Roboto,Helvetica,Arial,sans-serif;
    font-size: 15px;
    font-weight: 500;
    line-height: 2.2;
    outline: transparent;
    padding: 0 1rem;
    text-align: center;
    text-decoration: none;
    transition: box-shadow .2s ease-in-out;
    user-select: none;
    -webkit-user-select: none;
    touch-action: manipulation;
    white-space: nowrap;
    margin: 5px 0 15px 0;
  }

  .button-62:not([disabled]):focus {
    box-shadow: 0 0 .25rem rgba(0, 0, 0, 0.5), -.125rem -.125rem 1rem rgba(239, 71, 101, 0.5), .125rem .125rem 1rem rgba(255, 154, 90, 0.5);
  }

  .button-62:not([disabled]):hover {
    box-shadow: 0 0 .25rem rgba(0, 0, 0, 0.5), -.125rem -.125rem 1rem rgba(239, 71, 101, 0.5), .125rem .125rem 1rem rgba(255, 154, 90, 0.5);
  }
</style>