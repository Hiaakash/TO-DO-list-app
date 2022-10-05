<template>
  <section class="create-todo">
  <h3>
    CREATE A TODO 📝
  </h3>
  <form id="todoForm" v-on:submit.prevent="submitTodoData">
    <h4>What's on your Todo list?</h4>
    <div class="inputContainer">
    <input class="todoInput" type="text" name="content" id="content" placeholder="E.g.: Have to pay bills" />
  </div>
    <div class="options">
    <label >
      <input type="radio" name="category" id="category1" value="business"/>
      <span class="business bubble"></span>
      <div>Business</div>
    </label>

    <label >
      <input type="radio" name="category" id="category2" value="personal"/>
      <span class="personal bubble"></span>
      <div>Personal</div>
    </label>
  </div>
  <input type="submit" value="addTodo" />
  </form>
  </section>
</template>

<script>
export default {
  props: ['submitTodo'],
  name: 'TodoSection',
  data () {
    return {
      name: ''
    }
  },
  methods: {
    submitTodoData: function (e) {
      e.preventDefault()
      this.submitTodo(e)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.greetingsContainer {
  color: #42b983;
}
.inputContainer > input {
  font-family: 'Noto Sans Mono', monospace;
}
</style>
