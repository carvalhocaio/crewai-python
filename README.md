# Coordenando Equipes de Agentes de IA com CrewAI em Python

Este repositório contém a implementação prática do tutorial **"CrewAI in Python: Coordinating Teams of AI Agents"** do [Real Python](https://realpython.com/crewai-python/). O projeto demonstra como construir e coordenar equipes de agentes inteligentes especializados usando o framework CrewAI e os modelos **Gemini (Google)**.

---

## Índice
- [Visão Geral](#visão-geral)
- [Estrutura do Projeto](#estrutura-do-projeto)
- [Pré-requisitos](#pré-requisitos)
- [Instalação e Configuração](#instalação-e-configuração)
- [Como Executar os Exemplos](#como-executar-os-exemplos)
  - [1. Agente Único (`single_agent.py`)](src/single_agent.py)
  - [2. Equipe de Pesquisa e Escrita (`research_and_writer_crew.py`)](src/research_and_writer_crew.py)
  - [3. Controle Explícito de Contexto (`explicit_context.py`)](src/explicit_context.py)
  - [4. Agente com Ferramentas de Scraping (`agent_with_tool.py`)](src/agent_with_tool.py)
- [Desenvolvimento e Qualidade do Código](#desenvolvimento-e-qualidade-do-código)
- [Conceitos Importantes do CrewAI](#conceitos-importantes-do-crewai)

---

## Visão Geral

O **CrewAI** é um framework de orquestração multiagente focado em engenharia de agentes de alto desempenho. Diferente de prompts gigantescos onde pedimos para um modelo atuar em várias frentes diferentes, o CrewAI permite estruturar uma equipe ("crew") onde cada agente possui um papel (`role`), objetivo (`goal`) e histórico (`backstory`) bem definidos.

Neste projeto:
- Gerenciamos o ambiente virtual e dependências usando **`uv`** (gerenciador de pacotes rápido para Python).
- Desenvolvemos scripts independentes baseados nos exemplos apresentados no tutorial do Real Python.
- Utilizamos os modelos **Google Gemini** (`gemini-2.5-flash` e `gemini-2.5-pro`) como motores das tarefas cognitivas.
- Garantimos qualidade e formatação de código por meio do **Ruff** integrado em comandos `Makefile`.

---

## Estrutura do Projeto

Os scripts desenvolvidos na pasta `src/` ilustram o avanço gradativo na complexidade do uso do CrewAI:

1. **`src/single_agent.py`**:
   - Criação de um único agente (`Travel Advisor`) encarregado de sugerir destinos econômicos no Sudeste Asiático.
   - Ideal para entender a anatomia básica de um agente (`Agent`), de uma tarefa (`Task`) e do kickoff de uma tripulação (`Crew`).

2. **`src/research_and_writer_crew.py`**:
   - Conecta dois agentes trabalhando em equipe: um Analista de Pesquisa Sênior (`Senior Research Analyst`) e um Escritor de Conteúdo (`Content Writer`).
   - Mostra o comportamento padrão do pipeline sequencial, em que a saída gerada pela pesquisa é passada automaticamente como entrada para a tarefa de escrita.

3. **`src/explicit_context.py`**:
   - Explica o uso do parâmetro `context` em objetos `Task`.
   - Demonstra como especificar explicitamente que uma tarefa depende dos resultados gerados por tarefas anteriores específicas, o que é fundamental para fluxos mais complexos ou não lineares.

4. **`src/agent_with_tool.py`**:
   - Equipa o agente de pesquisa com ferramentas (`tools`).
   - Utiliza a ferramenta `ScrapeWebsiteTool` para realizar scraping ao vivo do site [python.org/downloads](https://www.python.org/downloads/) e retornar a versão de lançamento e data estável do Python mais recente. A saída alimenta o redator (`Tech Blogger`) que cria um anúncio conciso.

---

## Pré-requisitos

Para rodar o projeto localmente, você precisará de:
- **Python 3.12** ou superior.
- **`uv`** instalado em sua máquina. Caso não tenha, você pode instalá-lo seguindo as [instruções oficiais](https://github.com/astral-sh/uv).
- Uma chave de API do Gemini, que pode ser gerada gratuitamente no [Google AI Studio](https://aistudio.google.com/).

---

## Instalação e Configuração

1. **Clone o repositório:**
   ```bash
   git clone https://github.com/carvalhocaio/crewai-python
   cd crewai-python
   ```

2. **Instale as dependências e crie o ambiente virtual:**
   ```bash
   uv sync
   ```

3. **Configure as variáveis de ambiente:**
   Crie um arquivo `.env` na raiz do projeto (ou edite o existente) e insira sua chave de API do Gemini:
   ```env
   GEMINI_API_KEY="sua_chave_do_gemini_aqui"
   ```

---

## Como Executar os Exemplos

Todos os exemplos podem ser disparados facilmente através do `uv run python`:

### 1. Agente Único
```bash
uv run python src/single_agent.py
```

### 2. Equipe de Pesquisa e Escrita
```bash
uv run python src/research_and_writer_crew.py
```

### 3. Controle Explícito de Contexto
```bash
uv run python src/explicit_context.py
```

### 4. Agente com Ferramentas de Scraping
```bash
uv run python src/agent_with_tool.py
```

---

## Desenvolvimento e Qualidade do Código

O projeto conta com um **Makefile** que empacota tarefas rotineiras de linting e formatação usando o **Ruff**:

- **Verificar erros e estilo (Linter):**
  ```bash
  make lint
  ```
- **Corrigir automaticamente avisos do Linter:**
  ```bash
  make lint-fix
  ```
- **Formatar o código:**
  ```bash
  make format
  ```
- **Validar linter e formatação juntos:**
  ```bash
  make check
  ```

---

## Conceitos Importantes do CrewAI

- **Role, Goal & Backstory**: Formam a "identidade" do agente. Quanto mais específicos forem os detalhes aqui fornecidos, mais coesa e realista será a atuação do LLM no respectivo papel.
- **Expected Output**: Toda tarefa (`Task`) requer a definição de uma saída esperada. Isso ajuda a calibrar a assertividade do resultado de forma muito mais confiável.
- **Context**: Permite alimentar tarefas com os retornos exatos de outras tarefas anteriores no grafo, assegurando que o fluxo de informação faça sentido lógico.
- **Tools**: Estendem o potencial dos agentes, transformando-os de meras "caixas de texto estáticas" em agentes capazes de ler páginas webs, consultar bancos de dados ou operar APIs de terceiros.

---

*Este repositório foi construído para fins educacionais com base no tutorial [CrewAI in Python: Coordinating Teams of AI Agents](https://realpython.com/crewai-python/) do site **Real Python**.*
