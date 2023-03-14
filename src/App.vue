<script>
import { def } from '@vue/shared';
import Task from './components/Task.vue'

export default{
  name : 'App',
  components: {
    Task
  }
}
</script>

<template>
  <div id="app">
    <Task></Task>
  </div>
</template>

<style scoped>

</style>
