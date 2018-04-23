<template lang="pug">
  #app
    header.header 
      i(class="far fa-list-alt") 
      .header-title Панель учета сотрудников
    .container
      employees

</template>

<script>

import employees from './components/employees.vue'


export default {

  components:{
    employees
  }
}
</script>

<style lang="scss" src='styles/employees.scss'>

</style>
