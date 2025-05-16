<template>
  <div>
    <ul class="bg-red-200 rounded p-4 mb-2" v-if="errors.length > 0">
      <li v-for="(error, index) in errors" :key="index" class="text-red-400 font-semibold">
        {{ error }}
      </li>
    </ul>

    <form @submit.prevent="submitTodo" class="w-full flex flex-col gap-2">
      <input v-model="todo.text" type="text" class="w-full flex rounded border-2 p-2"
        placeholder="Was soll gemacht werden?" />
      <input v-model="todo.date" type="date" class="w-full rounded border-2 p-2 flex padding" />

      <UiButton button-type="submit" design="danger">
        Hinzufügen
      </UiButton>
    </form>
  </div>
</template>

<script>
import UiButton from './ui/UiButton.vue';

export default {
  name: 'TodoForm',
  components: {
    UiButton
  },
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
      this.todo.text = this.todo.text.trim()

      if (!this.todo.text) {
        this.errors.push('Kein Todo eingegeben!')
      }
      if (this.todo.text.length < 5) {
        this.errors.push('Todo muss mindestens 5 Zeichen haben!')
      }
      if (!this.todo.date) {
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
