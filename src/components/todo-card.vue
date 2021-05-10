<template>
    <div id = "todo-card">
        <header class="card--header">
            <p>{{ date }}</p>
            <h1>VueJs Tutorial ToDo List</h1>
             <p v-if="nbTasks <=1" >{{ nbTasks }} Tâche</p> <!-- Si il ya 0 ou 1 tache, "tache" ne prend pas de "s" -->
            <p v-if="nbTasks >1" >{{ nbTasks }} Tâches</p> <!-- Si il ya 2 tâches ou plus, "taches" prend un "s" -->
            <p>Tâches</p>
            
        </header>
        
            <new-todo @new-todo-task="saveTask" ></new-todo>
            <todo-list 
            v-bind:tasks="tasks" 
            @delete-task="taskDeleted" 
            @task-check="taskChecked" >
            </todo-list>
    </div>
</template>

<script type ="text/javascript">
import newTodo from './new-todo.vue'
import todoList from './todo-list.vue'

export default {
  name: 'todoCard',
  
  methods: { // Enregistre une tâche une tâche
        saveTask(task) {
            const newTask = {value: task.todoTask, checked: false}
            this.tasks = [...this.tasks, newTask]
        },
        taskDeleted(task) { //Supprimer une tâche
            const { index } = task
            return this.tasks =  this.tasks.filter((item, i) => i !== index)  
        },
        taskChecked(task) { //Cocher une tâche
            const { index } = task
            this.tasks[index].checked = !this.tasks[index].checked
        },       
    },

    data() {
        return {
            tasks: [],
        }
    },

  components : {
      newTodo,
      todoList
    },

    computed: {
        date() { //Afiche la date 
            const date = new Date()
            const day = date.toLocaleString("default", { weekday : "long"})
            const month = date.toLocaleString("default", {month : "long"})
            return day + ' ' + date.getDay() + ' ' + month
        },
        nbTasks() { //Vérifie le nombre de tâches 
            return this.tasks && Array.isArray(this.tasks) ? this.tasks.length : 0
        }  
    }
 }
</script>

<style scoped>
    #todo-card{
        display : flex;
        justify-content : space-between;
        width : 800px;
        height : 300px;
        margin-top : 100px;
        background : white;
        flex-wrap:wrap;
        justify-content: center;
        border-radius : 15px;
    }
    h2{
        color : grey;
    }
    h1{
        color : green;
    }
    header {
        width : 100%;
        display : flex; 
        justify-content : space-evenly;
        box-shadow: 0px 2px 5px black;
        align-items : center;

    }
    #newTodo{
        width : 70%;
        justify-content: center;
        display : flex;
        align-items : center;
        margin-top : 25px;
        justify-content : space-between;
    }
</style>