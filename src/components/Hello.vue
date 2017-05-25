<template>
  <div class="hello">
    <ol>
      <todo-item v-for="item in grocerylist" v-bind:todo="item"></todo-item>
    </ol>
  </div>
</template>

<script>
export default {
  name: 'hello',
  data () {
    return {
      grocerylist: [
        { text: '蔬菜' },
        { text: '奶酪' },
        { text: '任意' }
      ]
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
