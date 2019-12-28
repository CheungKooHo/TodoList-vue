<template>
  <div class="to-do">
    <input
      class="add-input"
      type="text"
      placeholder="What we need to be done?"
      autofocus="autofocus"
      @keyup.enter="addTodo"
    />

    <!-- items组件 -->
    <items v-for="(todo) in filteredTodos" :key="todo.id" :todo="todo" @del="delTodo"></items>
    <!-- <items></items> -->
    <!-- tabs组件 -->
    <tab
      :filter="filter"
      :todos="todos"
      @toggleFilter="toggleFilter"
      @clear="clear"
      v-show="this.todos.length"
    ></tab>
  </div>
</template>

<script>
import Items from "@/components/Items";
import Tab from "@/components/Tab";

let id = 0;

export default {
  name: "ToDo",
  components: {
    Items,
    Tab
  },
  data() {
    return {
      todos: [],
      filter: "all"
    };
  },
  computed: {
    filteredTodos() {
      if (this.filter === "all") {
        return this.todos;
      } else {
        let completed = this.filter === "completed";

        // 将todos数组中，completed为true的值过滤出来，并返回一个新数组
        return this.todos.filter(todo => completed === todo.completed);
      }
    }
  },
  methods: {
    addTodo(e) {
      if (e.target.value.trim()) {
        // if (this.newTodo.trim()) {
        this.todos.unshift({
          id: id++,
          content: e.target.value.trim(),
          // content: this.newTodo.trim(),
          completed: false
        });
        e.target.value = "";
        // this.newTodo = "";
      } else {
        alert("请输入待办事项，并按下ENTER添加！");
      }
    },
    delTodo(delId) {
      this.todos.splice(this.todos.findIndex(todo => todo.id === delId), 1);
    },
    toggleFilter(state) {
      this.filter = state;
    },
    clear() {
      this.todos = this.todos.filter(todo => todo.completed === false);
    }
  }
};
</script>

<style>
.to-do {
  width: 600px;
  margin: 0 auto;
  box-shadow: 0 0 5px #666666;
}
.add-input {
  position: relative;
  margin: 0;
  width: 100%;
  font-size: 24px;
  font-family: inherit;
  font-weight: inherit;
  line-height: 1.4em;
  border: 0;
  outline: none;
  color: inherit;
  box-sizing: border-box;
  padding: 16px;
  border: none;
  box-shadow: inset 0 -2px 1px rgba(0, 0, 0, 0.03);
}
</style>