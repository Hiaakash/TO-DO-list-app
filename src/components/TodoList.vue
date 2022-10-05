<template>
  <section class="todoListContainer">
    <h3>TO-DO LIST</h3>
    <div class="list" id="todo-list">
      <div class="todo-item" v-for="(todo,index) in todoListData" v-bind:key="index">

        <label >
          <input type="checkbox" :checked="todo.done" @click="checkBoxHandler(todo)"/>
          <span :class="getClass(todo.category)"></span>
        </label>
        <div class="todo-content">
        <input type="text" :value="todo.content" readonly>
        </div>

        <div class="actions">
          <button class="edit" @click="editTodo(index, todo)">EDIT</button>
          <button class="delete" @click="deleteTodo(index, todo)">DELETE</button>
        </div>
      </div>
    </div>

  </section>
</template>

<script>
export default {
  props: ['todoListData'
  ],
  name: 'TodoList',
  data () {
    return {
    }
  },
  mounted () {
    // console.log('PROP =>', this.todoListData)
  },
  updated () {
  },
  methods: {
    getClass: function (cls) {
      return `${cls} bubble`
    },
    checkBoxHandler: function (todo) {
      const currTodo = this.todoListData.map(todos => {
        if (todos.createdAt === todo.createdAt) {
          todos.done = !todo.done
        }

        return todos
      })
      // console.log('CURR TODO LIST', currTodo)
      localStorage.setItem('todos', JSON.stringify(currTodo))
    },
    editTodo: function (val, todo) {
      const content = document.getElementsByClassName('todo-content')
      const input = content[val].querySelector('input')
      input.removeAttribute('readonly')
      input.focus()
      input.addEventListener('blur', e => {
        input.setAttribute('readonly', true)
        todo.content = e.target.value
        const currTodo = this.todoListData.map(todos => {
          if (todos.createdAt === todo.createdAt) {
            todos.content = e.target.value
          }

          return todos
        })
        localStorage.setItem('todos', JSON.stringify(currTodo))
      })
    },
    deleteTodo: function (index, todo) {
      const currTodo = this.todoListData.filter(todos => {
        if (todos.createdAt === todo.createdAt) {
          return false
        } else {
          return true
        }
      })
      this.todoListData = currTodo
      localStorage.setItem('todos', JSON.stringify(currTodo))
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .todo-content > input {
    font-family: 'Noto Sans Mono', monospace;
  }

</style>
