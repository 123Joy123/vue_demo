<template>
    <header>
        <h1>{{title}}</h1>
        <Button v-show="homePage" @show-add-task="$emit('show-add-task')" :title="showAddTask ? 'Close': 'Add Task'" :color="showAddTask ? 'red': 'green'"/>
    </header>
</template>

<script>
import Button from './Botton'

export default {
    name:'Header',
    props:{
        title:String,
        showAddTask:Boolean,
    },
    components:{
        Button,
    },
    emits:['show-add-task'],
    computed:{
        homePage(){
            if(this.$route.path==='/'){
                return true
            }
            else{
                return false
            }
        }
    }
}
</script>

<style scoped>
    header{
        display: flex;
        justify-content: space-around;
        align-items: center;
        margin-bottom: 20px;
    }
</style>>