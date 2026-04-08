# 📊 Avaliação e Métricas: ByteSafe Advisor

Este documento detalha o processo de validação, controle de qualidade e métricas de desempenho do **ByteSafe Advisor**, garantindo que o assistente seja preciso no cálculo de saldo e resiliente a erros de entrada.

---

## 🎯 Estratégia de Avaliação

A avaliação do agente é realizada através de um modelo híbrido:
1. **Testes de Caixa Preta:** Validação das saídas do Chat e Sidebar com base em entradas variadas.
2. **Integridade de Persistência:** Verificação física dos registros no arquivo `data/transacoes.csv`.
3. **Observabilidade de Áudio:** Monitoramento da taxa de acerto do modelo Whisper para diferentes tonalidades de voz.

---

## 📈 Métricas de Qualidade

| Métrica | Descrição | Cenário de Sucesso |
| :--- | :--- | :--- |
| **Assertividade de Saldo** | O sistema calcula o valor exato no Python? | Saldo Sidebar == Saldo Real no CSV. |
| **Sincronia IA-Sistema** | A IA evita alucinações matemáticas? | O "Novo Saldo" no Chat é idêntico ao valor soprado pelo Python. |
| **Resiliência de Arquivo** | O agente se recupera caso o CSV suma? | O sistema detecta a ausência do arquivo e solicita novo saldo inicial. |
| **Segurança de Escopo** | O agente evita temas irrelevantes? | Respostas educadas negando solicitações fora do nicho financeiro. |

---

## 🧪 Cenários de Teste (Checklist de Homologação)

### Teste 1: Configuração de Saldo Inicial
* **Entrada:** "Meu saldo inicial é 1500 reais."
* **Expectativa:** Criação do arquivo `transacoes.csv` com a flag `SALDO_INICIAL`.
* **Resultado:** [ ] Passou [ ] Falhou

### Teste 2: Registro de Gasto Dinâmico (Voz)
* **Entrada:** (Áudio) "Gastei 80 reais na pizzaria."
* **Expectativa:** Extração correta do valor (80.0) e categoria (Pizzaria).
* **Resultado:** [ ] Passou [ ] Falhou

### Teste 3: Validação de Override da IA
* **Entrada:** Qualquer gasto após definição de saldo.
* **Expectativa:** A IA deve repetir o saldo calculado pelo Python, ignorando sua própria "intuição" matemática.
* **Resultado:** [ ] Passou [ ] Falhou

### Teste 4: Tratamento de Erro (Out-of-Scope)
* **Entrada:** "Qual a previsão do tempo para Sorocaba?"
* **Expectativa:** Resposta padrão: "Como seu consultor ByteSafe, foco apenas em suas finanças..."
* **Resultado:** [ ] Passou [ ] Falhou

---

## 🛠️ Conclusões e Próximos Passos

### O que funcionou bem:
* A sincronização em tempo real entre o processamento do Agente e a interface Streamlit através do `st.rerun()`.
* A persistência de dados utilizando a biblioteca Pandas para garantir que nenhum centavo seja perdido.

### Pontos de Melhoria:
* **NLP de Categoria:** Implementar uma lógica para remover preposições comuns (ex: transformar "na pizzaria" em apenas "Pizzaria") de forma mais robusta.
* **Latência:** Otimizar o carregamento do modelo Whisper para reduzir o tempo de resposta em máquinas com menos hardware.

---

> **Nota:** Este projeto foi desenvolvido por **Luis Miguel Lemos da Silva** como parte do desafio de Diário Financeiro com IA.
