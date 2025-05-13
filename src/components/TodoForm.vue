<template>
  <div>
    <ul v-if="errors.length > 0">
      <li v-for="(error, index) in errors" :key="index">
        {{ error }}
      </li>
    </ul>

    <form @submit.prevent="submitTodo">
      <input v-model="todo.text" type="text" placeholder="Was soll gemacht werden?" />
      <input v-model="todo.date" type="date" />
      <button type="submit">Hinzufügen</button>
    </form>
  </div>
</template>

<script>
export default {
  name: 'TodoForm',

  data() {
    return {
      todo: {
        text: '',
        date: '',
      },
      errors: [],
    }
  },
  methods: {
    submitTodo() {
      this.errors = []
      if (!this.todo.text) {
        this.errors.push('todo.text ist nicht vorhanden')
      } else if (this.todo.text.length < 5) {
        this.errors.push('todo.text ist kürzer als 5 zeichen')
      } else if (!this.todo.date) {
        this.errors.push('todo.date ist nicht vorhanden')
      }
      if (this.errors.length > 0) {
        return
      }
      this.$emit('add-todo', this.todo)
      this.nextId = ''
      this.todo.text = ''
      this.todo.date = ''
    },
  },
}
</script>
