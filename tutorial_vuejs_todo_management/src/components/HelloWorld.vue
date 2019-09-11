<template>
  <div>
    {{ msg }}
    <form>
      <button v-on:click="addToDo()">ADD TASK</button>
      <button>DELETE FINISHED TASKS</button>
      <p>input: <input type="text" v-model="newToDo"></p>
      <p>task: {{ newToDo }}</p>
    </form>
    <div class="task-list">
      <label class="task-list__item" v-for="todo in todos">
        <input type="checkbox"><button>EDIT</button>{{ todo.text }}
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
        {text: "vue-router", done: false},
        {text: 'vuex', done: false},
        {text: 'vue-loader', done: false},
        {text: 'awesome-vue', done: true },
      ],
      newToDo: ""
    }
  },
  methods: {
    addToDo: function(event) {
      let text = this.newToDo && this.newToDo.trim()
      if (!text) return
      this.todos.push({text: text, done: false})
      this.newToDo = ""
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
