<template>
  <li>
    <div class="information">
      <input type="checkbox" :checked="todo.completed" @change="$emit('change-status', todo.id)" />
      <p :class="todo.completed ? 'completed' : ''">{{ todo.message }}</p>
    </div>
    <div class="controls">
      <button class="edit-btn">Edit</button>
      <button class="delete-btn" @click="$emit('delete-todo', todo.id)">Delete</button>
    </div>
  </li>
</template>

<script>
export default {
  name: "todo-item",
  props: {
    todo: {
      type: Object,
      required: true
    }
  }
}
</script>

<style scoped>
p {
  margin: 0;
  text-align: start;
}

button {
  padding: 10px;
  border: none;
  cursor: pointer;
}

.edit-btn {
  background-color: white;
  border: 1px solid black;
}

.delete-btn {
  color: white;
  background-color: palevioletred;
}

input {
  width: 40px;
  height: 40px;
  flex-shrink: 0;
  margin: 0 40px 0 0;
  cursor: pointer;
}

.completed {
  text-decoration: line-through;
}

.information {
  display: flex;
  align-items: center;
  margin-bottom: 5px;
}

.controls {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 5px;
}
</style>
