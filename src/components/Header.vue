<script setup lang="ts">
// Nenhum script necessário
</script>

<template>
  <header class="header">
    <div class="header-content">
      <div class="logo">
        <i class="fas fa-clipboard-list"></i>
        <h1>TaskMaster</h1>
      </div>
      <div class="search-bar">
        <i class="fas fa-search"></i>
        <input type="text" placeholder="Pesquisar tarefas" />
      </div>
      <div class="user-actions">
        <button class="icon-btn"><i class="fas fa-plus"></i></button>
        <button class="icon-btn"><i class="fas fa-bell"></i></button>
        <button class="icon-btn"><i class="fas fa-user"></i></button>
      </div>
    </div>
  </header>
</template>

<style scoped>
.header {
  background-color: var(--fb-white);
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  height: 56px; /* Altura fixa para o cabeçalho */
}

.header-content {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 8px 16px;
  max-width: 1200px;
  margin: 0 auto;
  width: 100%;
  height: 100%; /* Ocupa toda a altura do cabeçalho */
}

.logo {
  display: flex;
  align-items: center;
  flex-shrink: 0;
}

.logo i {
  font-size: 24px;
  color: var(--fb-blue);
  margin-right: 8px;
}

.logo h1 {
  font-size: 24px;
  font-weight: bold;
  color: var(--fb-blue);
}

.search-bar {
  display: flex;
  align-items: center;
  background-color: var(--fb-gray);
  border-radius: 20px;
  padding: 6px 12px;
  flex: 1;
  max-width: 400px;
  margin: 0 16px;
}

.search-bar i {
  color: var(--fb-dark-gray);
  margin-right: 8px;
}

.search-bar input {
  border: none;
  background-color: transparent;
  font-size: 14px;
  width: 100%;
}

.search-bar input:focus {
  outline: none;
}

.user-actions {
  display: flex;
  gap: 8px;
  order: 2;
}

.icon-btn {
  background-color: var(--fb-gray);
  border: none;
  border-radius: 50%;
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: transform 0.3s ease, background-color 0.3s ease;
}

.icon-btn:hover {
  transform: scale(1.05);
}

.icon-btn i {
  font-size: 18px;
  color: var(--fb-black);
}

@media (max-width: 768px) {
  .header-content {
    flex-wrap: wrap;
  }

  .logo {
    width: 100%;
    margin-bottom: 8px;
  }

  .search-bar {
    order: 3;
    max-width: 100%;
    margin: 8px 0 0;
  }

  .user-actions {
    order: 2;
  }
}
</style>
