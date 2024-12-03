<template>
  <div class="main">
    <CalForm />
  </div>
</template>

<script>
import CalForm from './views/CalForm.vue'


export default {
  name: 'App',
  components: {
    CalForm,

  }
}
</script>

<style >
@import './main.css'
</style>
