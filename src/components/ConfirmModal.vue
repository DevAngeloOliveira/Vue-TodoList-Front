<script setup lang="ts">
defineProps<{
  isOpen: boolean;
  message: string;
}>();

const emit = defineEmits<{
  (e: "confirm"): void;
  (e: "cancel"): void;
}>();

const confirm = () => {
  emit("confirm");
};

const cancel = () => {
  emit("cancel");
};
</script>

<template>
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
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.modal-content {
  background-color: var(--white);
  padding: 2rem;
  border-radius: var(--border-radius);
  box-shadow: var(--box-shadow);
  text-align: center;
  max-width: 90%;
  width: 400px;
}

button {
  padding: 0.75rem 1.5rem;
  border: none;
  border-radius: var(--border-radius);
  cursor: pointer;
  font-weight: bold;
  transition: var(--transition);
}

.confirm-btn {
  background-color: var(--primary-blue);
  color: var(--white);
}

.confirm-btn:hover {
  background-color: var(--light-blue);
}

.cancel-btn {
  background-color: var(--medium-gray);
  color: var(--white);
}

.cancel-btn:hover {
  background-color: var(--dark-gray);
}

.modal-enter-active,
.modal-leave-active {
  transition: opacity 0.3s ease;
}

.modal-enter-from,
.modal-leave-to {
  opacity: 0;
}

.modal-actions {
  display: flex;
  justify-content: center;
  gap: 1rem;
  margin-top: 1.5rem;
}
</style>
