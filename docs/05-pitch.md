# 🎙️ Pitch: ByteSafe Advisor

Este documento apresenta o roteiro e a proposta de valor do **ByteSafe Advisor**, focando na solução de problemas financeiros reais através da tecnologia.

---

## 1. O Problema (30 seg)
**A Dor do Cliente:**
A principal barreira para o controle financeiro não é a falta de ferramentas, mas a **fricção do registro**. Abrir um aplicativo, navegar por menus e digitar gastos manualmente é uma tarefa burocrática que leva à desistência. Sem registros em tempo real, o usuário perde a noção do seu saldo, resultando em "furos" no orçamento e falta de previsibilidade financeira no fim do mês.

---

## 2. A Solução (1 min)
**Como o Agente Resolve:**
O **ByteSafe Advisor** transforma a gestão financeira em uma conversa natural. Através de uma interface **Voice-First**, o usuário simplesmente fala suas transações. 
* **Processamento de Voz:** Utilizamos o modelo **OpenAI Whisper** para garantir transcrições precisas.
* **Inteligência de Dados:** O **Google Gemini API** extrai entidades (valor e categoria) e fornece feedback contextualizado.
* **Cálculo em Tempo Real:** Uma camada de lógica em **Python (Pandas)** garante que os cálculos matemáticos sejam 100% precisos, atualizando uma base de dados local (CSV) e refletindo o saldo instantaneamente na interface **Streamlit**.

---

## 3. Demonstração (1 min)
**O que é mostrado na prática:**
1.  **Inicialização:** O usuário define seu saldo por voz (Ex: "Tenho 1500 reais") e a barra lateral (Sidebar) atualiza o saldo disponível imediatamente.
2.  **Registro de Gasto:** O usuário grava um comando simples: *"Gastei 50 reais com pizza"*.
3.  **Feedback Instantâneo:** O agente confirma o registro, categoriza o gasto e exibe o novo saldo calculado no Chat e na Sidebar de forma sincronizada.
4.  **Persistência:** Mostramos o arquivo `transacoes.csv` sendo populado em tempo real, garantindo que os dados não se percam após fechar a aplicação.

---

## 4. Diferencial e Impacto (30 seg)
**Inovação e Valor Social:**
O diferencial do ByteSafe é a **eliminação da barreira de entrada**. Ao remover a necessidade de digitação, transformamos o controle financeiro em um hábito sem esforço. 
* **Impacto:** Promove a educação financeira prática, especialmente para jovens profissionais e estudantes que precisam de agilidade.
* **Privacidade:** Os dados são mantidos em uma base local, dando ao usuário controle total sobre suas informações sensíveis.

---

## ✅ Checklist do Pitch
- [x] **Duração:** Roteiro otimizado para 3 minutos.
- [x] **Problema:** Claramente definido (fricção e desistência).
- [x] **Solução:** Demonstrada com stack tecnológica moderna (Streamlit/Python/Gemini).
- [x] **Diferencial:** Foco em Voice-First e integração de dados real-time.

---

Link para o Pitch: https://1drv.ms/f/c/1a599ba6672aaacd/IgCiO7vyL-r4Rbb09jjbA0WfAT0mCgrdmYGtOXoz9vZx0yA?e=VRqHhH
