<script setup lang="ts">
// Importação dos componentes e funções necessárias
import Header from "./components/Header.vue";
import TodoList from "./components/TodoList.vue";
import Footer from "./components/Footer.vue";
import { ref } from "vue";

// Definição da interface Todo
interface Todo {
  id: number;
  text: string;
  status: "emProducao" | "concluida" | "abandonada";
  category: "trabalho" | "pessoal" | "estudo";
  subTasks: any[]; // TODO: Definir uma interface específica para SubTask
}

// Array de categorias disponíveis
const categories = [
  { value: "todas", label: "Todas" },
  { value: "trabalho", label: "Trabalho" },
  { value: "pessoal", label: "Pessoal" },
  { value: "estudo", label: "Estudo" },
];

// Estado reativo para o filtro ativo e lista de todos
const activeFilter = ref("todas");
const todos = ref<Todo[]>([]);

// Função para atualizar o filtro ativo
const setFilter = (filter: string) => {
  activeFilter.value = filter;
};

// Função para adicionar uma nova tarefa
const addTodo = (newTodo: Omit<Todo, "id">) => {
  const id =
    todos.value.length > 0 ? Math.max(...todos.value.map((t) => t.id)) + 1 : 1;
  todos.value.push({ ...newTodo, id });
};

// Função para atualizar uma tarefa existente
const updateTodo = (updatedTodo: Todo) => {
  const index = todos.value.findIndex((t) => t.id === updatedTodo.id);
  if (index !== -1) {
    todos.value[index] = updatedTodo;
  }
};

// Função para obter o ícone correspondente a cada categoria
const getCategoryIcon = (category: string) => {
  switch (category) {
    case "trabalho":
      return "fas fa-briefcase";
    case "pessoal":
      return "fas fa-user";
    case "estudo":
      return "fas fa-book";
    default:
      return "fas fa-tasks";
  }
};
</script>

<template>
  <!-- Estrutura principal da aplicação -->
  <div class="app-container">
    <Header class="header" />
    <div class="content-wrapper">
      <!-- Barra lateral com informações do usuário e filtros -->
      <aside class="sidebar">
        <!-- ... (código da barra lateral) ... -->
      </aside>
      <!-- Conteúdo principal com a lista de tarefas -->
      <main class="main-content">
        <TodoList
          :activeFilter="activeFilter"
          :todos="todos"
          @add-todo="addTodo"
          @update-todo="updateTodo"
        />
      </main>
    </div>
    <Footer class="footer" />
  </div>
</template>

<style>
/* Estilos globais e layout principal da aplicação */
/* ... (estilos CSS) ... */
</style>
