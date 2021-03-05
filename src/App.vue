
<template>
  <div id="app">

    <todoCard>
    </todoCard>
    
    
  </div>
  
</template>

<script>
 import todoCard from './components/todo-card.vue'
export default {
  name: 'app',
  components : {
      todoCard
  }
}



</script>

<style>
#app{
  display : flex; 
  justify-content : center;
  width : 100%;
  height : 100vh;
  background : rgb(230, 207, 0);
}
</style>