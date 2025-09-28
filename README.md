# API Banco - FastAPI + SQL Server

Esta é uma **API REST** para gerenciar correntistas e movimentações de um banco fictício, construída com **FastAPI** e conectada a um **SQL Server**.  
O projeto permite consultar correntistas, movimentações e extratos.

---

## ⚙️ Tecnologias utilizadas

- **Python 3.13**
- **FastAPI**: Framework web moderno para APIs
- **SQLAlchemy**: ORM para interagir com o banco de dados
- **SQL Server**: Banco de dados relacional
- **Uvicorn**: Servidor ASGI para rodar a API
- **Pydantic**: Validação e serialização de dados

---

## 📂 Estrutura do Projeto

fastapi_banco/
├─ main.py # Arquivo principal da API
├─ database.py # Conexão com o SQL Server
├─ models.py # Modelos SQLAlchemy (Correntista, Movimentacao)
├─ schemas.py # Schemas Pydantic (para request/response)
├─ crud.py # Funções de acesso ao banco (CRUD)
├─ .env # Variáveis de ambiente (ex: DATABASE_URL)
└─ requirements.txt # Dependências do projeto


---

## ⚡ Como rodar a API

1. **Clonar o projeto**

```bash
git clone <URL_DO_REPOSITORIO>
cd fastapi_banco
Criar e ativar um ambiente virtual

python -m venv .venv
# Windows
.venv\Scripts\activate
# Linux/Mac
source .venv/bin/activate


Instalar as dependências

pip install -r requirements.txt


Configurar o banco de dados

Crie o arquivo .env na raiz do projeto com a URL de conexão:

DATABASE_URL=mssql+pyodbc://@DESKTOP-U5SFQEC\SQLEXPRESS/SistemasCorporativos?driver=ODBC+Driver+18+for+SQL+Server&trusted_connection=yes&TrustServerCertificate=yes


Substitua DESKTOP-U5SFQEC\SQLEXPRESS pelo seu servidor SQL Server.

Rodar a API

uvicorn main:app --reload


A API estará disponível em:

http://127.0.0.1:8000

📝 Endpoints disponíveis
1. Listar Correntistas
GET /correntistas


Exemplo de resposta:

[
  {
    "CorrentistaID": 1,
    "NomeCorrentista": "João Silva",
    "Saldo": 1500.50
  }
]

2. Listar Movimentações
GET /movimentacoes


Exemplo de resposta:

[
  {
    "MovimentacaoID": 1,
    "TipoOperacao": "C",
    "CorrentistaID": 1,
    "ValorOperacao": 500.00,
    "DataOperacao": "2025-09-28T15:30:00",
    "Descricao": "Depósito em conta",
    "CorrentistaBeneficiarioID": null
  }
]

3. Extrato de um Correntista
GET /extrato/{correntista_id}


Exemplo:

GET http://127.0.0.1:8000/extrato/1


Exemplo de resposta:

[
  {
    "CorrentistaID": 1,
    "NomeCorrentista": "João Silva",
    "TipoOperacao": "Crédito",
    "MovimentacaoID": 1,
    "Descricao": "Depósito em conta",
    "DataOperacao": "2025-09-28T15:30:00",
    "ValorOperacao": 500.00,
    "BeneficiarioID": null,
    "NomeBeneficiario": null
  }
]

🔗 Testando a API

Você pode usar o navegador ou ferramentas como Postman ou Insomnia.

FastAPI fornece documentação automática:

Swagger: http://127.0.0.1:8000/docs

ReDoc: http://127.0.0.1:8000/redoc

✅ Observações

Certifique-se de que o SQL Server esteja rodando e que a base SistemasCorporativos exista.

Ajuste o driver ODBC caso tenha versão diferente do SQL Server.

As tabelas e views já estão configuradas para correntistas, movimentações e extratos.
