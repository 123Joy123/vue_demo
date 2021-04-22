<template>
    <header>
        <h1>{{title}}</h1>
        <Button title="Add Task" color="green"/>
    </header>
</template>

<script>
import Button from './Botton'

export default {
    name:'Header',
    props:{
        title:String,
    },
    components:{
        Button,
    },
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