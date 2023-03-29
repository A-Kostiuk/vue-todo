<template>
  <h1>ToDo App</h1>
  <additionTodo @add-todo="addTodo" />
  <select class="filter" v-model="filter">
    <option value="all">All</option>
    <option value="completed">Completed</option>
    <option value="not-completed">Not completed</option>
  </select>
  <hr />
  <todoList :todos="filterTodos"
            @delete-todo="deleteTodo"
            @change-status="changeStatus"
            @edit-todo="editTodo"
  />
</template>

<script>
import additionTodo from '@/components/addition-todo'
import todoList from "@/components/todo-list";

export default {
  name: 'App',
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=5')
        .then(response => response.json())
        .then(json => {
          this.todos = json
        })
  },
  data() {
    return {
      todos: [],
      filter: 'all'
    }
  },
  computed: {
    filterTodos() {
      switch (this.filter) {
        case "completed":
          return this.todos.filter((todo) => todo.completed === true)
        case 'not-completed':
          return this.todos.filter((todo) => todo.completed === false)
        default:
          return this.todos
      }
    }
  },
  methods: {
    deleteTodo(id) {
      this.todos = this.todos.filter((todo) => todo.id !== id)
    },
    changeStatus(id) {
      const el = this.todos.find((todo) => todo.id === id)
      el.completed = !el.completed
    },
    addTodo(value) {
      const newTodo = {
        title: value,
        completed: false,
        id: new Date()
      }
      this.todos.push(newTodo)
    },
    editTodo(editInform) {
      const todo = this.todos.find((todo) => todo.id === editInform.id);
      todo.title = editInform.title
    }
  },
  components: {
    additionTodo,
    todoList
  }
}
</script>

<style lang="scss">
@import "assets/style";

#app {
  width: 600px;
  margin: 0 auto;
  text-align: center;
}

.filter {
  width: 50%;
  font-size: 16px;
  padding: 5px;
  margin-bottom: 20px;
}

</style>
