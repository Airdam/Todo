<template>
  <div>
    <ul v-if="errors.length > 0">
      <li v-for="(error, index) in errors" :key="index" class="text-red-400 font-extrabold">
        {{ error }}
      </li>
    </ul>

    <form @submit.prevent="submitTodo" class="w-full flex">
      <input
        v-model="todo.text"
        type="text"
        class="w-full flex rounded border-2 p-2 m-2"
        placeholder="Was soll gemacht werden?"
      />
      <input v-model="todo.date" type="date" class="rounded border-2 p-2 flex padding m-2" />
      <button type="submit" class="rounded flex m-2 p-2 text-black bg-red-400">Hinzufügen</button>
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
        this.errors.push('Kein Todo eingegeben!')
      } else if (this.todo.text.length < 5) {
        this.errors.push('Todo muss mindestens 5 Zeichen haben!')
      } else if (!this.todo.date) {
        this.errors.push('Kein Datum ausgewählt!')
      }
      if (this.errors.length > 0) {
        return
      }

      this.$emit('add-todo', this.todo)
      this.todo.text = ''
      this.todo.date = ''
    },
  },
}
</script>
