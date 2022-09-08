<template>
  <div id="app">
    <nav class="orange darken-2">
      <div class="nav-wrapper"></div>
    </nav>
    <img alt="Vue logo" src="../assets/logo.png" width="32" />
    <TarefaList :msg="'Welcome to Your Vue.js App'" :tasks="listaDeTarefa" />
  </div>
</template>

<script>
import TasksApi from "../TasksApi.js";
import TarefaList from "../components/TarefaList.vue";

export default {
  components: {
    TarefaList,
  },
  data: () => {
    return {
      listaDeTarefa: ["A", "B", "C"],
    };
  },
  created() {
    TasksApi.getTasks((data) => {
      this.listaDeTarefa = data;
    });
  },
};
</script>

<style></style>
