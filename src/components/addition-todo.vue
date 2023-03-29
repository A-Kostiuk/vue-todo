<template>
  <form @submit.prevent="onSubmit">
    <input type="text" v-model="value">
    <button type="submit">Add</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      value: '',
    }
  },
  methods: {
    onSubmit() {
      if (this.value.trim()) {
        this.$emit('add-todo', this.value);
        this.value = ''
      }
    }
  },
  name: 'addition-todo'
}
</script>

<style scoped>
form {
  margin-bottom: 40px;
}

input {
  display: block;
  width: 100%;
  margin-bottom: 5px;
  padding: 5px;
  font-size: 18px;
}

button {
  width: 100%;
  color: white;
  background-color: black;
  border: none;
  cursor: pointer;
  padding: 10px;
}
</style>
