<template>
   <div class="m-3">
      <div class="card bg-dark text-white">
         <div class="card-body">
            <form class="form-data" >
               <div class="container">
                  <label for="addToDo">Enter a new Task</label>
                  <textarea si
                  type="text" 
                  name='addToDo' 
                  id='addToDo'
                  v-model.trim="texto"
                  class="form-control"></textarea>
                  <br>
               </div>
               <div class="container">
                  <button @click.prevent="verTodo()" class="btn btn-primary btn-block">Aceptar</button>
               </div>
            </form>
         </div>
      </div>
   </div>
</template>



<script>
export default {
   name:  'TodoAdd',
   data() {
      return {
         texto:'',
      }
   },
   methods:{
      verTodo(){
         this.$emit('addTodo',this.texto)
         this.texto = ''
      }
   }
}
</script>

<style scoped>
   textarea {
  resize: none;
}
</style>