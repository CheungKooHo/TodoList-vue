<template>
  <div :class="['items',todo.completed ? 'completed' : '']">
    <input class="toggle" type="checkbox" v-model="todo.completed" />
    <label v-show="!this.isEditShow" @dblclick="editClick">{{todo.content}}</label>
    <button class="del" @click="delTodo">x</button>
    <input
      v-show="this.isEditShow"
      @keyup.enter="edited"
      @keyup.esc="cancle"
      class="edit"
      type="text"
      v-model.trim="todo.content"
      v-focus="todo===this.editingTodo"
    />
  </div>
</template>

<script>
export default {
  name: "Items",
  data() {
    return {
      isEditShow: false,
      editingTodo: ""
    };
  },
  props: {
    todo: {
      type: Object
    }
  },
  directives: {
    focus(el, value) {
      if (value) {
        el.focus();
      }
    }
  },
  methods: {
    delTodo() {
      this.$emit("del", this.todo.id);
    },
    editClick() {
      this.editingTodo = this.todo;
      this.isEditShow = true;
    },
    edited(e) {
      if (this.todo.content.trim() === "") {
        this.delTodo();
      }
      this.todo.content = e.target.value.trim();
      e.target.value = "";
      this.isEditShow = false;
    }
  }
};
</script>

<style>
.items {
  position: relative;
  background-color: #fff;
  font-size: 24px;
  border-bottom: 1px solid rgba(0, 0, 0, 0.06);
}
.toggle {
  text-align: center;
  width: 40px;
  height: 40px;
  line-height: 40px;
  position: absolute;
  top: 0;
  bottom: 0;
  margin: auto 0;
  border: none;
  appearance: none;
  outline: none;
  padding-left: 5px;
  cursor: pointer;
}
.toggle::after {
  content: url("~@/assets/img/round.svg");
}
.toggle:checked::after {
  content: url("~@/assets/img/done.svg");
}
label {
  white-space: pre-line;
  word-break: break-all;
  padding: 15px 60px 15px 15px;
  margin-left: 45px;
  display: block;
  line-height: 1.2em;
  transition: color 0.4s;
}
.completed label {
  color: #d9d9d9;
  text-decoration: line-through;
}
.edit {
  white-space: pre-line;
  word-break: break-all;
  padding: 15px 60px 15px 15px;
  margin-left: 45px;
  display: block;
  line-height: 1.2em;
  transition: color 0.4s;
  border: 0;
  outline: none;
}
.del {
  position: absolute;
  top: 0;
  right: 10px;
  bottom: 0;
  width: 40px;
  height: 40px;
  margin: auto 0;
  font-size: 30px;
  color: #cc9a9a;
  margin-bottom: 11px;
  transition: color 0.2s ease-out;
  background-color: transparent;
  appearance: none;
  border-width: 0;
  cursor: pointer;
  outline: none;
}
</style>