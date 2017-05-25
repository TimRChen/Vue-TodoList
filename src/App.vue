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
    <div id="time">
      <p>BeiJing Time: "{{ now }}"</p>
    </div>
    <div id="name">{{ fullName }}</div>
    <button @click="changeName">changeName</button>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      text: '123',
      firstName: 'Foo',
      lastName: 'Bar'
    }
  },
  computed: {
    now: function () {
      return new Date().toLocaleTimeString()
    },
    reverseText: function () {
      return this.text.split('').reverse().join('')
    },
    fullName: {
      // getter
      get: function () {
        return `${this.firstName}  ${this.lastName}`
      },
      // setter
      set: function (newValue) {
        let names = newValue.split(' ')
        this.firstName = names[0]
        this.lastName = names[names.length - 1]
      }
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
    },
    changeName: function () {
      this.firstName = 'Tim'
      this.lastName = 'Rchen'
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
