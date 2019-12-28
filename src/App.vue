<template>
  <div id="app">
    <to-do-head></to-do-head>
    <to-do></to-do>
  </div>
</template>

<script>
import ToDoHead from "@/components/ToDoHead.vue";
import ToDo from "@/components/ToDo.vue";

export default {
  name: "App",
  components: {
    ToDoHead,
    ToDo
  }
};
</script>

<style scoped>
@import "./assets/css/base.css";
#app {
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
}
</style>
