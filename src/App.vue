<template>
  <h1>ToDo App</h1>
  <additionTodo @add-todo="addTodo" />
  <hr />
  <todoList :todos="todos"
            @delete-todo="deleteTodo"
            @change-status="changeStatus"
  />
</template>

<script>
import additionTodo from '@/components/addition-todo'
import todoList from "@/components/todo-list";

export default {
  name: 'App',
  data() {
    return {
      todos: [{message: 'todo 1', completed: true, id: 0}, {message: 'todo 2', completed: false, id: 1}]
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
        message: value,
        completed: false,
        id: this.todos[this.todos.length - 1].id + 1
      }
      this.todos.push(newTodo)
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

</style>
