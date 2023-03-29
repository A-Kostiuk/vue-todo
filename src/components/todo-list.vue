<template>
  <ul>
    <todoItem v-for="todo in todos"
              :key="todo.message"
              :todo="todo"
              @delete-todo="deleteTodo"
              @change-status="changeStatus"
    />
  </ul>
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
