<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <Liste msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
// @ is an alias to /src
import Liste from '@/components/Liste.vue'

export default {
  name: 'Home',
  components: {
    Liste
  }
}
</script>
