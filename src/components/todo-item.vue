<template>
  <li>
    <div class="information">
      <input class="status" type="checkbox" :checked="todo.completed" @change="$emit('change-status', todo.id)" />
      <p :class="todo.completed ? 'completed' : ''">{{ index + 1 }}</p>
      <input class="edit-field" type="text" v-model="newValue" v-if="isEdit" />
      <p :class="todo.completed ? 'completed' : ''" v-else>{{ todo.title }}</p>
    </div>
    <div class="controls">
      <button class="edit-btn" @click="editTodo">Edit</button>
      <button class="delete-btn" @click="$emit('delete-todo', todo.id)">Delete</button>
    </div>
  </li>
</template>

<script>
export default {
  name: "todo-item",
  data() {
    return {
      isEdit: false,
      newValue: this.todo.title
    }
  },
  props: {
    todo: {
      type: Object,
      required: true
    },
    index: Number
  },
  methods: {
    editTodo() {
      if (this.isEdit) {
        const editInform = {id: this.todo.id, title: this.newValue}
        this.$emit('edit-todo', editInform)
      }
      this.isEdit = !this.isEdit
    }
  }
}
</script>

<style scoped>

.edit-field {
  margin: 0;
  font-size: 16px;
  padding: 5px 0;
  flex-grow: 1;
}

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

.status {
  width: 40px;
  height: 40px;
  flex-shrink: 0;
  margin: 0 20px 0 0;
  cursor: pointer;
}

.completed {
  text-decoration: line-through;
}

.information {
  display: flex;
  align-items: center;
  margin-bottom: 5px;
  gap: 15px;
}

.controls {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 5px;
}
</style>
