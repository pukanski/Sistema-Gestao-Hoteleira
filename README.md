# Sistema-Gestão-Hoteleira

Um sistema Full-Stack completo para o gerenciamento de reservas de um hotel. O projeto é dividido em uma API RESTful (Node.js) e uma interface de usuário dinâmica e protegida (React). O sistema lida com autenticação, gestão de clientes, quartos e regras de negócio complexas para evitar conflitos de reserva (overbooking e double-booking).

---

##  Tecnologias Utilizadas

**Frontend:**
* **React (via Vite):** Renderização rápida e eficiente.
* **Context API:** Gerenciamento de estado global para a sessão do usuário (`AuthContext`).
* **Axios:** Centralização e interceptação de requisições HTTP para a API.
* **React Router:** Navegação e proteção de rotas (`PrivateRoute`).

**Backend:**
* **Node.js & Express:** Roteamento e controladores da API.
* **Autenticação JWT & Bcrypt:** Geração de tokens e hash de senhas seguro.
* **Swagger:** Documentação automatizada da API (`swagger.json`).
* **Banco de Dados Relacional:** (Modelo populado via `seed.js`).

---

##  Funcionalidades Principais

* ** Autenticação Segura:** Login integrado entre React e Node via JWT. O frontend protege as telas internamente, enquanto o backend bloqueia rotas sem o token `Bearer`. Fluxo de recuperação de senha simulado.
* ** Dashboard Integrado:** Painel centralizado para visão geral do sistema após o login.
* ** Gestão de Clientes:** CRUD completo de hóspedes, com validações estritas (unicidade de CPF e Email).
* ** Gestão de Quartos:** Controle de categorias (Standard, Deluxe, Suíte), preços de diárias e status em tempo real (Disponível, Ocupado, Manutenção).
* ** Gestão de Reservas (Core Business):** * Associação direta entre Cliente e Quarto.
  * **Cálculo Automático:** Valor total calculado dinamicamente com base nos dias e diária.
  * **Prevenção de Conflitos:** Bloqueio de reservas no passado, double-booking (quarto já reservado no período) e overbooking (quarto em manutenção).

---

##  Estrutura do Projeto

```text
/
├── backend/                # API RESTful
│   ├── config/             # Configurações de banco de dados
│   ├── controllers/        # Lógica de negócio das rotas
│   ├── middleware/         # Validação de JWT e regras
│   ├── models/             # Entidades do banco de dados
│   ├── routes/             # Definição dos endpoints
│   └── validators/         # Validações de payload
│
└── frontend/               # Interface de Usuário
    └── src/
        ├── api/            # Instância do Axios
        ├── components/     # Componentes reutilizáveis (Layouts e PrivateRoutes)
        ├── context/        # AuthContext para gerenciamento de sessão
        └── pages/          # Telas (Login, Dashboard, Clientes, Quartos, Reservas)
```

---

##  Como Executar o Projeto (Setup)

Você precisará abrir **dois terminais** para rodar o backend e o frontend simultaneamente.

### 1. Rodando a API (Backend)
Abra o primeiro terminal na pasta raiz e navegue até o backend:
```bash
cd backend
npm install
node seed.js    # Limpa e popula o banco de dados com dados iniciais
node app.js     # Inicia o servidor Node.js
```

### 2. Rodando a Interface (Frontend)
Abra o segundo terminal na pasta raiz e navegue até o frontend:
```bash
cd frontend
npm install
npm run dev     # Inicia o servidor de desenvolvimento do Vite (React)
```

### 3. Acessando o Sistema
Após iniciar ambos os servidores, acesse o link gerado pelo Vite (geralmente `http://localhost:5173`) no seu navegador. Para entrar no sistema, utilize as credenciais de administrador padrão geradas pelo arquivo `seed.js`:

* **Email:** `admin@hotel.com`
* **Senha:** `123`

### 4. Documentação da API (Swagger)
O backend possui uma documentação interativa gerada com Swagger, contendo todos os endpoints, parâmetros e exemplos de requisição. 

Com o backend rodando, acesse no seu navegador:
* **`http://localhost:8081/api-docs`**

---

##  Cobertura de Testes e Validações

O backend possui regras rígidas mapeadas e validadas:
* **Fase de Autenticação:** Bloqueio de acesso sem token (401 Unauthorized).
* **Restrições de Exclusão:** Prevenção contra exclusão de clientes ou quartos que possuam histórico de reservas (Conflito de Chave Estrangeira - 409).
* **Validações de Reserva:** Impede viagens no tempo (reservas no passado), checkout menor que check-in, e faz recálculos automáticos em caso de *update* (ex: alterar a categoria do quarto atualiza o valor total da hospedagem).

---
*Projeto acadêmico desenvolvido para consolidar conceitos de desenvolvimento Full-Stack, integração de APIs, gerenciamento de estado no frontend e regras de negócio complexas no backend.*
