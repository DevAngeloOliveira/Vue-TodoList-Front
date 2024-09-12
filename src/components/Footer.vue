<script setup lang="ts">
// Nenhum script necessário
</script>

<template>
  <footer class="footer">
    <div class="footer-content">
      <p>&copy; 2024 Aplicativo de Lista de Tarefas - Vue + Laravel</p>
      <div class="social-icons">
        <a
          href="https://github.com/DevAngeloOliveira"
          target="_blank"
          rel="noopener noreferrer"
          title="GitHub"
          ><i class="fab fa-github"></i
        ></a>
        <a
          href="https://www.linkedin.com/in/gabriel-%C3%A2ngelo-b71565267/"
          target="_blank"
          rel="noopener noreferrer"
          title="LinkedIn"
          ><i class="fab fa-linkedin"></i
        ></a>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.footer {
  background-color: var(--fb-white);
  border-top: 1px solid var(--fb-light-gray);
  padding: 16px 0;
  height: 50px; /* Altura fixa para o rodapé */
}

.footer-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 16px;
  height: 100%; /* Ocupa toda a altura do rodapé */
}

p {
  margin: 0;
  font-size: 0.9rem;
  color: var(--fb-dark-gray);
}

.social-icons {
  display: flex;
  gap: 15px;
}

.social-icons a {
  color: var(--fb-dark-gray);
  font-size: 1.2em;
  transition: transform 0.3s ease, color 0.3s ease;
}

.social-icons a:hover {
  transform: translateY(-2px);
  color: var(--fb-blue);
}

@media (max-width: 768px) {
  .footer-content {
    flex-direction: column;
    text-align: center;
  }

  .social-icons {
    margin-top: 8px;
  }
}
</style>
