# 📚 Base de Conhecimento

## Dados Utilizados

O ByteSafe Advisor utiliza os datasets da pasta `data` para garantir que cada resposta seja personalizada e baseada no histórico real do cliente.

| Arquivo | Formato | Utilização do ByteSafe Advisor |
| :--- | :--- | :--- |
| `historico_atendimento.csv` | CSV | Consultar interações passadas para manter a continuidade da conversa (ex: saber se o usuário já perguntou sobre uma dívida antes). |
| `perfil_investidor.json` | JSON | Identificar o nível de tolerância ao risco para sugerir onde poupar o dinheiro que "sobrou" no mês. |
| `produtos_financeiros.json` | JSON | Cruzar os dados do perfil com as opções do banco para recomendar o investimento ideal via voz. |
| `transacoes.csv` | CSV | Fonte principal de dados para o cálculo de saldo, detecção de gastos excessivos e categorização de despesas. |

---

## Adaptações nos Dados

Os dados originais foram expandidos para incluir **metas de gastos diários** vinculadas ao perfil do investidor. 
- Clientes com perfil "Conservador" recebem alertas mais rigorosos quando o saldo em `transacoes.csv` diminui rapidamente.
- Adicionei um mapeamento de **sinônimos de voz** para as categorias do CSV (ex: o termo falado "comi um lanche" é mapeado para a categoria "Alimentação" presente no dataset).

---

## Estratégia de Integração

### Como os dados são carregados?
Os arquivos são carregados utilizando a biblioteca **Pandas** no início da execução do script Python. Para garantir performance, os dados do `perfil_investidor.json` são mantidos em cache durante a sessão, enquanto o `transacoes.csv` é lido a cada nova inserção para garantir que o saldo falado seja sempre o mais atualizado.

### Como os dados são usados no prompt?
Utilizo uma estratégia de **Injeção de Contexto Dinâmico**. O agente não recebe o arquivo inteiro (para não gastar tokens), mas sim um resumo estruturado no **System Prompt**:
1. O saldo é calculado somando as receitas e subtraindo as despesas do `transacoes.csv`.
2. O perfil do investidor é extraído do JSON para definir o "tom de voz" (mais cauteloso ou mais arrojado).
3. O histórico de atendimento é resumido para que o agente saiba o contexto das últimas 3 frases ditas pelo usuário.

---

## Exemplo de Contexto Montado

Abaixo, um exemplo de como os dados brutos são transformados em texto para a "mente" do ByteSafe Advisor:

```text
[CONTEXTO DO SISTEMA]
Você é o ByteSafe Advisor. 
Dados do Cliente:
- Nome: Luis Miguel
- Perfil: Arrojado (extraído de perfil_investidor.json)
- Saldo calculado: R$ 1.860,50 (baseado em transacoes.csv)

Histórico Recente:
- O cliente perguntou sobre 'investimentos em renda variável' na última sessão.
- Gasto elevado detectado em: 'Eletrônicos' (R$ 1.200,00).

[ENTRADA DE VOZ DO USUÁRIO]
"Quanto eu ainda posso gastar hoje?"
