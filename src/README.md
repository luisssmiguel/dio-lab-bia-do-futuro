# 💻 Código da Aplicação: ByteSafe Advisor

Esta seção detalha a implementação técnica do agente, os requisitos de sistema e as instruções para execução local do protótipo funcional.

---

## 🏗️ Estrutura de Arquivos

Diferente da estrutura sugerida, o projeto foi otimizado para uma arquitetura flat na raiz, facilitando o gerenciamento de dependências e caminhos de arquivos locais:

```text
PROJETO-DIO/
├── app.py              # Interface do usuário e fluxo do Streamlit
├── agente.py           # Cérebro da aplicação (Lógica, IA e Dados)
├── requirements.txt    # Lista de bibliotecas necessárias
└── .env                # Variáveis de ambiente (Chaves de API)

## requirements.txt

```
streamlit
pandas
google-generativeai
python-dotenv
audio-recorder-streamlit
openai-whisper
```

## Como Rodar

# Criar o ambiente
python -m venv .venv

# Ativar o ambiente (Windows)
.venv\Scripts\activate

# Ativar o ambiente (Linux/Mac)
source .venv/bin/activate

# Rodar a aplicação
streamlit run app.py
```
