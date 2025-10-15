# banco-api-performance


Repositório dedicado a testes de performance (carga e estresse) para a API de um sistema bancário, utilizando a ferramenta k6.

O objetivo é proporcionar que os endpoints críticos da aplicação, como `login` e `transferências`, suportem o volume esperado de tráfego e atendam aos requisitos de tempo de resposta sob diferentes condições de carga.

## 💻 Tecnologias Utilizadas

| Tecnologia | Descrição |
| :--- | :--- |
| **k6** | Ferramenta open source para testes de carga e performance. |
| **JavaScript (ES6+)** | Linguagem utilizada para escrever e configurar os scripts de teste. |
| **Visual Studio Code** | IDE utilizada para desenvolvimento e edição dos scripts. |
| **GJSON** | Para extração de dados em respostas JSON . |
| **`BASE_URL`**| Variável de ambiente para configuração dinâmica. |


## 📁 Estrutura do Repositório

BANCO-API-PERFORMANCE/
├── config/        # Arquivo de configuração de variáveis de ambiente.
│   └── config.local.json
├── fixtures/      # Dados de entrada para os testes (ex: usuários, payloads).
│   └── postLogin.json
├── helpers/       # Funções utilitárias reutilizáveis para interação com a API.
│   └── autenticacao.js
├── tests/         # Casos de testes organizados por módulo da API.
│   ├── login.test.js
│   └── transferencias.test.js
├── utils/         # Funções utilitárias reutilizáveis.
│   └── variaveis.js
├── html-report.html
└── README.md


## 🎯 Objetivo de Cada Grupo de Arquivo

| Diretório/Arquivo | Objetivo |
| :--- | :--- |
| **`config/`** | Contém arquivos de configuração específicos para diferentes ambientes (ex: `config.local.json` para desenvolvimento/teste local). |
| **`fixtures/`** | Armazena dados estáticos no formato JSON que são utilizados pelos testes, como _payloads_ (corpos de requisição) fixos. Exemplo: `postLogin.json` contém dados de usuário para login. |
| **`helpers/`** | Módulos JavaScript que contêm funções auxiliares e lógicas reutilizáveis. Exemplo: `autenticacao.js` deve conter a função para obter o token (login), que é usado por outros testes (como o de transferências). |
| **`tests/`** | Contém os scripts principais de teste de performance em k6. Cada arquivo foca em um cenário específico. Ex: `login.test.js` e `transferencias.test.js`. |
| **`utils/`** | Módulos JavaScript que contêm utilitários e variáveis globais ou constantes que podem ser importadas por qualquer script do projeto. Ex: `variaveis.js`. |
| **`html-report.html`** | Arquivo gerado pelo k6 ao final da execução, contendo o relatório detalhado dos resultados do teste. |

## 🚀 Modo de Instalação e Execução do Projeto

### 1. Instalação do k6

Para executar os testes, é necessário ter o k6 instalado em seu sistema operacional. Siga as instruções oficiais de instalação para a sua plataforma:

- [Instalação do k6 (Documentação Oficial)](https://k6.io/docs/getting-started/installation/)

### 2. Clonagem do Repositório

Clone este repositório para a sua máquina local:

Altere o arquivo `config.local.json` e defina a URL base da API a ser testada:

```json
{
    "baseURL": "http://localhost:3000"
}
```

```bash
k6 run tests/login.test.js
```

Certifique-se de passar a variável de ambiente `BASE_URL`, caso não esteja usando um `config.local.json` ou uma abordagem de carregamento automático:

```bash
k6 run tests/login.test.js -e BASE_URL=http://localhost:3000
```

### 3. Execução com Relatório em Tempo Real e Exportação (Dashbord e HTML)

Para acompanhar a execução em um dashboard web em tempo real e exportar automaticamente o relatório final para o arquivo html-report.html, utilize o seguinte comando, que utiliza variáveis de ambiente específicas do k6 (K6_WEB_DASHBOARD e K6_WEB_DASHBOARD_EXPORT):

```bash
K6_WEB_DASHBOARD="true";
K6_WEB_DASHBOARD_EXPORT="html-report.html";
k6 run tests/transferencias.test.js
-e BASE_URL=http://localhost:3000
```
Após a execução, o k6 fornecerá uma URL para acessar o dashboard, e o relatório final estará disponível no arquivo html-report.html.
