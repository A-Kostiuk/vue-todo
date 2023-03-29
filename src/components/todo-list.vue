<template>
  <ul v-if="todos.length > 0">
    <todoItem v-for="(todo, index) in todos"
              :key="todo.message"
              :todo="todo"
              :index="index"
              @delete-todo="deleteTodo"
              @change-status="changeStatus"
              @edit-todo="editTodo"
    />
  </ul>
  <p v-else>
    You haven`t any todos, please add todo
  </p>
</template>

<script>
import todoItem from "@/components/todo-item";

export default {
  name: "todo-list",
  props: ['todos'],
  methods: {
    deleteTodo(id) {
      this.$emit('delete-todo', id)
    },
    changeStatus(id) {
      this.$emit('change-status', id)
    },
    editTodo(editInform) {
      this.$emit('edit-todo', editInform)
    }
  },

  components: {
    todoItem
  }
}
</script>

<style scoped>
ul {
  display: flex;
  flex-direction: column;
  gap: 10px;
  list-style: none;
  padding: 0;
  margin: 0;
}
</style>
