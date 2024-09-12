<script setup lang="ts">
// Nenhum script necessário para o footer
</script>

<template>
  <!-- Estrutura do rodapé -->
  <footer class="footer">
    <div class="footer-content">
      <p>&copy; 2024 TaskMaster - Vue + Laravel</p>
      <div class="social-icons">
        <a
          href="https://github.com/DevAngeloOliveira"
          target="_blank"
          rel="noopener noreferrer"
          title="GitHub"
        >
          <i class="fab fa-github"></i>
        </a>
        <a
          href="https://www.linkedin.com/in/gabriel-%C3%A2ngelo-b71565267/"
          target="_blank"
          rel="noopener noreferrer"
          title="LinkedIn"
        >
          <i class="fab fa-linkedin"></i>
        </a>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.footer {
  background-color: var(--fb-white);
  border-top: 1px solid var(--fb-light-gray);
  padding: 8px 16px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.footer-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  max-width: 1200px;
  margin: 0 auto;
  width: 100%;
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
  transition: color 0.3s ease;
}

.social-icons a:hover {
  color: var(--fb-blue);
}

@media (max-width: 768px) {
  .footer-content {
    flex-direction: column;
    align-items: center;
    gap: 8px;
  }

  p {
    font-size: 0.8rem;
  }

  .social-icons {
    gap: 10px;
  }

  .social-icons a {
    font-size: 1em;
  }
}
</style>
