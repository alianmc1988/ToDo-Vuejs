<template>
    <div>
        <div v-for="todo in todoslist" :key="todo.id">
            <!-- @delete-todo="$emit('delete-todo',todo.id)" -->
            <TodoItems :tarea= 'todo' :eliminar="eliminar" />        
        </div>
    </div>
</template>



<script>

import TodoItems from './TodoItems.vue'
export default {
    name:'Todos',
    props:['todoslist', 'eliminar'],   
    components:{
        TodoItems
    },
}
</script>
