<script setup lang="ts">
import { ref, shallowRef, onMounted, watch } from "vue";

// Definição da interface SubTask
interface SubTask {
  id: number;
  text: string;
  status: "emProducao" | "concluida" | "abandonada";
}

// Definição das props e emits
const props = defineProps<{
  todoId: number;
  initialSubTasks: SubTask[];
}>();

const emit = defineEmits<{
  (e: "updateSubTasks", todoId: number, subTasks: SubTask[]): void;
}>();

// Estado reativo para controle das subtarefas
const newSubTask = ref("");
const subTasks = shallowRef<SubTask[]>([]);
let nextSubTaskId = ref(1);

// Inicialização e observação das subtarefas
onMounted(() => {
  subTasks.value = props.initialSubTasks;
  nextSubTaskId.value = Math.max(...subTasks.value.map((st) => st.id), 0) + 1;
});

watch(
  () => props.initialSubTasks,
  (newSubTasks) => {
    subTasks.value = [...newSubTasks];
    nextSubTaskId.value = Math.max(0, ...newSubTasks.map((st) => st.id)) + 1;
  },
  { deep: true }
);

// Funções para manipulação de subtarefas
const addSubTask = () => {
  if (newSubTask.value.trim() !== "") {
    const newTask: SubTask = {
      id: nextSubTaskId.value++,
      text: newSubTask.value.trim(),
      status: "emProducao",
    };
    subTasks.value.push(newTask);
    newSubTask.value = "";
    emitUpdate();
  }
};

const updateSubTaskStatus = (
  subTask: SubTask,
  newStatus: "concluida" | "abandonada"
) => {
  const index = subTasks.value.findIndex((st) => st.id === subTask.id);
  if (index !== -1) {
    subTasks.value[index] = { ...subTask, status: newStatus };
    emitUpdate();
  }
};

const removeSubTask = (subTaskId: number) => {
  subTasks.value = subTasks.value.filter((st) => st.id !== subTaskId);
  emitUpdate();
};

const emitUpdate = () => {
  emit("updateSubTasks", props.todoId, subTasks.value);
};
</script>

<template>
  <!-- Estrutura das subtarefas -->
  <div class="sub-tasks">
    <h4><i class="fas fa-tasks"></i> Sub-tarefas</h4>
    <div class="sub-task-input">
      <input
        v-model.trim="newSubTask"
        @keyup.enter="addSubTask"
        placeholder="Adicionar sub-tarefa"
      />
      <button
        @click="addSubTask"
        :disabled="!newSubTask.trim()"
        class="add-btn"
      >
        <i class="fas fa-plus"></i> Adicionar
      </button>
    </div>
    <transition-group name="list" tag="ul" class="sub-task-list">
      <li v-for="subTask in subTasks" :key="subTask.id" class="sub-task-item">
        <div class="sub-task-content">
          <i :class="getStatusIcon(subTask.status)"></i>
          <span :class="subTask.status">
            {{ subTask.text }}
          </span>
        </div>
        <div class="sub-task-actions">
          <button
            v-if="subTask.status === 'emProducao'"
            @click="updateSubTaskStatus(subTask, 'concluida')"
            class="action-btn complete"
            title="Concluir"
          >
            <i class="fas fa-check"></i>
          </button>
          <button
            v-if="subTask.status === 'emProducao'"
            @click="updateSubTaskStatus(subTask, 'abandonada')"
            class="action-btn abandon"
            title="Abandonar"
          >
            <i class="fas fa-times"></i>
          </button>
          <button
            @click="removeSubTask(subTask.id)"
            class="action-btn remove"
            title="Remover"
          >
            <i class="fas fa-trash-alt"></i>
          </button>
        </div>
      </li>
    </transition-group>
  </div>
</template>

<style scoped>
/* Estilos específicos das subtarefas */
.sub-tasks {
  background-color: var(--light-gray);
  margin-top: 1rem;
  border-radius: var(--border-radius);
  padding: 1rem;
  box-shadow: var(--box-shadow);
}

h4 {
  margin-bottom: 1rem;
  color: var(--ts-dark);
  font-size: 1.2rem;
  display: flex;
  align-items: center;
}

h4 i {
  margin-right: 0.5rem;
  color: var(--vue-green);
}

.sub-task-input {
  display: flex;
  margin-bottom: 1rem;
}

.sub-task-input input {
  flex-grow: 1;
  padding: 0.5rem;
  border: 1px solid var(--medium-gray);
  border-radius: var(--border-radius) 0 0 var(--border-radius);
  font-size: 1rem;
  transition: var(--transition);
}

.sub-task-input input:focus {
  outline: none;
  border-color: var(--ts-blue);
}

.add-btn {
  background-color: var(--primary-blue);
  color: var(--white);
  border: none;
  padding: 0.5rem 1rem;
  cursor: pointer;
  border-radius: 0 var(--border-radius) var(--border-radius) 0;
  transition: var(--transition);
  font-size: 1rem;
}

.add-btn:hover {
  background-color: var(--light-blue);
}

.add-btn:disabled {
  background-color: var(--vue-gray);
  cursor: not-allowed;
}

.sub-task-list {
  list-style-type: none;
  padding: 0;
}

.sub-task-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0.75rem;
  background-color: var(--white);
  border: 1px solid var(--light-gray);
  border-radius: var(--border-radius);
  margin-bottom: 0.5rem;
  transition: background-color 0.3s ease, transform 0.3s ease;
}

.sub-task-item:hover {
  background-color: var(--fb-light-gray);
  transform: translateX(5px);
}

.sub-task-content {
  display: flex;
  align-items: center;
}

.sub-task-content i {
  margin-right: 0.5rem;
}

.sub-task-actions {
  display: flex;
  gap: 0.5rem;
}

.action-btn {
  background-color: transparent;
  border: none;
  cursor: pointer;
  font-size: 1rem;
  padding: 0.25rem;
  border-radius: 50%;
  transition: opacity 0.3s ease, transform 0.3s ease;
  opacity: 0.7;
}

.action-btn:hover {
  transform: scale(1.1);
}

.complete {
  color: var(--vue-green);
}

.abandon {
  color: #f44336;
}

.remove {
  color: var(--medium-gray);
}

.concluida {
  text-decoration: line-through;
  color: var(--vue-gray);
}

.abandonada {
  text-decoration: line-through;
  color: #f44336;
}

.list-enter-active,
.list-leave-active {
  transition: all 0.5s ease;
}

.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}
</style>

<script lang="ts">
// Função auxiliar para obter ícone do status
function getStatusIcon(status: string): string {
  switch (status) {
    case "emProducao":
      return "fas fa-spinner";
    case "concluida":
      return "fas fa-check-circle";
    case "abandonada":
      return "fas fa-times-circle";
    default:
      return "fas fa-question-circle";
  }
}
</script>
