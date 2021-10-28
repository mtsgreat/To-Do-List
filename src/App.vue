<template>

  <FormTask/>
</template>

<script>
import FormTask from './components/FormTask.vue'

export default {
  name: 'App',
  components: {
    FormTask
  }
}
</script>

<style>

*{
  font-family: 'Roboto', sans-serif;
}

  body, html, h1 {
    margin: 0;
    padding: 0;
    overflow-x: hidden;
  }

#app {
  
  width: 100%;
  height: 100vh;
  display: flex;
}

@media only screen and (max-width: 600px) {
  #app {
   
    display: inline-block !important;
    
}

 body, html, h1 {
  
    overflow-x: hidden !important;
  }

}
</style>
