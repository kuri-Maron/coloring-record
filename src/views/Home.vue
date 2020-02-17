<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <!-- <record/> -->
    <div-record/>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
// import Record from '@/components/Record.vue'
import divRecord from '@/components/divRecord.vue'

export default {
  name: 'Home',
  components: {
    // HelloWorld
    // Record
    divRecord
  }
}
</script>
