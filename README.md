# TaskMaster - Gerenciador de Tarefas Vue + Laravel

TaskMaster é uma aplicação web moderna para gerenciamento de tarefas, construída com Vue.js 3 no frontend e Laravel no backend (backend não incluído neste repositório).

## Características

- Interface de usuário intuitiva e responsiva
- Criação, edição e exclusão de tarefas
- Categorização de tarefas (Trabalho, Pessoal, Estudo)
- Status de tarefas (Em Produção, Concluída, Abandonada)
- Subtarefas para melhor organização
- Filtros e abas para fácil navegação
- Design inspirado no Facebook para familiaridade do usuário

## Tecnologias Utilizadas

- Vue.js 3
- TypeScript
- Vite (para build e desenvolvimento)
- Font Awesome (para ícones)

## Estrutura do Projeto

O projeto está organizado da seguinte forma:

- `src/`
  - `components/`: Componentes Vue reutilizáveis
  - `App.vue`: Componente raiz da aplicação
  - `main.ts`: Ponto de entrada da aplicação
- `public/`: Arquivos estáticos
- `index.html`: Página HTML principal

## Componentes Principais

### App.vue
Componente raiz que gerencia o estado global e renderiza os componentes principais.

### Header.vue
Cabeçalho da aplicação com logo, barra de pesquisa e ícones de ação.

### TodoList.vue
Componente principal para exibição e gerenciamento de tarefas.

### SubTasks.vue
Gerencia as subtarefas de cada tarefa principal.

### ConfirmModal.vue
Modal de confirmação para ações importantes, como abandonar uma tarefa.

### Footer.vue
Rodapé da aplicação com informações de copyright e links sociais.

## Estilos

Os estilos estão definidos em `TodoListStyles.vue` e utilizam variáveis CSS para manter consistência no design.

## Como Executar

1. Clone o repositório
2. Instale as dependências:
   ```
   npm install
   ```
3. Execute o servidor de desenvolvimento:
   ```
   npm run dev
   ```
4. Abra o navegador em `http://localhost:5173`

## Build para Produção

Para criar uma build de produção:
```
npm run build
```
Os arquivos serão gerados na pasta `dist/`.

## Contribuindo

Contribuições são bem-vindas! Por favor, leia as diretrizes de contribuição antes de submeter pull requests.

## Licença

Este projeto está licenciado sob a [Licença MIT](LICENSE).

## Contato

Para mais informações, entre em contato através do [GitHub](https://github.com/DevAngeloOliveira) ou [LinkedIn](https://www.linkedin.com/in/gabriel-%C3%A2ngelo-b71565267/).