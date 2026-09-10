# 💸 Notion-Finances

Pipeline ETL em Python para extração, transformação e análise de dados financeiros pessoais integrados ao **Notion**, complementados com indicadores econômicos oficiais do **Banco Central do Brasil (BACEN)**, tais como histórico do **CDI** e cotação do **Dólar (PTAX)**.

---

## 📌 Funcionalidades

- **Integração com Notion API (`notion_api.py`)**:
  - Consulta paginada automática (`has_more` e `next_cursor`) para extrair todos os registros financeiros.
  - Ordenação por Data, Nome e Valor.
  - Extração e padronização dos campos: `ID`, `NAME`, `VALUE`, `TYPE`, `CATEGORY`, `SUB_CATEGORY`, `DATE`, `EFECTIVE_VALUE` e `ACCOUNT`.
  - Tratamento robusto para valores ausentes ou nulos.
  - Estruturação em DataFrame do Pandas.

- **Indicadores do BACEN**:
  - **Taxa CDI (`cdi_api.py`)**: Extração de séries temporais históricas da taxa CDI via API do Banco Central do Brasil (SGS - Sistema Gerenciador de Séries Temporais).
  - **Cotação do Dólar (`dolar_api.py`)**: Extração de cotações PTAX (compra, venda e data/hora) em determinado período através da API Olinda do BACEN.

- **Base de Dados & Análise**:
  - Estrutura pronta para consolidação com Pandas e persistência relacional (suporte configurável para MySQL / SQLAlchemy).

---

## 📂 Estrutura do Projeto

```text
notion-finances/
├── cdi_api.py           # ETL de taxas CDI via API do Banco Central
├── dolar_api.py         # ETL de cotação do Dólar PTAX via API Olinda do BACEN
├── notion_api.py        # ETL de transações financeiras via API do Notion
├── requirements.txt     # Dependências do projeto Python
├── .env                 # Variáveis de ambiente e credenciais (ignorado no git)
└── README.md            # Documentação do projeto
```

---

## 🚀 Como Executar

### 1. Pré-requisitos

- Python 3.10+ instalado
- Conta no [Notion Developers](https://developers.notion.com/) e token de integração configurado com permissão na base de dados

### 2. Clonar o repositório e criar o ambiente virtual

```bash
git clone https://github.com/edermedeiroos/Notion-Finances.git
cd Notion-Finances

# Criar ambiente virtual
python -m venv .venv

# Ativar ambiente virtual
# No Windows (PowerShell):
.venv\Scripts\Activate.ps1
# No Linux/macOS:
source .venv/bin/activate
```

### 3. Instalar dependências

```bash
pip install -r requirements.txt
```

### 4. Configurar variáveis de ambiente

Crie um arquivo `.env` na raiz do projeto com base nas seguintes variáveis:

```env
NOTION_INTERNAL_INTEGRATION_SECRET=seu_token_de_integracao_notion
DATA_SOURCE_ID=id_da_sua_base_de_dados_no_notion

# Configurações do Banco de Dados (opcional/planejado)
DB_USER=root
DB_PASSWORD=sua_senha
DB_HOST=localhost
DB_PORT=3306
DB_DATABASE=notion
```

### 5. Execução dos Scripts

- **Executar extração do Notion**:
  ```bash
  python notion_api.py
  ```

- **Executar extração da taxa CDI**:
  ```bash
  python cdi_api.py
  ```

- **Executar extração do Dólar PTAX**:
  ```bash
  python dolar_api.py
  ```

---

## 🛠️ Tecnologias Utilizadas

- [Python](https://www.python.org/)
- [Pandas](https://pandas.pydata.org/)
- [Requests](https://requests.readthedocs.io/)
- [SQLAlchemy](https://www.sqlalchemy.org/) & [mysql-connector-python](https://dev.mysql.com/doc/connector-python/en/)
- [Notion API](https://developers.notion.com/)
- [APIs Banco Central do Brasil (BACEN)](https://dadosabertos.bcb.gov.br/)

---

## 📄 Licença

Este projeto está sob a licença MIT. Consulte o arquivo [LICENSE](LICENSE) para mais detalhes.
