# 📚 Documentação do Agente: ByteSafe Advisor

Este documento detalha o propósito, a arquitetura e as diretrizes de segurança do **ByteSafe Advisor**, um assistente de voz especializado em gestão financeira pessoal.

---

## 🎯 Caso de Uso

### O Problema
A manutenção de um controle financeiro rigoroso em tempo real é frequentemente abandonada devido à burocracia. Abrir aplicativos, navegar por menus e digitar valores manualmente cria uma fricção que gera furos no orçamento e desmotivação.

### A Solução
O **ByteSafe Advisor** elimina essa barreira através de uma interface **Voice-First**. Utilizando modelos de transcrição (Whisper) e inteligência generativa (Gemini), o agente extrai valores e categorias de comandos naturais, atualiza uma base de dados local (CSV) instantaneamente e oferece feedback auditivo e visual sobre a saúde financeira do usuário.

### Público-Alvo
Jovens profissionais, estudantes e entusiastas de tecnologia que buscam agilidade e uma forma intuitiva de gerir suas finanças sem interromper suas rotinas.

---

## 👤 Persona e Tom de Voz

* **Nome do Agente:** ByteSafe Advisor
* **Personalidade:** Consultivo e Educativo. Atua como um mentor digital que organiza dados e incentiva o hábito de poupar.
* **Tom de Comunicação:** Acessível e Direto. Evita jargões técnicos complexos, mas mantém a seriedade necessária para o trato com dinheiro.
* **Exemplos de Linguagem:**
    * *"Olá Luis Miguel! Sou o ByteSafe Advisor. Qual transação vamos organizar agora?"*
    * *"Entendido! Registrei sua despesa de R$ 35,00 em 'Alimentação'. Seu saldo atualizado é de R$ 450,00."*

---

## 🏗️ Arquitetura do Sistema

### Fluxo de Dados
1. **Entrada:** Usuário grava áudio via interface Streamlit.
2. **Transcrição:** O modelo **OpenAI Whisper (Small)** converte o áudio em texto.
3. **Lógica Python:** O script extrai valores via Regex e atualiza o arquivo `transacoes.csv`.
4. **Inteligência:** O **Google Gemini API** recebe o texto e o saldo real para formatar uma resposta contextualizada.
5. **Saída:** O Streamlit exibe o histórico de chat e atualiza a Sidebar com o novo saldo.

### Componentes Técnicos
| Componente | Tecnologia |
| :--- | :--- |
| **Interface** | Streamlit (Python framework) |
| **STT (Speech-to-Text)** | OpenAI Whisper |
| **Cérebro (LLM)** | Google Gemini (Gemini 1.5 Flash) |
| **Persistência** | Pandas & CSV (Armazenamento Local) |
| **Audio Capture** | Audio Recorder Streamlit |

---

## 🛡️ Segurança e Anti-Alucinação

Para garantir a integridade dos dados financeiros do Luis, o agente utiliza as seguintes estratégias:

* **Contexto Estrito:** O agente nunca inventa o saldo. Ele sempre consulta o cálculo matemático feito pelo Python no arquivo CSV antes de responder.
* **Filtro de Ruído:** Implementação de filtros de segurança para evitar que ruídos de áudio ou transcrições errôneas (ex: termos aleatórios) gerem lançamentos fantasmas.
* **Admissão de Falha:** Caso o valor numérico não seja detectado na frase, o agente solicita que o usuário repita a informação de forma clara.
* **Filtro de Escopo:** O agente ignora perguntas não relacionadas a finanças, reforçando seu papel de consultor especializado.

### 🚫 Limitações Declaradas
* O agente **não** realiza transações bancárias reais (PIX ou transferências).
* O agente **não** possui conexão direta com APIs bancárias (opera em base de dados local).
* O processamento exige conectividade com a internet para comunicação com a API do Gemini.
