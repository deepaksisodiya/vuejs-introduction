<template>
  <div>
    <header>TODO App</header>
    <input v-model="inputText" />
    <button @click="addTodo">Add Todo</button>

    <ol>
      <li v-for="(todo, index) in todos" :key="index">
        <div>
          <del v-if="todo.completed">{{ todo.text }}</del>
          <span v-else>{{ todo.text }}</span>
          <input
            type="checkbox"
            v-model="todo.completed"
            @click="toggleTodo(index)"
          />
          <button @click="deleteTodo(index)">Delete</button>
        </div>
      </li>
    </ol>

    <div v-if="todos.length > 0">
      <div>Total Todos {{ todos.length }}</div>
      <div>Completed Todos {{ completedTodos }}</div>
      <div>Remaining Todos {{ remainingTodos }}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Todos",

  data() {
    return {
      inputText: "",
      todos: []
    };
  },

  computed: {
    completedTodos() {
      return this.todos.filter(todo => {
        return todo.completed;
      }).length;
    },

    remainingTodos() {
      return this.todos.filter(todo => {
        return !todo.completed;
      }).length;
    }
  },

  methods: {
    addTodo() {
      if (!this.inputText) return;

      const todoObj = {
        text: this.inputText,
        completed: false
      };

      this.todos.push(todoObj);
      this.inputText = "";
    },

    toggleTodo(toggleIndex) {
      this.todos = this.todos.map((todo, index) => {
        if (index === toggleIndex) {
          return {
            ...todo,
            completed: !todo.completed
          };
        }
        return todo;
      });
    },

    deleteTodo(deleteIndex) {
      this.todos = this.todos.filter((todo, index) => {
        if (deleteIndex !== index) {
          return todo;
        }
      });
    }
  }
};
</script>

<style></style>
