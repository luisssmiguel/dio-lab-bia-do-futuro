# 📚 Base de Conhecimento: Estrutura de Dados

O **ByteSafe Advisor** opera através de um ecossistema de dados local, garantindo privacidade e personalização ao utilizar os datasets presentes na pasta `data`.

---

## 📂 Arquivos Utilizados

| Arquivo | Formato | Papel no Ecossistema ByteSafe |
| :--- | :--- | :--- |
| `transacoes.csv` | CSV | **Fonte de Verdade:** Base para cálculo de saldo real, detecção de gastos e categorização automática. |
| `perfil_investidor.json` | JSON | **Personalidade:** Define a tolerância ao risco e o tom de voz dos alertas financeiros. |
| `produtos_financeiros.json` | JSON | **Catálogo:** Lista de investimentos recomendados quando o usuário possui saldo positivo. |
| `historico_atendimento.csv` | CSV | **Contexto:** Armazena interações passadas para manter a continuidade do atendimento. |

---

## 🛠️ Adaptações e Lógica de Dados

Para otimizar a experiência de voz e a precisão do Agente, implementamos as seguintes camadas lógicas:

1. **Persistência de Saldo Inicial:** Diferente de uma aplicação volátil, o primeiro valor informado pelo usuário é cravado no `transacoes.csv` com a tag `SALDO_INICIAL`, servindo de âncora para todos os cálculos futuros.
2. **Mapeamento de Sinônimos:** O agente utiliza lógica de texto para converter termos falados (ex: "comi um lanche") em categorias estruturadas (ex: "Alimentação").
3. **Alertas por Perfil:** Clientes com perfil **Conservador** recebem alertas de sistema mais rigorosos quando o saldo diminui rapidamente, enquanto perfis **Arrojados** recebem sugestões de diversificação.

---

## 🔄 Estratégia de Integração

### 1. Carregamento e Performance
Os dados são manipulados utilizando a biblioteca **Pandas**. Para garantir performance e evitar latência:
* O `perfil_investidor.json` é carregado no início da sessão.
* O `transacoes.csv` é consultado e atualizado a cada interação via `st.rerun()`, garantindo que o saldo exibido na **Sidebar** seja sempre o valor real em disco.

### 2. Injeção de Contexto Dinâmico (RAG Local)
Para economizar tokens e focar no que importa, o Agente não lê o arquivo inteiro a cada prompt. O sistema Python injeta apenas um **Resumo Estruturado** no System Prompt:
* **Cálculo de Saldo:** O Python processa a matemática e entrega o resultado pronto para a IA.
* **Filtro de Histórico:** Apenas as últimas transações e interações relevantes são enviadas como contexto.

---

## 📝 Exemplo de Prompt Injetado (Back-end)

Abaixo, um exemplo de como o sistema organiza os dados brutos antes de enviá-los para o processamento do modelo Gemini:

```text
[DADOS DO SISTEMA - VERDADE ABSOLUTA]
Usuário: Luis Miguel
Perfil: Arrojado (perfil_investidor.json)
Saldo em Disco: R$ 1.860,50 (calculado via Pandas em transacoes.csv)

[HISTÓRICO RECENTE]
1. O usuário perguntou sobre 'Cripto' na última conversa.
2. Alerta: Gasto elevado detectado em 'Eletrônicos'.

[ENTRADA DO USUÁRIO]
"Quanto eu ainda posso gastar hoje?"
