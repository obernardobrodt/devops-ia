# 📖 Guia de Inicialização Local (App v0)

Este documento centraliza as instruções e correções necessárias para subir o ambiente de desenvolvimento local (Backend e Frontend) no **Windows PowerShell**, corrigindo problemas comuns de caminhos e dependências.

---

## 🚀 Pré-requisitos

Antes de iniciar, certifique-se de estar na **raiz do projeto** (`devops-ia`) em todos os terminais abertos no VS Code.

### 🔌 1. Subir o Banco de Dados (Docker)
O backend depende de uma instância ativa do PostgreSQL. 

* **Se for a primeira vez criando o banco:**
```powershell
  docker run --name devops-postgres -e POSTGRES_USER=app -e POSTGRES_PASSWORD=app -e POSTGRES_DB=appdb -p 5432:5432 -d postgres:16

Se o container já existir (apenas parado):

PowerShell
  docker start devops-postgres
💡 Dica: Você pode validar se o banco está online rodando o comando docker ps.

🛠️ Executando a Aplicação
Como o projeto possui arquiteturas independentes em Python, será necessário trabalhar com dois terminais separados no VS Code, ambos com o ambiente virtual (.venv) ativo.

🖥️ Passo 2: Inicializar o Backend (Terminal 1)
Injete a variável de ambiente necessária para a conexão com o banco:

PowerShell
   $env:DATABASE_URL="postgresql://app:app@localhost:5432/appdb"
Ative o ambiente virtual:

PowerShell
   .\app_v0\.venv\Scripts\Activate.ps1
Garanta que o driver do Postgres esteja instalado (Correção de Bug):

PowerShell
   pip install psycopg2-binary
Suba o servidor FastAPI via Uvicorn:

PowerShell
   uvicorn app_v0.backend.main:app --reload --host 127.0.0.1 --port 8000
🎨 Passo 3: Inicializar o Frontend (Terminal 2)
Clique no botão de + no terminal do VS Code para abrir uma nova aba, mantendo o terminal do Backend rodando em paralelo.

Ative o ambiente virtual nesta segunda aba também:

PowerShell
   .\app_v0\.venv\Scripts\Activate.ps1
Execute a interface do Streamlit:

PowerShell
   streamlit run app_v0/frontend/main.py
🏁 Checklist de Sucesso
Se tudo foi feito corretamente, seu ambiente estará distribuído assim:

Banco de Dados: Rodando no Docker na porta 5432

Backend API: Disponível em http://127.0.0.1:8000

Frontend UI: Disponível em http://127.0.0.1:8501 (abrirá automaticamente no navegador)