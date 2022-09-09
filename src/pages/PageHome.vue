<template>
  <div id="app">
    <nav class="orange darken-2">
      <div class="nav-wrapper">
        <img alt="Vue logo" src="../assets/logo.png" width="32" />
      </div>
    </nav>
    <div v-show="exibir.lista" style="padding">
      <button @click="mostrarCadastro">Adicionar</button>
    </div>
    <!--Lista-->
    <div v-show="exibir.lista">
      <TarefaList :msg="'Welcome to Your Vue.js App'" :tasks="listaDeTarefa" />
    </div>

    <!--Form-->

    <div v-show="exibir.form">
      <h2>Cadastrar Tarefa</h2>
      <input
        type="text"
        name="title"
        id="title"
        placeholder="Entre com a tarefa"
        v-model="form.title"
      />
      <input
        type="text"
        name="projext"
        v-model="form.project"
        placeholder="Entre com um projeto"
      />
      <button class="btn" @click="salvarTarefa">Salvar</button>
    </div>
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
      listaDeTarefa: [],
      exibir: {
        lista: true,
        form: false,
      },
      form: {
        title: "",
        project: "",
      },
    };
  },
  methods: {
    listarTarefas() {
      TasksApi.getTasks((data) => {
        this.listaDeTarefa = data;
      });
    },
    mostrarCadastro() {
      this.exibir.form = true;
      this.exibir.lista = false;
    },
    salvarTarefa() {
      this.exibir.form = false;
      this.exibir.lista = true;
      const novaTarefa = {
        title: this.form.title,
        project: this.form.project,
        date: new Date().toLocaleDateString("pt"),
      };
      TasksApi.createTask(novaTarefa, () => {
        this.listarTarefas();
      });
    },
  },
  created() {
    this.listarTarefas();
  },
};
</script>

<style></style>
