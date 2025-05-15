<template>
  <div class="w-full items-center">
    <div v-if="todos.length < 1">Keine todos vorhanden</div>
    <ul v-else>
      <li
        v-for="(todo, index) in todos"
        :key="todo.id"
        class="flex rounded mt-2 bg-gray-500 items-center"
      >
        <span
          class="rounded m-2 p-2 flex-1"
          :style="{
            textDecoration: todo.done ? 'line-through ' : 'none',

            color: todo.done ? 'green' : 'black',
          }"
        >
          Todo: {{ todo.text }} <br />
          Datum: {{ todo.date }}
        </span>

        <button
          @click="toggleDone(todo)"
          :class="[
            'm-2 p-2 border m-2 p-2 flex rounded font-semibold',
            todo.done ? 'bg-green-400 text-gray-800' : 'bg-green-400 text-gray-800',
          ]"
        >
          {{ todo.done ? 'Erledigt' : 'Offen' }}
        </button>

        <button
          @click="$emit('edit-todo', todo)"
          class="bg-blue-400 text-gray-800 flex border m-2 p-2 rounded"
        >
          Bearbeiten
        </button>

        <button
          @click="$emit('delete-todo', todo)"
          class="bg-red-400 text-gray-800 flex border m-2 p-2 rounded"
        >
          Löschen
        </button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'TodoList',
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
