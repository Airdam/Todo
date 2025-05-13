<template>
  <div>
    <form @submit.prevent="submitEdit">
      <input v-model="edited.text" type="text" />
      <input v-model="edited.date" type="date" />
      <button type="submit">Speichern</button>
      <button type="button" @click="$emit('cancel-edit')">Abbrechen</button>
    </form>
  </div>
</template>

<script>
export default {
  name: 'TodoEdit',
  props: {
    todo: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      edited: {
        text: this.todo.text,
        date: this.todo.date,
        id: this.todo.id,
        done: this.todo.done,
      },
    }
  },
  methods: {
    submitEdit() {
      this.$emit('save-edit', this.edited)
    },
  },
}
</script>
