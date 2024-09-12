<script setup lang="ts">
import { ref, computed } from "vue";
import ConfirmModal from "./ConfirmModal.vue";
import SubTasks from "./SubTasks.vue";
import "./TodoListSyles.vue";

// Definição das interfaces
interface SubTask {
  id: number;
  text: string;
  status: "emProducao" | "concluida" | "abandonada";
}

interface Todo {
  id: number;
  text: string;
  status: "emProducao" | "concluida" | "abandonada";
  category: "trabalho" | "pessoal" | "estudo";
  subTasks: SubTask[];
}

// Definição das props e emits
const props = defineProps<{
  activeFilter: string;
  todos: Todo[];
}>();

const emit = defineEmits<{
  (e: "add-todo", todo: Omit<Todo, "id">): void;
  (e: "update-todo", todo: Todo): void;
}>();

// Estado reativo para controle da lista de tarefas
const newTodo = ref("");
const newTodoCategory = ref("");
const activeTab = ref("todas");
const showAddTodoActions = ref(false);
const expandedTodos = ref<number[]>([]);

// Arrays de categorias e tabs disponíveis
const categories = [
  { value: "todas", label: "Todas" },
  { value: "trabalho", label: "Trabalho" },
  { value: "pessoal", label: "Pessoal" },
  { value: "estudo", label: "Estudo" },
];

const tabs = [
  { value: "todas", label: "Todas" },
  { value: "emProducao", label: "Em Produção" },
  { value: "concluida", label: "Concluídas" },
  { value: "abandonada", label: "Abandonadas" },
];

// Funções para manipulação de tarefas
const addTodo = () => {
  if (newTodo.value.trim() && newTodoCategory.value) {
    emit("add-todo", {
      text: newTodo.value.trim(),
      status: "emProducao",
      category: newTodoCategory.value as "trabalho" | "pessoal" | "estudo",
      subTasks: [],
    });
    newTodo.value = "";
    newTodoCategory.value = "";
  }
};

const updateTodoStatus = (
  todo: Todo,
  newStatus: "concluida" | "abandonada"
) => {
  emit("update-todo", { ...todo, status: newStatus });
};

// Computed property para filtrar tarefas
const filteredTodos = computed(() => {
  if (activeTab.value === "todas") {
    return props.todos;
  }
  return props.todos.filter((todo) => todo.status === activeTab.value);
});

// Lógica para confirmação de abandono de tarefa
const showConfirmModal = ref(false);
const todoToAbandon = ref<Todo | null>(null);

const openConfirmModal = (todo: Todo) => {
  todoToAbandon.value = todo;
  showConfirmModal.value = true;
};

const confirmAbandon = () => {
  if (todoToAbandon.value) {
    updateTodoStatus(todoToAbandon.value, "abandonada");
  }
  showConfirmModal.value = false;
};

// Função para atualizar subtarefas
const updateSubTasks = (todoId: number, updatedSubTasks: SubTask[]) => {
  const index = props.todos.findIndex((t) => t.id === todoId);
  if (index !== -1) {
    emit("update-todo", { ...props.todos[index], subTasks: updatedSubTasks });
  }
};

// Função para alternar a expansão de uma tarefa
const toggleExpand = (todoId: number) => {
  const index = expandedTodos.value.indexOf(todoId);
  if (index === -1) {
    expandedTodos.value.push(todoId);
  } else {
    expandedTodos.value.splice(index, 1);
  }
};

// Funções auxiliares para obter ícones e labels
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

const getCategoryLabel = (category: string) => {
  const cat = categories.find((c) => c.value === category);
  return cat ? cat.label : "Desconhecida";
};

const getStatusLabel = (status: string) => {
  switch (status) {
    case "emProducao":
      return "Em produção";
    case "concluida":
      return "Concluída";
    case "abandonada":
      return "Abandonada";
    default:
      return "Desconhecido";
  }
};

// Computed property para controle do botão de adicionar
const isAddButtonDisabled = computed(() => {
  return !newTodo.value.trim() || !newTodoCategory.value;
});

// Lógica para mostrar/esconder ações de adicionar tarefa
const hideAddTodoActions = () => {
  if (!newTodo.value.trim() && !newTodoCategory.value) {
    showAddTodoActions.value = false;
  }
};
</script>

<template>
  <!-- Estrutura da lista de tarefas -->
  <div class="todo-container">
    <div class="add-todo-card">
      <div class="user-avatar">
        <img src="../assets/images/image.png" alt="User Avatar" />
      </div>
      <div class="add-todo-input">
        <input
          v-model="newTodo"
          @focus="showAddTodoActions = true"
          @blur="hideAddTodoActions"
          class="todo-input"
          placeholder="No que você está trabalhando?"
        />
        <div v-if="showAddTodoActions" class="add-todo-actions">
          <select v-model="newTodoCategory" class="category-select">
            <option value="">Selecione uma categoria</option>
            <option value="trabalho">Trabalho</option>
            <option value="pessoal">Pessoal</option>
            <option value="estudo">Estudo</option>
          </select>
          <button
            @click="addTodo"
            :disabled="isAddButtonDisabled"
            class="add-btn"
          >
            Adicionar Tarefa
          </button>
        </div>
      </div>
    </div>
    <div class="todo-tabs">
      <button
        v-for="tab in tabs"
        :key="tab.value"
        @click="activeTab = tab.value"
        :class="['tab-btn', { active: activeTab === tab.value }]"
      >
        {{ tab.label }}
      </button>
    </div>

    <div class="todo-list-wrapper">
      <transition-group name="list" tag="div" class="todo-list">
        <div
          v-for="todo in filteredTodos"
          :key="todo.id"
          class="todo-card"
          :class="{
            'todo-completed': todo.status === 'concluida',
            'todo-abandoned': todo.status === 'abandonada',
          }"
        >
          <div class="todo-header">
            <div class="user-avatar">
              <img src="../assets//images/image.png" alt="User Avatar" />
            </div>
            <div class="todo-info">
              <span class="todo-category">
                <i :class="getCategoryIcon(todo.category)"></i>
                {{ getCategoryLabel(todo.category) }}
              </span>
              <span class="todo-timestamp">{{
                new Date().toLocaleString()
              }}</span>
            </div>
            <div class="todo-menu">
              <i class="fas fa-ellipsis-h"></i>
            </div>
          </div>
          <div class="todo-content">
            {{ todo.text }}
          </div>
          <div class="todo-status-bar">
            <span :class="['status-indicator', todo.status]"></span>
            {{ getStatusLabel(todo.status) }}
          </div>
          <div class="todo-actions">
            <button
              v-if="todo.status === 'emProducao'"
              @click="updateTodoStatus(todo, 'concluida')"
              class="action-btn complete"
            >
              <i class="fas fa-check"></i> Concluir
            </button>
            <button
              v-if="todo.status === 'emProducao'"
              @click="openConfirmModal(todo)"
              class="action-btn abandon"
            >
              <i class="fas fa-times"></i> Abandonar
            </button>
            <button @click="toggleExpand(todo.id)" class="action-btn expand">
              <i class="fas fa-comments"></i> Sub-tarefas
              <span class="subtask-count">{{ todo.subTasks.length }}</span>
            </button>
          </div>
          <div
            v-if="expandedTodos.includes(todo.id)"
            class="subtasks-container"
          >
            <SubTasks
              :todoId="todo.id"
              :initialSubTasks="todo.subTasks"
              @updateSubTasks="updateSubTasks"
            />
          </div>
        </div>
      </transition-group>
    </div>
  </div>
  <!-- Modal de confirmação para abandonar tarefa -->
  <ConfirmModal
    :isOpen="showConfirmModal"
    message="Tem certeza que deseja abandonar esta tarefa?"
    @confirm="confirmAbandon"
    @cancel="showConfirmModal = false"
  />
</template>

<style scoped>
.subtasks-container {
  padding: 1rem;
  background-color: var(--fb-light-gray);
  border-top: 1px solid var(--fb-gray);
}

.todo-menu {
  cursor: pointer;
  padding: 0.5rem;
  border-radius: 50%;
  transition: background-color 0.3s ease;
}

.todo-menu:hover {
  background-color: var(--fb-gray);
}

.todo-card {
  transition: box-shadow 0.3s ease, transform 0.3s ease;
}

.todo-card:hover {
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  transform: translateY(-2px);
}

.todo-menu-dropdown {
  position: absolute;
  right: 0;
  top: 100%;
  background-color: var(--fb-white);
  border-radius: var(--border-radius);
  box-shadow: var(--box-shadow);
  padding: 8px 0;
  z-index: 10;
}

.todo-menu-item {
  padding: 8px 16px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.todo-menu-item:hover {
  background-color: var(--fb-light-gray);
}

.todo-card {
  background-color: var(--card-bg);
  color: var(--text-color);
  border: 1px solid var(--border-color);
}
</style>
