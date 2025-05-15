<template>
  <div>
    <form @submit.prevent="submitEdit">
      <input v-model="edited.text" type="text" class="rounded border-2 padding m-2" />
      <input v-model="edited.date" type="date" class="rounded border-2 padding m-2" />
      <button type="submit" class="text-green-400 rounded border-2 padding m-2">Speichern</button>
      <button
        type="button"
        @click="$emit('cancel-edit')"
        class="text-red-400 rounded border-2 padding m-2"
      >
        Abbrechen
      </button>
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
