<template>    
    <header class="navbar-wrapper">
    
        
        <nav class="nav-mobile nav justify-content-center navbar-light bg-dark d-none d-md-flex p-3">
            <router-link class="nav-link active fa fa-home" to="/"><b>Home</b> </router-link>
            <router-link class="nav-link fa fa-book" to="/about"><b>about</b> </router-link>
            
        </nav>
        
        
    </header>
</template>

<script>
export default{
    name:'Navigation',
    
}
</script>