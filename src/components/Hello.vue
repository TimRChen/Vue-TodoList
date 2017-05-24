<template>
  <div class="hello">
    <p>{{ message }}</p>
    <button v-on:click="reverseMessage">逆转消息</button>
  </div>
</template>

<script>
export default {
  name: 'hello',
  data () {
    return {
      message: 'Welcome to Your Vue.js App'
    }
  },
  methods () {
    return {
      reverseMessage: function () {
        this.message = this.message.split('').reverse().join('')
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
