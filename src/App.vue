<template>
  <div>
    <main-header></main-header>
    <main-todo></main-todo>
  </div>
</template>

<script>
import '../src/assets/styles/global.css'
import MainHeader from './components/MainHeader.vue'
import MainTodo from './components/MainTodo/MainTodo.vue'

export default {
  name: 'App',
  components:{
    MainHeader,
    MainTodo
  }
}
</script>

<style>
</style>
