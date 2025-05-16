<template>
  <div>
    <form @submit.prevent="submitEdit" class="w-full flex flex-col gap-2">
      <input v-model="edited.text" type="text" class="w-full flex rounded border-2 p-2" />
      <input v-model="edited.date" type="date" class="w-full flex rounded border-2 p-2" />
      <UiButton button-type="submit" design="success">
          Speichern
      </UiButton>
      <UiButton @click.native="$emit('cancel-edit')" button-type="button" design="danger">
        Abbrechen
      </UiButton>
    </form>
  </div>
</template>

<script>
import UiButton from './ui/UiButton.vue';

export default {
  name: 'TodoEdit',
  components: {
    UiButton
  },
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
