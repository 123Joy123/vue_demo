<template>
  <div class="container">
    <Header title="Task Tracker" />
    <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks" />
  </div>
  
</template>

<script>
import Header from './components/Header'
import Tasks from './components/Tasks'

export default {
  name: 'App',
  components: {
    Header,
    Tasks,
  },
  data(){
    return {
      tasks:[],
    }
  },
  methods:{
    deleteTask(id){
      // filter滤波器，保留符合当前条件的，比如高通滤波器只有高频率的能通过
      this.tasks=this.tasks.filter((task)=>task.id !== id);
      console.log('task',id);
    },
    toggleReminder(id){
      // map可以将数组里每个元素都按它的函数处理一边
      // ...后面跟一个对象，该对象的属性除了逗号后面的会被修改，别的都不变
      this.tasks=this.tasks.map((task)=> task.id===id ? {...task,reminder: !task.reminder} : task);
    }
  },
  created(){
    this.tasks=[
      {
        id:1,
        text:'Doctors Appointment',
        day:'March 1st at 2:30pm',
        reminder:true,
      },
      {
        id:2,
        text:'Meeting at school',
        day:'March 3rd at 1:30pm',
        reminder:true,
      },
      {
        id:3,
        text:'Food shopping',
        day:'March 1st at 11:00am',
        reminder:false,
      }
    ]
  },
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Poppins', sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>
