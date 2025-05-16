<template>
  <div class="w-full items-center">
    <div v-if="todos.length === 0">Keine todos vorhanden</div>
    <ul v-else>
      <li v-for="todo in todos" :key="todo.id" class="flex flex-col rounded bg-gray-500 items-center p-4 mb-2">
        <span class="w-full flex-1 mb-4" :style="{
          textDecoration: todo.done ? 'line-through ' : 'none',
          color: todo.done ? '#8eee5b' : '#fff',
        }">
          Todo: {{ todo.text }} <br />
          Datum: {{ todo.date }}
        </span>

        <div class="flex justify-end w-full gap-2">
          <UiButton @click.native="toggleDone(todo)" button-type="button" :design="todo.done ? 'danger' : 'success'">
            <img class="h-6 w-6 cursor-pointer" :src="todo.done ? '/icons/lock-open.svg' : '/icons/check.svg'" />
          </UiButton>

          <UiButton @click.native="$emit('edit-todo', todo)" button-type="button" design="info">
            <img class="h-6 w-6 cursor-pointer" src="/icons/pen.svg" />
          </UiButton>

          <UiButton @click.native="$emit('delete-todo', todo)" button-type="button" design="danger">
            <img class="h-6 w-6 cursor-pointer" src="/icons/trash.svg" />
          </UiButton>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
import UiButton from './ui/UiButton.vue';

export default {
  name: 'TodoList',
  components: {
    UiButton
  },
  props: {
    todos: {
      type: Array,
      required: true,
    },
  },
  methods: {
    toggleDone(todo) {
      todo.done = !todo.done
      this.$emit('save-edit', todo)
    },
    methods: {
      toggleDone(todo) {
        todo.done = !todo.done
      },
    },
  },
}
</script>
