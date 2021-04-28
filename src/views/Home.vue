<template>
    <AddTask v-show="showAddTask" @add-task="addTask" />
    <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks" />
</template>

<script>
import Tasks from '../components/Tasks'
import AddTask from '../components/AddTask'

export default {
  name: 'App',
  components: {
    Tasks,
    AddTask,
  },
  props:{
      showAddTask:Boolean,
  },
  data(){
    return {
      tasks:[],
    }
  },
  methods:{
    async deleteTask(id){
      const res=await fetch(`api/tasks/${id}`,{
        method:'DELETE',
      })
      // filter滤波器，保留符合当前条件的，比如高通滤波器只有高频率的能通过
      res.status===200 ? (this.tasks=this.tasks.filter((task)=>task.id !== id)) : alert('Error deleting task!')
    },
    async toggleReminder(id){
      const taskToToggle=await this.fetchTask(id)
      const updTask={...taskToToggle,reminder:!taskToToggle.reminder}

      const res= await fetch(`api/tasks/${id}`,{
        method:'PUT',
        headers:{
          'Content-type':'application/json',
        },
        body:JSON.stringify(updTask),
      })
      const data=await res.json()
      // map可以将数组里每个元素都按它的函数处理一边
      // ...后面跟一个对象，该对象的属性除了逗号后面的会被修改，别的都不变
      this.tasks=this.tasks.map((task)=> task.id===id ? {...task,reminder:data.reminder} : task)
    },
    async addTask(task){
      const res=await fetch('api/tasks',{
        method:'POST',
        headers:{
          'Content-type':'application/json',
        },
        body:JSON.stringify(task),
      })
      const data=await res.json() 
      this.tasks=[...this.tasks,data]
    },
    // showAddTaskMethod(){
    //   this.showAddTask=!this.showAddTask
    // },
    async fetchTasks(){
      const res=await fetch('api/tasks')
      const data=await res.json()
      return data
    },
    async fetchTask(id){
      const res=await fetch(`api/tasks/${id}`)
      const data=await res.json()
      return data
    }
  },
  async created(){
    this.tasks=await this.fetchTasks()
    // [
    //   {
    //     id:1,
    //     text:'Doctors Appointment',
    //     day:'March 1st at 2:30pm',
    //     reminder:true,
    //   },
    //   {
    //     id:2,
    //     text:'Meeting at school',
    //     day:'March 3rd at 1:30pm',
    //     reminder:true,
    //   },
    //   {
    //     id:3,
    //     text:'Food shopping',
    //     day:'March 1st at 11:00am',
    //     reminder:false,
    //   }
    // ]
  },
}
</script>