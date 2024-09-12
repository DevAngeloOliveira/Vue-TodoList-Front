<script setup lang="ts">
// Definição das props
defineProps<{
  isOpen: boolean;
  message: string;
}>();

// Definição dos emits
const emit = defineEmits<{
  (e: "confirm"): void;
  (e: "cancel"): void;
}>();

// Funções para confirmar ou cancelar a ação
const confirm = () => {
  emit("confirm");
};

const cancel = () => {
  emit("cancel");
};
</script>

<template>
  <!-- Estrutura do modal de confirmação -->
  <transition name="modal">
    <div v-if="isOpen" class="modal-overlay" @click.self="cancel">
      <div class="modal-content">
        <p>{{ message }}</p>
        <div class="modal-actions">
          <button @click="confirm" class="confirm-btn">Sim</button>
          <button @click="cancel" class="cancel-btn">Não</button>
        </div>
      </div>
    </div>
  </transition>
</template>

<style scoped>
/* Estilos específicos do modal de confirmação */
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.4);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.modal-content {
  background-color: var(--fb-white);
  padding: 1.5rem;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1), 0 8px 16px rgba(0, 0, 0, 0.1);
  text-align: center;
  max-width: 90%;
  width: 400px;
}

.modal-content p {
  font-size: 1.1rem;
  color: var(--fb-black);
  margin-bottom: 1.5rem;
}

.modal-actions {
  display: flex;
  justify-content: flex-end;
  gap: 0.5rem;
}

button {
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  font-weight: 600;
  font-size: 1rem;
  transition: background-color 0.3s ease;
}

.confirm-btn {
  background-color: var(--fb-blue);
  color: var(--fb-white);
}

.confirm-btn:hover {
  background-color: #166fe5;
}

.cancel-btn {
  background-color: var(--fb-light-gray);
  color: var(--fb-black);
}

.cancel-btn:hover {
  background-color: #d8dadf;
}

.modal-enter-active,
.modal-leave-active {
  transition: opacity 0.2s ease;
}

.modal-enter-from,
.modal-leave-to {
  opacity: 0;
}
</style>
