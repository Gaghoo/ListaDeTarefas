<template>
    <div id="app">
        <h1>Tarefas</h1>
        <TaskProgress :progress="progress"/>
        <NewTask @taskAdded="addTask"/>
        <TasksGrid :tasks="tasks" 
            @taskDeleted="deleteTask" 
            @taskStateChanged="toggleTaskState"
        />
    </div>
</template>

<script>
import TaskProgress from './components/TaskProgress'
import TasksGrid from './components/TasksGrid'
import NewTask from './components/NewTask'

export default {
    name: 'App',
    data() {
        return{
        tasks:[]
        }
    },
    created(){
        const json = localStorage.getItem('tasks')
        const array = JSON.parse(json)
        this.tasks = Array.isArray(array) ? array : []
    },
    methods:{
        addTask(task){
            const sameName = t => t.name === task.name
            const reallyNew = this.tasks.filter(sameName).length == 0
            if (reallyNew) {
                this.tasks.push({
                    name: task.name,
                    pending: task.pending || true
                })
            }
        },
        deleteTask(i){
            this.tasks.splice(i, 1)
        },
        toggleTaskState(i){
            this.tasks[i].pending = !this.tasks[i].pending
        }
    },
    computed:{
        progress(){
            const total = this.tasks.length
            const done = this.tasks.filter(t => !t.pending).length
            return Math.round(done / total * 100) || 0
        }
    },
    watch:{
        tasks:{
            deep: true,
            handler(){
                localStorage.setItem('tasks', JSON.stringify(this.tasks))
            }
        }
    },
    components: {
        TasksGrid,
        NewTask,
        TaskProgress
    },
}
</script>

<style>
body{
    font-family: 'Courier New', Courier, monospace;
    background: linear-gradient(to bottom, #000000, #434343);
    color: #fff;
}
#app {
    display: flex;
    flex: 1;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 100vh;
}
#app h1{
    margin: 5px 10px;
    font-weight: 300;
    font-size: 3rem;
}
</style>
