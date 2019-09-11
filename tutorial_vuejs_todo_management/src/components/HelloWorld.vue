<template>
  <div>
    {{ msg }}
    <form>
      <button @click="addToDo()">ADD TASK</button>
      <button @click="removeToDo()">DELETE FINISHED TASKS</button>
      <p>input: <input type="text" v-model="newToDo"></p>
      <p>task: {{ newToDo }}</p>
    </form>
    <div class="task-list">
      <label class="task-list__item"
             v-for="todo in todos"
             :class="{ 'task-list__item--checked': todo.done }"
             :key="todo.id">
        <input type="checkbox" v-model="todo.done">
        <input type="checkbox" v-model="todo.editing">
        <input v-if="todo.editing" type="text" v-model="todo.text" @keyup.enter="todo.editing = !todo.editing">
        <span v-else>{{ todo.text }}</span>
      </label>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      todos: [
        {id: 1, text: "vue-router", done: false, editing: false},
        {id: 2, text: 'vuex', done: false, editing: false},
        {id: 3, text: 'vue-loader', done: false, editing: false},
        {id: 4, text: 'awesome-vue', done: true, editing: false},
      ],
      newToDo: "",
      idCount: 4
    }
  },
  methods: {
    addToDo: function(event) {
      let text = this.newToDo && this.newToDo.trim()
      if (!text) return
      const id = ++this.idCount
      this.todos.push({id: id, text: text, done: false, editing: false})
      this.newToDo = ""
    },
    removeToDo: function(event) {
      this.todos = this.todos.filter(todo => !todo.done)
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
@mixin flex-vender() {
  display: flex;
  display: -webkit-flex;
  display: -moz-flex;
  display: -ms-flex;
  display: -o-flex;
}
.task-list {
  @include flex-vender;
  flex-direction: column;
  align-items: center;
  &__item {
    width: 270px;
    text-align: left;
    $element: #{&};
    &--checked {
      @extend #{$element};
      color: #85a6c6;
    }
  }
}
</style>
