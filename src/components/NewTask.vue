<template>
    <div class="add-task">
        <input v-model="name" @keydown.enter="add" type="text" class="form-element" placeholder="Nova Tarefa...">
        <button class="form-element" @click="add">+</button>
    </div>
</template>

<script>
export default {
    data(){
        return{
            name: ''
        }
    },
    methods:{
        add(){
            this.$emit('taskAdded', {name: this.name})
            this.name = ''
        }
    }
}
</script>

<style>
.add-task{
    margin: 35px;
}
.form-element{
    outline: none;
    font-size: 18px;
    border:1px solid #fff;
    padding: 5px 10px 8px;
    color: #fff;
}
.add-task input{
    width: 450px;
    background: #fff2;
    border-top-left-radius: 5px;
    border-bottom-left-radius: 5px;
}
button.form-element{
    border-left: none;
    background-color: #2196f3;
    border-top-right-radius: 5px;
    border-bottom-right-radius: 5px;
}
</style>