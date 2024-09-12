<script setup lang="ts">
import { ref } from "vue";

const isSearchFocused = ref(false);
const notificationCount = ref(3); // Exemplo de contagem de notificações

const toggleNotifications = () => {
  // TODO: Implementar lógica para abrir/fechar notificações
  console.log("Toggle notificações");
};
</script>

<template>
  <!-- Estrutura do cabeçalho -->
  <header class="header">
    <div class="header-content">
      <div class="logo">
        <i class="fas fa-clipboard-list"></i>
        <h1>TaskMaster</h1>
      </div>
      <div class="search-bar" :class="{ 'search-bar-focus': isSearchFocused }">
        <i class="fas fa-search"></i>
        <input
          type="text"
          placeholder="Pesquisar tarefas"
          @focus="isSearchFocused = true"
          @blur="isSearchFocused = false"
        />
      </div>
      <div class="user-actions">
        <button class="icon-btn" title="Adicionar tarefa" ">
          <i class="fas fa-plus"></i>
        </button>
        <button
          class="icon-btn"
          title="Notificações"
          @click="toggleNotifications"
        >
          <i class="fas fa-bell"></i>
          <span v-if="notificationCount" class="notification-badge">{{
            notificationCount
          }}</span>
        </button>
        <button class="icon-btn" title="Perfil" >
          <i class="fas fa-user"></i>
        </button>
        <!-- Removido: botão de alternar tema -->
      </div>
    </div>
    <!-- ... (código do cabeçalho) ... -->
  </header>
</template>

<style scoped>
.header {
  background-color: #ffffff;
  border-bottom: 1px solid #e0e0e0;
  padding: 8px 16px;
}
.header-content {
  display: flex;
  align-items: center;
  justify-content: space-between;
  max-width: 1200px;
  margin: 0 auto;
}
.logo {
  display: flex;
  align-items: center;
  color: #1877f2;
  font-weight: bold;
}
.logo i {
  font-size: 24px;
  margin-right: 8px;
}
.logo h1 {
  font-size: 18px;
}
.search-bar {
  flex-grow: 1;
  max-width: 600px;
  margin: 0 16px;
  position: relative;
  background-color: #f0f2f5;
  border-radius: 20px;
  padding: 4px 12px;
  display: flex;
  align-items: center;
  transition: box-shadow 0.3s ease;
}
.search-bar-focus {
  box-shadow: 0 0 0 2px #1877f2;
}
.search-bar i {
  color: #65676b;
  margin-right: 8px;
  pointer-events: none; /* Impede que o ícone seja selecionável */
}
.search-bar input {
  flex-grow: 1;
  border: none;
  background-color: transparent;
  font-size: 14px;
  padding: 4px 0;
  outline: none;
}
.user-actions {
  display: flex;
  gap: 8px;
}
.icon-btn {
  background-color: transparent;
  border: none;
  border-radius: 50%;
  width: 36px;
  height: 36px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  position: relative;
  transition: background-color 0.3s ease;
}
.icon-btn:hover {
  background-color: #f0f2f5;
}
.icon-btn:active {
  background-color: #e4e6eb;
}
.icon-btn i {
  font-size: 18px;
  color: #050505;
}
.notification-badge {
  position: absolute;
  top: -5px;
  right: -5px;
  background-color: #fa3e3e;
  color: white;
  border-radius: 50%;
  padding: 2px 5px;
  font-size: 12px;
  font-weight: bold;
}
@keyframes pulse {
  0% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.1);
  }
  100% {
    transform: scale(1);
  }
}
.icon-btn:hover .notification-badge {
  animation: pulse 0.5s infinite;
}
@media (max-width: 768px) {
  .logo h1 {
    display: none;
  }
  .search-bar {
    max-width: 50%;
  }
}
/* Estilos específicos do cabeçalho */
/* ... (estilos CSS) ... */
</style>
