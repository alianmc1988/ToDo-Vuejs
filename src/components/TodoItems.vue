<template>
    <div class="TodoItem">
        <div class="card m-3" >
          <div :class = 'tarea.completed ? "completado": "TodoItem-card p-3"'>
              <div class="py-4" ><p>{{tarea.title}}</p></div> 
              
              
          <div class="container">
            <hr> 
            <label for="completada" class="mx-3 "  v-if="!tarea.completed">Task finished</label>
            <input type="checkbox" v-model = 'tarea.completed' id="completada">
          </div> 
          </div>
          <!-- @click="$emit('delete-todo', tarea.id)" -->
          <button class="btn btn-danger" v-if="tarea.completed" @click="eliminar(tarea.id)" >Delete Task</button>
        </div>
    </div>
</template>



<script>
export default {
    name:  'TodoItem',
    props:['tarea','eliminar'],
    
}
</script>

<style scoped>
  .completado{
    background-color: aqua;
    text-decoration: line-through;
  }
  .TodoItem-card{
    background-color: darkgray;
  }
</style>