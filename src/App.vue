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
  }

#app {
  
  width: 100%;
  height: 100vh;
  display: flex;
}
</style>
