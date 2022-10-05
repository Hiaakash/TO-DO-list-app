
<template>
  <div id="app">
    <Greetings>
      <h1 :slot="Title">📋 To-Do List 📋</h1>
    </Greetings>
    <TodoSection :submitTodo="submitTodo" />
    <TodoList :todoListData="todoListData" />
  </div>
</template>

<script>
import Greetings from './components/Greetings.vue'
import TodoSection from './components/TodoSection.vue'
import TodoList from './components/TodoList.vue'

export default {
  name: 'App',
  components: {
    Greetings,
    TodoSection,
    TodoList
  },
  data () {
    return {
      todoListData: []
      // title: 'Title'
    }
  },
  created () {
    this.todoListData = JSON.parse(localStorage.getItem('todos')) || []
  },
  methods: {
    submitTodo: function (e) {
      const todo = {
        content: e.target.elements.content.value,
        category: e.target.elements.category.value,
        done: false,
        createdAt: new Date().getTime()
      }
      this.todoListData.push(todo)
      localStorage.setItem('todos', JSON.stringify(this.todoListData))
      console.log('CURR TODO', this.todoListData)
      e.target.reset()
    }

  }
}
</script>

<style>
@import './main.css';
#app {
  font-family: 'Noto Sans Mono', monospace;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin: 0px;
  padding: 0px;
  box-sizing: border-box;
}

</style>
