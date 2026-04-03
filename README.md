# 🤖 AcademyLetter — Newsletter Semanal de IA

> Workflow automatizado no n8n que coleta, analisa e envia uma newsletter semanal sobre Inteligência Artificial direto no Telegram.

Projeto desenvolvido para o processo seletivo do **Inteli Academy** — Liga de IA do [Inteli (Instituto de Tecnologia e Liderança)](https://www.inteli.edu.br/).

---

## 📌 O que esse workflow faz?

Todo início de semana (segundas às 6h), ou quando disparado manualmente, o workflow:

1. **Coleta notícias** de 5 fontes diferentes em paralelo
2. **Padroniza e consolida** todos os dados em um único bloco
3. **Envia para o Gemini 2.5 Flash**, que gera uma newsletter profissional
4. **Publica automaticamente** no Telegram via bot

---

## 🗺️ Visão geral do workflow

![Visão geral do workflow](assets/prints/01_workflow_completo.png)

---

## 🧩 Fontes de dados utilizadas

| Fonte | O que traz | Precisa de chave? |
|---|---|---|
| **NewsAPI (PT-BR)** | Notícias em português sobre tecnologia | ✅ Sim (gratuita) |
| **NewsAPI (Geral)** | Notícias em inglês sobre IA e LLMs | ✅ Sim (gratuita) |
| **Dev.to** | Artigos técnicos da comunidade dev | ❌ Não |
| **arXiv** | Papers acadêmicos recentes de IA | ❌ Não |
| **Tavily Search** | Busca web otimizada para LLMs | ✅ Sim (gratuita) |

---

## 🚀 Como configurar do zero

### Pré-requisitos

- [n8n](https://n8n.io/) instalado localmente ou em servidor
- Conta gratuita nas APIs abaixo
- Um bot do Telegram criado via @BotFather

---

### 1. Clonar o repositório

```bash
git clone https://github.com/tottithome/Newsletter_n8n_IA.git
cd Newsletter_n8n_IA
```

---

### 2. Criar as contas e obter as API Keys

#### 🔑 NewsAPI
1. Acesse [newsapi.org](https://newsapi.org/) e clique em **Get API Key**
2. Crie uma conta gratuita
3. Copie sua API Key no painel

![Onde encontrar a API Key da NewsAPI](assets/prints/02_newsapi_key.png)

---

#### 🔑 Tavily
1. Acesse [tavily.com](https://tavily.com/) e crie uma conta gratuita
2. No painel, copie sua API Key

![Onde encontrar a API Key da Tavily](assets/prints/03_tavily_key.png)

---

#### 🔑 Google Gemini (Google AI Studio)
1. Acesse [aistudio.google.com](https://aistudio.google.com/)
2. Clique em **Get API Key** → **Create API Key**
3. Copie a chave gerada

![Criando a API Key no Google AI Studio](assets/prints/04_gemini_key.png)

---

#### 🤖 Bot do Telegram
1. Abra o Telegram e busque por **@BotFather**
2. Envie `/newbot` e siga as instruções
3. Copie o **token** que o BotFather vai te enviar
4. Para obter seu **Chat ID**, busque por **@userinfobot** e envie qualquer mensagem — ele vai te responder com seu ID

![Criando o bot no BotFather](assets/prints/05_botfather.png)

---

### 3. Importar o workflow no n8n

1. Abra o n8n no navegador
2. Clique em **Workflows** no menu lateral
3. Clique em **Import from file**
4. Selecione o arquivo `AI_Newsletter_-_Inteli_Academy.json` da raiz do repositório

![Importando o workflow no n8n](assets/prints/06_importar_workflow.png)

---

### 4. Configurar as credenciais no n8n

#### Credencial do Google Gemini
1. No workflow, clique no nó **Message a model**
2. Em **Credential**, clique em **Create new**
3. Cole sua API Key do Google AI Studio
4. Clique em **Save**

![Configurando a credencial do Gemini](assets/prints/07_credencial_gemini.png)

---

#### Credencial do Telegram
1. Clique no nó **Telegram - mandar a newsletter**
2. Em **Credential**, clique em **Create new**
3. Cole o token do seu bot (gerado pelo BotFather)
4. Clique em **Save**

![Configurando a credencial do Telegram](assets/prints/08_credencial_telegram.png)

---

### 5. Inserir as API Keys nos nós HTTP

#### NewsAPI
1. Clique no nó **NewsAPI-PtBr**
2. Na URL, substitua `SUA_NEWSAPI_KEY` pela sua chave real
3. Repita o processo no nó **NewsAPI-Geral**

![Inserindo a chave da NewsAPI](assets/prints/09_newsapi_configurar.png)

---

#### Tavily
1. Clique no nó **Tavily Search**
2. No campo **JSON Body**, substitua `SUA_TAVILY_KEY` pela sua chave real

![Inserindo a chave da Tavily](assets/prints/10_tavily_configurar.png)

---

#### Chat ID do Telegram
1. Clique no nó **Telegram - mandar a newsletter**
2. No campo **Chat ID**, coloque o seu Chat ID (obtido via @userinfobot)

![Inserindo o Chat ID no nó do Telegram](assets/prints/11_telegram_chatid.png)

---

### 6. Testar o workflow

1. Clique no nó **Gancho manual**
2. Clique em **Execute workflow**
3. Aguarde — em alguns segundos a newsletter vai aparecer no seu Telegram!

![Executando o workflow manualmente](assets/prints/12_executar_workflow.png)

![Newsletter recebida no Telegram](assets/prints/13_resultado_telegram.png)

---

## ⏰ Execução automática

O workflow já vem configurado com um **Schedule Trigger** que dispara toda segunda-feira às 6h da manhã automaticamente.

Para ativá-lo, basta clicar no toggle **Active** no canto superior direito do workflow.

![Ativando o workflow automático](assets/prints/14_ativar_workflow.png)

---

## 📁 Estrutura do repositório

```
Newsletter_n8n_IA/
├── AI_Newsletter_-_Inteli_Academy.json   # Arquivo do workflow para importar no n8n
├── README.md                             # Este arquivo
└── assets/
    └── prints/                           # Prints usados no tutorial
```

---

## 🛠️ Tecnologias utilizadas

- **[n8n](https://n8n.io/)** — Plataforma de automação de workflows
- **[Google Gemini 2.5 Flash](https://aistudio.google.com/)** — LLM para geração da newsletter
- **[NewsAPI](https://newsapi.org/)** — Agregador de notícias
- **[Tavily](https://tavily.com/)** — Busca web para LLMs
- **[Dev.to API](https://dev.to/api)** — Artigos da comunidade tech
- **[arXiv API](https://arxiv.org/help/api)** — Papers acadêmicos de IA
- **[Telegram Bot API](https://core.telegram.org/bots/api)** — Envio da newsletter

---

## 📬 Newsletter no Telegram

Acompanhe a newsletter em funcionamento: **[@psInteliAcademy_bot](https://t.me/psInteliAcademy_bot)**

---

## 👤 Autor

Desenvolvido por **[tottithome](https://github.com/tottithome)** para o processo seletivo do Inteli Academy.
