<template>
  <div class="home">
    <!-- <img  alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <TodoSearch class="mb-3" @buscar = 'buscar' />
    <div class="container">
      <div class="row">
        <div class="col-md-6 agrega-tareas-wrapper wrappers">
          <div> <h2 class="my-3">Todo Add</h2>
            <TodoAdd @addTodo = 'addTodo' />
          </div><hr>
          <div >
            <h3>Search Result</h3>
            <TodoItems v-if="item_to_show" :tarea = 'item_to_show' :eliminar="eliminar"/>
            <span v-else>Nothing to show...</span> 
          </div>
        </div>

        <div class="col-md-6 lista-tareas-wrapper wrappers">
          <h2 class="my-3">Todo List</h2>
          <div v-if="!todos.length"><span>No hay tareas para mostrar</span></div>
          <!-- @delete-todo="eliminar" -->
          <div v-else><Todo :todoslist="copyTodos" :eliminar="eliminar"/></div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import TodoSearch from '../components/Search.vue'
import Todo from '../components/Todos.vue'
import TodoAdd from '../components/TodoAdd.vue'
import TodoItems from '../components/TodoItems.vue' 
import axios from 'axios'

class TodoInterface {
  constructor(id,title,completed){
    this.id = id,
    this.title = title,
    this.completed = completed
  }
}
export default {
  name: 'Home',
  components: {
    // HelloWorld,
    TodoSearch,
    Todo,
    TodoAdd,
    TodoItems
  },
  data() {
    return {
      todos:[],
      copyTodos:[],
      item_to_show:false
    }
  },
  
  created() {   
    
    axios.get('http://localhost:4200/todo',{timeout:1000})
    .then(response=> {
      console.log(response.data[0])
      this.todos = response.data
      this.copyTodos = [...this.todos]
      return
      })
    .catch(err=>console.log(`Servidor caido ${err}`)) 
     
   
  },
  methods:{
    eliminar(id){
      axios.delete(`http://localhost:4200/todo/${id}`,{timeout:1000}).then(el=>{
        if(el.status=='OK')
        console.log(el)
          this.todos = this.todos.filter(el=>el.id != id)     
          this.copyTodos = [...this.todos] 
        }).catch(el=> console.log(el))
    },
    addTodo(texto){
      let newtoDo = new TodoInterface(this.todos.length? this.todos[this.todos.length-1].id+1:0,texto.toUpperCase(),false)
      axios.post(`http://localhost:4200/todo`,newtoDo)
      .then(el=>{
       
        this.todos.push(el.data)
        this.copyTodos = [...this.todos]
      })
      .catch(error => {
        console.log(error)
        return alert('Ha ocurrido un error en el servidor y no se ha guardado la informacion')  
      })

      
    },
    buscar(text){
      this.item_to_show = this.copyTodos.filter(el=> el.title===text.toUpperCase())[0]
      if (!this.item_to_show)
        return alert('There is no task that match with your request')        
    },

  },
}
</script>

<style scoped>
.wrappers{
  border: 2px solid red;
  height: 40rem;
}
.lista-tareas-wrapper{
  overflow-y: scroll;
}
</style>
