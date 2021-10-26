<template>
   <nav class="nav justify-content-center navbar-dark bg-dark  d-md-flex p-3">           
         <label for="searchbox" class="mx-3" > <b class="color-white text-white">Search</b> </label>
         <input type="text" v-model ='text' id="searchbox" @keypress.enter="handleSearch()">
   </nav>
</template>



<script>
export default {
   name:  'TodoSearch',
   data() {
      return {
         text:''
      }
   },
   methods:{
      handleSearch(){
         this.$emit('buscar',this.text)
         this.text = ''
         return
      }
   },
}
</script>