<template>
  <div id="app">
    <h2 id="title">Vue-Todos</h2>
    <div class="container">
      <input 
        class="inputText" 
        placeholder="what's your task?"
        autofocus="true"
        v-model="todoText"
        v-on:keyup.enter="addTodo(todoText)" />
      <ul>
        <li v-for="item in items">
          <input 
            type="checkbox" 
            v-on:click="handleClick(item)" />
          <span 
            v-bind:class="{ active: item.isChecked }" 
            v-text="item.label" />
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      items: []
    }
  },
  methods: {
    addTodo: function (todoText) {
      this.items.push({
        label: todoText,
        isChecked: false
      })
      this.todoText = ''
    },
    handleClick: function (item) {
      item.isChecked = !item.isChecked
    }
  }
}
</script>

<style>
* {
  padding: 0;
  margin: 0;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  max-width: 600px;
  margin: 60px auto 0 auto;
}

#title {
  text-align: center;
  text-decoration: underline;
}

.container {
  margin: 0 100px;
}

.inputText {
  width: 100%;
  height: 30px;
  border: none;
  border-bottom: 1px solid #ddd;
  font-size: 20px;
  margin: 15px auto;
}

ul {
  list-style: none;
}

li {
  margin-bottom: 12px;
  border-bottom: 1px solid #d2d2d2;
}

.active {
  text-decoration: line-through;
}

</style>
