<template>
  <div id="app">
    <h2 id="title">Vue-Todos</h2>
    <div class="container">
      <input
        class="inputText"
        placeholder="what's your task?"
        autofocus="true"
        v-model="todoText"
        @keyup.enter="addTodo(todoText)" />
      <ul>
        <li v-for="item in items">
          <input
            type="checkbox"
            :checked="item.isChecked"
            @click="handleClick(item)" />
          <span
            :class="{ active: item.isChecked }" 
            v-text="item.label" />
          <button
            class="delete"
            v-text="'delete'"
            @click="deleteTodo(item)" />
        </li>
      </ul>
      <div class="control">
        <input
          type="checkbox"
          v-model="isAllChecked"
          @click="handleSelectAll" />
        <span v-text="stat"/>
        <button
          class="clear"
          v-text="'清除已完成'"
          @click="clearDone" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      items: [],
      todoText: '',
      isAllChecked: false
    }
  },
  computed: {
    stat: function () {
      let closed = this.items.filter(item => item.isChecked).length
      return `${closed || 0} closed / ${this.items.length}`
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
      // 全选状态时，若某一选项取消，则
      if (item.isChecked === false) {
        this.isAllChecked = false
      }
    },

    changeTodoState: function (isChecked, isChangeAll = false) {
      this.isAllChecked = isChecked
      if (isChangeAll) {
        this.items.forEach(item => (item.isChecked = isChecked))
      }
    },

    handleSelectAll: function (e) {
      this.changeTodoState(e.target.checked, true)
    },

    deleteTodo: function (item) {
      let index = this.items.indexOf(item)
      this.items.splice(index, 1)
    },

    clearDone: function () {
      if (this.isAllChecked) {
        this.items = []
        this.isAllChecked = false
      } else {
        this.items = this.items.filter(item => !item.isChecked)
      }
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

.delete {
  float: right;
  width: 12%;
  height: 16px;
  background: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
.delete:hover, .control .clear:hover {
  background: #FF6A6A;
  color: #fff;
}

.active {
  text-decoration: line-through;
}

.control .clear {
  float: right;
  width: 20%;
  height: 30px;
  background: #fff;
  border: none;
  border-radius: 8px;
  cursor: pointer;
}


</style>
