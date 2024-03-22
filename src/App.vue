<template>
  <p>Uncompleted Todos:</p>

  <div
    :key="todo.id"
    :class="{ red: !todo.done }"
    v-for="todo in uncompleted"
  >
    {{ todo.task }} - <span>{{ todo.done }}</span>
    <input type="checkbox" v-model="todo.done" />
  </div>

  <p>Completed Todos:</p>
  <div
    :key="todo.id"
    :class="{ blue: todo.done }"
    v-for="todo in completed"
  >
    {{ todo.task }} - <span>{{ todo.done }}</span>
    <input type="checkbox" v-model="todo.done" />
  </div>

  <br><br>

  <select v-model="selectedOption.option">
    <option value="1">1</option>
    <option value="2">2</option>
    <option value="3">3</option>
  </select>

  <slot name="description" />

  <p>
    {{ selectedOption.option }}
  </p>
</template>

<script>

export default {
  name: "App",
  components: {},
  beforeCreate() {
    console.log('beforeCreate')
    console.log('DOM: ', this.$el)
  },
  created() {
    console.log('created')
    console.log('DOM: ', this.$el)
  },
  beforeMount() {
    console.log('beforeMount')
    console.log('DOM: ', this.$el)
  },
  mounted() {
    console.log('mounted')
    console.log('DOM: ', this.$el)
  },
  beforeUnmount() {
    console.log('beforeUnmount')
  },
  unmounted() {
    console.log('unmounted')
  },
  data() {
    return {
      selectedOption: {
        option: 0
      },
      todos: [
        { id: 1, task: "item 1", done: false },
        { id: 2, task: "item 2", done: false },
        { id: 3, task: "item 3", done: false },
        { id: 4, task: "item 4", done: true },
      ],
      isBlue: true,
      isRed: false,
    };
  },
  watch: {
    selectedOption: {
      handler() {
        console.log('option alterada')
      },
      deep: true
    }
  },
  methods: {
    selectedOptionWasChanged() {
      console.log('selected option was changed')
    }
  },
  computed: {
    uncompleted() {
      return this.todos.filter(todo => !todo.done)
    },
    completed() {
      return this.todos.filter(todo => todo.done)
    }
  }
};
</script>

<style>
.blue {
  color: blue;
}

.red {
  color: red;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
