<template>
    <div id = "todo-list">
        <ul>
             <li v-for="(task, index) in tasks" v-bind:key="index"> <!-- parcour la liste des tâches -->
                <div>
                    <input type="checkbox" v-bind:checked="task.checked" @change.prevent="taskChecked(index)">
                </div>
                <p :class="{'checked' : task.checked}">{{ task.value }}</p>  <!-- J'ajoute une class "checked" si la tache est cohée  -->
                <button @click="taskDeleted(index)">Delete</button>
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    el : '#todo-list',
    name : 'todoList',

     props:  {
        tasks: Array
    },
    methods: {
        taskChecked(index) { 
            this.$emit('task-check', {index})
        },
        taskDeleted(index) {
            this.$emit('delete-task', {index})
        },
        
    }
}
</script>

<style>
    #todo-list{
        display : flex; 
        width : 100%;
    }
    #todo-list ul {
        display : flex; 
        justify-content : space-evenly;
        width : 100%;
        flex-wrap: wrap;
    }
    ul li{
        display : flex; 
        justify-content: space-between;
        align-items: center;
        width : 70%;

    }
    ul li div{
        display : flex;
        width : 50px;
    }
    ul li p {
        width : 65%;
    }
    ul  li div input{
        width : 30px;
        height : 30px;
        border-radius: 20px;
        border-radius: 50%;
        vertical-align: middle;
        border: 2px solid #ddd;
        -webkit-appearance: none;
        outline: none;
        cursor: pointer;
    }
    ul li div input:checked {
        background: rgb(5, 240, 103);
    }
    .checked{
        text-decoration : line-through; 
    }

    #todo-list button{
        height : 40px;
        width : 100px;
        border : none;
        background :rgb(255, 0, 0);
        border-radius : 10px;
    }
</style>