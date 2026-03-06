# 🍽️ Classificador de Intenções – API

![Node](https://img.shields.io/badge/node.js-20-green)
![TypeScript](https://img.shields.io/badge/typescript-5-blue)
![Fastify](https://img.shields.io/badge/framework-fastify-black)
![Tests](https://img.shields.io/badge/tests-vitest-yellow)
![AI](https://img.shields.io/badge/AI-LLM-purple)

API REST desenvolvida em **Node.js + TypeScript** para classificar automaticamente mensagens de clientes de restaurantes em **categorias de intenção**.

Este projeto foi desenvolvido como parte de um **desafio técnico para Estágio em Inteligência Artificial**, com foco em:

- Integração com **Modelos de Linguagem (LLMs)**
- **Prompt Engineering**
- Estrutura de API limpa e escalável
- Testes automatizados

A API pode ser utilizada para **automatizar triagem de mensagens de clientes**, direcionando solicitações para o fluxo correto de atendimento.

---

# 🚀 Tecnologias Utilizadas

- **Node.js**
- **TypeScript**
- **Fastify**
- **OpenAI / Gemini (LLMs compatíveis)**
- **Vitest** – testes automatizados

A aplicação **não utiliza banco de dados**.  
O arquivo `conversas-exemplo.json` funciona como uma **base de validação do classificador**.

---

# 📌 Categorias de Intenção

| Categoria | Descrição | Exemplo |
|--------|--------|--------|
| PEDIDO_CARDAPIO | Dúvidas ou pedidos sobre o cardápio | "Vocês têm pizza de calabresa?" |
| STATUS_ENTREGA | Perguntas sobre andamento do pedido | "Meu pedido já saiu?" |
| RECLAMACAO | Problemas ou insatisfação do cliente | "Minha pizza veio fria" |
| ELOGIO | Feedback positivo | "A comida de vocês é ótima!" |
| OUTROS | Mensagens que não se encaixam nas categorias | "Boa noite" |

---

# 🏗️ Arquitetura da Aplicação

A aplicação segue uma estrutura simples baseada em **separação de responsabilidades**.

```
src
│
├── controllers # Recebe requisições HTTP
├── services # Regras de negócio e integração com IA
├── routes # Definição de rotas
├── prompts # Prompt utilizado pelo classificador
├── tests # Testes automatizados
├── utils # Funções auxiliares
└── server.ts # Inicialização da aplicação
```

Fluxo de funcionamento:


Request -> Controller -> Service -> LLM -> Classificação -> Response


---

# ▶️ Como Rodar o Projeto

### 1️⃣ Clonar repositório

```bash
git clone <url-do-repositorio>
```
2️⃣ Entrar na pasta
```
cd classificador-intencoes
```
3️⃣ Instalar dependências
```
npm install
```
4️⃣ Criar arquivo .env

Exemplo:
```
OPENAI_API_KEY=sua_chave
PORT=3333
```
5️⃣ Rodar o projeto
```
npm run dev
```
Servidor disponível em:
```
http://localhost:3333
```
📦 Endpoints
Classificar mensagem

POST /classify

Classifica uma mensagem em uma categoria de intenção.

Exemplo de requisição:
```
{
  "message": "Vocês têm pizza de calabresa?"
}
```
Exemplo de resposta
```
{
  "category": "PEDIDO_CARDAPIO",
  "confidence": 0.92
}
```
Classificação com contexto
A API também permite classificar mensagens considerando histórico da conversa.

Exemplo:
```
{
  "messages": [
    "Boa noite",
    "Meu pedido já saiu para entrega?"
  ]
}
```
🧪 Validação do classificador

POST /validate

Utiliza o arquivo conversas-exemplo.json para validar o desempenho do classificador.

Exemplo de resposta:
```
{
  "total": 25,
  "correct": 23,
  "accuracy": 0.92,
  "byCategory": {
    "PEDIDO_CARDAPIO": 1,
    "STATUS_ENTREGA": 0.8,
    "RECLAMACAO": 1,
    "ELOGIO": 1,
    "OUTROS": 0.8
  },
  "errors": []
}
```



🧪 Testes Automatizados

Foi implementado um teste automatizado para o endpoint /classify utilizando Vitest.

Durante os testes:
  O serviço responsável pela comunicação com a IA é mockado
    
  Não há chamadas reais para APIs externas

Executar testes:
```
npm run test
```
🔄 Suporte a Múltiplos Provedores de IA

A aplicação foi projetada para permitir troca fácil de provedor de IA.

Atualmente compatível com:
  OpenAI
  Gemini
  Outros LLMs compatíveis

Isso é possível graças ao isolamento da integração de IA na camada de service.


