<template>
  <!-- Esta seção pode ficar vazia se você estiver usando este arquivo apenas para estilos -->
</template>

<script>
// Esta seção pode ficar vazia se você não precisar de lógica
export default {
  name: "TodoListStyles",
};
</script>

<style>
.todo-container {
  background-color: transparent;
  max-width: 800px;
  margin: 0 auto;
}

.add-todo-card {
  background-color: var(--fb-white);
  border-radius: var(--border-radius);
  box-shadow: var(--box-shadow);
  padding: 1rem;
  margin-bottom: 1rem;
  display: flex;
  align-items: flex-start;
}

.user-avatar {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  overflow: hidden;
  margin-right: 1rem;
  flex-shrink: 0;
}

.user-avatar img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.add-todo-input {
  flex-grow: 1;
}

.todo-input {
  width: 100%;
  border: none;
  font-size: 1.2rem;
  padding: 0.75rem 1rem;
  background-color: var(--fb-gray);
  border-radius: 20px;
  transition: all 0.3s ease;
}

.todo-input:focus {
  outline: none;
  box-shadow: 0 0 0 2px var(--fb-blue);
}

.add-todo-actions {
  display: flex;
  justify-content: space-between;
  margin-top: 1rem;
}

.category-select {
  flex-grow: 1;
  margin-right: 1rem;
  padding: 0.5rem;
  border: 1px solid var(--fb-gray);
  border-radius: var(--border-radius);
  font-size: 1rem;
}

.add-btn {
  white-space: nowrap;
  background-color: var(--fb-blue);
  color: white;
  border: none;
  padding: 0.5rem 1rem;
  border-radius: var(--border-radius);
  font-size: 1rem;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.add-btn:hover:not(:disabled) {
  background-color: var(--fb-dark-blue);
}

.add-btn:disabled {
  opacity: 0.6;
  cursor: not-allowed;
}

.todo-tabs {
  display: flex;
  background-color: var(--fb-white);
  border-radius: var(--border-radius);
  overflow: hidden;
  margin-bottom: 1rem;
}

.tab-btn {
  flex: 1;
  padding: 0.75rem;
  border: none;
  background-color: transparent;
  cursor: pointer;
  font-weight: bold;
  color: var(--fb-dark-gray);
  transition: all 0.3s ease;
}

.tab-btn.active {
  background-color: var(--fb-blue);
  color: var(--fb-white);
}

.todo-list {
  display: grid;
  gap: 1rem;
}

.todo-card {
  background-color: var(--fb-white);
  border-radius: var(--border-radius);
  box-shadow: var(--box-shadow);
  overflow: hidden;
  transition: all 0.3s ease;
}

.todo-header {
  display: flex;
  align-items: center;
  padding: 1rem;
  background-color: var(--fb-light-gray);
}

.todo-info {
  flex-grow: 1;
  margin-left: 1rem;
}

.todo-category {
  font-weight: bold;
  display: flex;
  align-items: center;
  color: var(--fb-blue);
}

.todo-category i {
  margin-right: 0.5rem;
}

.todo-timestamp {
  font-size: 0.8rem;
  color: var(--fb-dark-gray);
}

.todo-content {
  padding: 1rem;
  font-size: 1.1rem;
}

.todo-status-bar {
  padding: 0.5rem 1rem;
  background-color: var(--fb-gray);
  font-size: 0.9rem;
  display: flex;
  align-items: center;
}

.status-indicator {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  margin-right: 0.5rem;
}

.status-indicator.emProducao {
  background-color: var(--fb-blue);
}
.status-indicator.concluida {
  background-color: var(--fb-green);
}
.status-indicator.abandonada {
  background-color: var(--fb-red);
}

.todo-actions {
  display: flex;
  padding: 0.75rem;
  border-top: 1px solid var(--fb-light-gray);
}

.action-btn {
  background-color: var(--fb-light-gray);
  color: var(--fb-dark-gray);
  border: none;
  padding: 0.5rem 1rem;
  border-radius: var(--border-radius);
  margin-right: 0.5rem;
  cursor: pointer;
  transition: all 0.3s ease;
}

.action-btn:hover {
  background-color: var(--fb-gray);
}

.action-btn.complete {
  color: var(--fb-green);
}
.action-btn.abandon {
  color: var(--fb-red);
}

.subtask-count {
  background-color: var(--fb-blue);
  color: white;
  border-radius: 50%;
  padding: 0.2rem 0.5rem;
  font-size: 0.8rem;
  margin-left: 0.5rem;
}

.todo-completed {
  opacity: 0.7;
}
.todo-abandoned {
  opacity: 0.7;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

.list-enter-active,
.list-leave-active {
  transition: all 0.5s ease;
}
.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}

@media (max-width: 768px) {
  .todo-tabs {
    flex-wrap: wrap;
  }
  .tab-btn {
    flex-basis: 50%;
  }
  .todo-actions {
    flex-wrap: wrap;
  }
  .action-btn {
    flex-basis: calc(50% - 0.5rem);
    margin-bottom: 0.5rem;
  }
}
</style>
