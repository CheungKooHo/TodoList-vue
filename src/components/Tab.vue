<template>
  <div class="tab">
    <span class="left">{{unFinishedTodoLength}} Items Left</span>
    <span class="tabs">
      <span
        v-for="state in states"
        :key="state"
        :class="['state', filter === state ? 'actived' : '']"
        @click="toggleFilter(state)"
      >{{state}}</span>
    </span>
    <span class="clear" @click="clearAll">Clear Completed</span>
  </div>
</template>

<script>
export default {
  name: "Tab",
  props: {
    todos: Array,
    filter: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      states: ["all", "active", "completed"]
    };
  },
  computed: {
    unFinishedTodoLength() {
      return this.todos.filter(todo => !todo.completed).length;
    }
  },
  methods: {
    clearAll() {
      this.$emit("clear");
    },
    toggleFilter(state) {
      this.$emit("toggleFilter", state);
    }
  }
};
</script>

<style>
.tab {
  font-weight: 600;
  display: flex;
  justify-content: space-between;
  padding: 5px 0;
  line-height: 30px;
  background-color: #ffffff;
  font-size: 14px;
}
.left,
.tabs,
.clear {
  padding: 0 10px;
  box-sizing: border-box;
}
.left,
.clear {
  width: 150px;
}
.left {
  text-align: left;
}
.clear {
  text-align: right;
  cursor: pointer;
}
.tabs {
  width: 200px;
  display: flex;
  justify-content: space-around;
}
.tabs span {
  display: inline-block;
  padding: 0 10px;
  cursor: pointer;
  border: 1px solid rgba(175, 47, 47, 0);
  border-radius: 10px;
}
.tabs span:hover {
  border-color: rgba(175, 47, 47, 0.4);
}
span.actived {
  border-color: rgba(175, 47, 47, 0.4);
}
</style>