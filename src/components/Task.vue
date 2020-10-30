<template>
    <div class="task" :class="stateClass" @click="$emit('taskStateChanged', task)">
        <span @click.stop="$emit('taskDeleted', task)" class="close">x</span>
        <p>{{task.name}}</p>
    </div>
</template>

<script>
export default {
    props:{
        task:{type: Object, required: true}
    },
    computed:{
        stateClass(){
            return{
                pending: this.task.pending,
                done: !this.task.pending
            }
        }
    }
}
</script>

<style>
.task{
    position: relative;
    width: 256px;
    height: 128px;
    margin: 8px 6px;
    padding: 5px 9px;
    border-radius: 10px;
    text-align: center;
    font-size: 20px;
    font-weight: 300;
    cursor: pointer;
    user-select: none;
    display: flex;
    justify-content: center;
    align-items: center;
}
.pending{
    border-left: 12px solid #93291E;
    background-color: #ED213A;
}
.done{
    color: #ccc;
    border-left: 12px solid #0f9b0f;
    background-color: #52c234;
    text-decoration: line-through;
}
.pending .close{
    background-color: #93291E;
}
.done .close{
    background-color: #0f9b0f;
}
.close{
    position: absolute;
    top: 10px;
    right: 10px;
    font-size: 14px;
    font-weight: 600;
    height: 20px;
    width: 20px;
    border-radius: 20px;
}
</style>