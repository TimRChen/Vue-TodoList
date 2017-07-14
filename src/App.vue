<template>
  <div id="app">
    <a href="https://github.com/TimRChen/Vue-TodoList"><img style="position: absolute; top: 0; right: 0; border: 0;" src="https://camo.githubusercontent.com/e7bbb0521b397edbd5fe43e7f760759336b5e05f/68747470733a2f2f73332e616d617a6f6e6177732e636f6d2f6769746875622f726962626f6e732f666f726b6d655f72696768745f677265656e5f3030373230302e706e67" alt="Fork me on GitHub" data-canonical-src="https://s3.amazonaws.com/github/ribbons/forkme_right_green_007200.png"></a>
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
      tmpList: [],
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
  created: function () {
    // init list array
    this.tmpList = this.getTodos('vue-todos') || []
    this.items = this.getTodos('vue-todos') || []
  },
  methods: {
    addTodo: function (todoText) {
      this.tmpList.push({
        label: todoText,
        isChecked: false
      })
      this.refresh_storage('vue-todos', this.tmpList)
      this.items = this.getTodos('vue-todos')
      this.todoText = ''
    },

    refresh_storage: function (key, value) {
      window.localStorage.setItem(key, JSON.stringify(value))
    },

    getTodos: function (key) {
      return JSON.parse(window.localStorage.getItem(key))
    },

    handleClick: function (item) {
      item.isChecked = !item.isChecked
      this.refresh_storage('vue-todos', this.items)
      // 全选状态时，若某一选项取消，则
      if (item.isChecked === false) {
        this.isAllChecked = false
      }
    },

    changeTodoState: function (isChecked, isChangeAll = false) {
      this.isAllChecked = isChecked
      if (isChangeAll) {
        this.items.forEach(item => (item.isChecked = isChecked))
        this.refresh_storage('vue-todos', this.items)
      }
    },

    handleSelectAll: function (e) {
      this.changeTodoState(e.target.checked, true)
    },

    deleteTodo: function (item) {
      let index = this.items.indexOf(item)
      this.items.splice(index, 1)
      this.refresh_storage('vue-todos', this.items)
    },

    clearDone: function () {
      if (this.isAllChecked) {
        this.items = []
        this.isAllChecked = false
        this.refresh_storage('vue-todos', this.items)
      } else {
        this.items = this.items.filter(item => !item.isChecked)
        this.refresh_storage('vue-todos', this.items)
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
