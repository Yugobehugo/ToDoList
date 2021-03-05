<template>
    <form  @submit.prevent="sendTask" id = "newTodo">      
        <input type="text" id = "task" required placeholder="Ajouter une tâche" v-model="valueTask">
        <button >Ajouter</button>
    </form>
</template>

<script>
export default {
    el : '#newTodo',
    name : "newTodo",

    methods: {
        sendTask() { //Affiche une tâche
            if(this.valueTask ) {
                
                this.$emit("new-todo-task", { todoTask: this.valueTask})
                this.valueTask = ""
            }
        }
    },
    data() {
        return {
            valueTask: "", 
        }
    }
}
</script>

<style >

        #task{
        width : 300px;
        height : 50px;
        border : none;
        border-bottom : solid 2px rgb(23, 207, 121);
        text-align : center;
        margin-right : 10px;
    }
    #newTodo button{
        height : 40px;
        width : 100px;
        border : none;
        background :rgb(5, 240, 103);
        border-radius : 10px;
        margin-top : 10px;
        margin-left : 10px;
    }
</style>