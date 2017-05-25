<template>
  <div id="app">
    <h1 v-bind:disabled="false">{{ text }}</h1>
    <form v-on:submit.prevent="onSubmit">
      <input type="text" v-model="text">
      <button v-on:click="handleClick">Click me!</button>
    </form>
    <div id="example">
      <p>original Text: "{{ text }}"</p>
      <p>computed reverse text: "{{ reverseText }}"</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      text: '123'
    }
  },
  computed: {
    reverseText: function () {
      return this.text.split('').reverse().join('')
    }
  },
  methods: {
    handleClick: function () {
      this.text = '456'
      alert(this.text)
    },
    onSubmit: function () {
      alert('onSubmit is run')
      console.log(`${this.text} by onSubmit`)
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
