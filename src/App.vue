<template>
  <div class="container">
    <Header @toggle-add-task='toggleAddTask' title="Task Tracker"
    :showAddTaskProp="showAddTask"> </Header>
    <div v-show='showAddTask'>
      <AddTask @add-task='addTask'></AddTask>
    </div>
    <Tasks
    @toggle-reminder='toggleReminder' 
    @delete-t="deleteTask" :tasks="tasks"></Tasks>
    <router-view></router-view>
    <Footer></Footer>

  </div>
  
</template>

<script>

import Header from './components/HeaderComponent.vue'
import Footer from './components/FooterComponent.vue'
import Tasks from './components/TasksComponent.vue'
import AddTask from './components/AddTaskComponent.vue'

export default {
  name: 'App',
  components: {
    Header,
    Tasks,
    AddTask,
    Footer
  },
  data() {
    return {
      tasks: [],
      showAddTask : false
    }
  },
  methods: {
    async addTask(newTask){
      const res = await fetch('http://localhost:5000/tasks/',
      {
        method: 'post',
        headers: {
          'content-type': 'application/json'
        },
        body: JSON.stringify(newTask)
        })
      const data = await res.json()
      this.tasks = [...this.tasks, data]
    },
    async deleteTask(id) {
      if(confirm("Are u sure?")){
        const res = await fetch(`http://localhost:5000/tasks/${id}`,{
          method: 'delete',
        })
        res.status === 200 ? this.tasks = this.tasks.filter((task) => task.id !== id ) : 'Error Deleting Task!'
      }
      
    },
    async toggleReminder(id) {
      const taskToToggle = await this.fetchTask(id)
      const updTask = {...taskToToggle, remainder: !taskToToggle.remainder}

      const res = await fetch(`http://localhost:5000/tasks/${id}`,
      {
        method: 'put',
        headers: {
          'content-type': 'application/json'
        },
        body: JSON.stringify(updTask)
      })
      const data = await res.json()
      this.tasks = this.tasks.map((task) => 
        task.id === id ? {...task, remainder: data.remainder } : task)
    },
    toggleAddTask() {
      this.showAddTask = !this.showAddTask;
    },
    async fetchTasks() {
      const res = await fetch('http://localhost:5000/tasks')
      const data = await res.json()
      console.log("invoke fetchtask method...")
      return data
    },
    async fetchTask(id){
      const res = await fetch(`http://localhost:5000/tasks/${id}`)
      const data = await res.json()
      console.log("invoke fetchtask method...")
      return data
    }
  },
  async created() {
    this.tasks = await this.fetchTasks();
  },
  
}
</script>

<style>
  .container {
    /* display: flex; */
    flex-direction: row;
    justify-content: center;
    border: 1px solid grey;
    padding: 20px;

  }
</style>
