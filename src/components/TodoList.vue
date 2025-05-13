<template>
  <div>
    <div v-if="todos.length < 1">Keine todos vorhanden</div>
    <ul v-else>
      <li v-for="(todo, index) in todos" :key="todo.id">
        <span :style="{ textDecoration: todo.done ? 'line-through' : 'none' , color: todo.done ? 'green' : 'black'}"> {{todo.id}} , {{ todo.text }} , {{ todo.date }}</span>
        <input type="checkbox" @change="$emit('edit-todo', todo)"></input>
        <button @click="$emit('edit-todo', todo)">Bearbeiten</button>
        <button @click="$emit('delete-todo', todo)">Löschen</button>
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
}
</script>
