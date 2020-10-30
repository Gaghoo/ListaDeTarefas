<template>
    <div class="task-grid">
        <template v-if="tasks.length">
            <Task 
                v-for="(task, i) in tasks" 
                :key="task.name" :task="task"
                @taskDeleted="$emit('taskDeleted', i)"
                @taskStateChanged="$emit('taskStateChanged', i)"
            />
        </template>
        <div class="no-task" v-else>
            <p>Você está sem tarefas pendentes. :D</p>
        </div>
    </div>
</template>

<script>
import Task from './Task'
export default {
    props: {
        tasks: {type: Array, required: true}
    },
    components:{
        Task
    }
}
</script>

<style>
.task-grid{
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
}
.no-task{
    margin: 12px 18px;
    padding: 8px;
    color: #999;
    font-size: 20px;
    font-weight: 700;
    border-radius: 30px;
    box-shadow: 0 0 13px #fff;
}
</style>