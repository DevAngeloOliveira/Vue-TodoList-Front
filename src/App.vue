<script setup lang="ts">
import Header from "./components/Header.vue";
import TodoList from "./components/TodoList.vue";
import Footer from "./components/Footer.vue";
import { ref } from "vue";

interface Todo {
  id: number;
  text: string;
  status: "emProducao" | "concluida" | "abandonada";
  category: "trabalho" | "pessoal" | "estudo";
  subTasks: any[]; // Você pode definir uma interface para SubTask se necessário
}

const categories = [
  { value: "todas", label: "Todas" },
  { value: "trabalho", label: "Trabalho" },
  { value: "pessoal", label: "Pessoal" },
  { value: "estudo", label: "Estudo" },
];

const activeFilter = ref("todas");
const todos = ref<Todo[]>([]);

const setFilter = (filter: string) => {
  activeFilter.value = filter;
};

const addTodo = (newTodo: Omit<Todo, "id">) => {
  const id =
    todos.value.length > 0 ? Math.max(...todos.value.map((t) => t.id)) + 1 : 1;
  todos.value.push({ ...newTodo, id });
};

const updateTodo = (updatedTodo: Todo) => {
  const index = todos.value.findIndex((t) => t.id === updatedTodo.id);
  if (index !== -1) {
    todos.value[index] = updatedTodo;
  }
};

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
  <div class="app-container">
    <Header class="header" />
    <div class="content-wrapper">
      <aside class="sidebar">
        <div class="user-info">
          <img
            src="./assets/images/image.png"
            alt="User Avatar"
            class="user-avatar"
          />
          <span class="user-name">Gabriel Ângelo</span>
        </div>
        <nav>
          <ul>
            <li v-for="cat in categories" :key="cat.value">
              <a
                href="#"
                @click.prevent="setFilter(cat.value)"
                :class="{ active: activeFilter === cat.value }"
              >
                <i :class="getCategoryIcon(cat.value)"></i>
                {{ cat.label }}
              </a>
            </li>
          </ul>
        </nav>
      </aside>
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
:root {
  --fb-blue: #1877f2;
  --fb-blue-hover: #166fe5;
  --fb-gray: #f0f2f5;
  --fb-dark-gray: #65676b;
  --fb-light-gray: #e4e6eb;
  --fb-white: #ffffff;
  --fb-black: #1c1e21;
  --fb-green: #42b72a;
  --fb-red: #ff0000;
  --border-radius: 8px;
  --box-shadow: 0 1px 2px rgba(0, 0, 0, 0.2);
  --transition: all 0.3s ease;
}

body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica,
    Arial, sans-serif;
  margin: 0;
  padding: 0;
  background-color: var(--fb-gray);
  color: var(--fb-black);
  line-height: 1.34;
  /* Removido: overflow: hidden; e height: 100vh; */
}

.app-container {
  display: flex;
  flex-direction: column;
  height: 100vh; /* Alterado de height para min-height */
}

.header {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  height: 56px; /* Ajuste conforme necessário */
}

.content-wrapper {
  display: flex;
  flex: 1;
  overflow: hidden;
  padding-top: 56px; /* Altura do cabeçalho fixo */
  max-width: 1200px;
  margin: 0 auto;
  width: 100%;
  /* Removido: overflow: hidden; */
}

.sidebar {
  width: 280px;
  padding: 20px;
  overflow-y: auto;
  background-color: var(--fb-white);
  height: calc(100vh - 56px); /* Altura total menos a altura do header */
}

.user-info {
  display: flex;
  align-items: center;
  padding: 12px 0;
  margin-bottom: 8px;
}

.user-avatar {
  width: 36px;
  height: 36px;
  border-radius: 50%;
  margin-right: 12px;
}

.user-name {
  font-weight: 600;
  font-size: 15px;
}

.sidebar nav ul {
  list-style-type: none;
  padding: 0;
  margin: 0;
}

.sidebar nav li {
  margin-bottom: 4px;
}

.sidebar nav a {
  display: flex;
  align-items: center;
  padding: 8px 12px;
  border-radius: 8px;
  color: var(--fb-black);
  text-decoration: none;
  transition: var(--transition);
}

.sidebar nav a:hover,
.sidebar nav a.active {
  background-color: var(--fb-light-gray);
}

.sidebar nav i {
  margin-right: 12px;
  font-size: 20px;
  width: 24px;
  text-align: center;
}

.main-content {
  flex: 1;
  padding: 20px;
  overflow-y: auto;
  /* Removido: height: 100%; */
  max-width: 800px;
  width: 100%;
  padding-bottom: 60px; /* Adicione espaço para o footer */
}

.footer {
  height: 40px; /* Ajuste conforme necessário */
}

@media (max-width: 1200px) {
  .content-wrapper {
    padding: 76px 20px 0; /* 56px (header) + 20px (padding-top) */
  }
}

@media (max-width: 992px) {
  .content-wrapper {
    flex-direction: column;
  }

  .sidebar {
    width: 100%;
    height: auto;
    max-height: 30vh;
  }

  .main-content {
    height: calc(
      100vh - 56px - 30vh - 40px
    ); /* Ajuste para considerar header, sidebar e footer */
    max-height: none;
  }
}
</style>
