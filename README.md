# APA - Introdução à Ciência de Dados (Fatecie)

Atividade Prática de Aprendizagem: 7 exercícios em Python usando **numpy**, **pandas** e **matplotlib**,
organizados no notebook `APA_introducao_ciencia_dados.ipynb`.

| # | Exercício | Ferramenta |
|---|---|---|
| 1 | Série com o número de alunos por titulação | `pd.Series` |
| 2 | Tabela com o número de alunos por titulação | `pd.DataFrame` |
| 3 | Tabela de calorias e % de gordura por item | `pd.DataFrame` com índice |
| 4 | Matriz com 50 elementos e 3 dimensões | `np.array(...).reshape(2, 5, 5)` |
| 5 | Gráfico de pizza com 3 itens, destacando um | `plt.pie(..., explode=...)` |
| 6 | Gráfico de linha com título, eixos e legenda | `plt.plot` |
| 7 | Gráfico de dispersão com pontos em estrela | `plt.scatter(..., marker='*')` |

O enunciado original está em [`docs/`](docs/).

---

## Estrutura do projeto

```
atividade-fatecie-introducao-dados/
├── APA_introducao_ciencia_dados.ipynb   # notebook com os 7 exercícios
├── docs/                                # enunciado da atividade (PDF)
├── pyproject.toml                       # definição do projeto e dependências (uv)
├── uv.lock                              # versões exatas travadas pelo uv
├── requirements.txt                     # mesmas versões, para quem usa pip
├── .python-version                      # versão do Python usada pelo uv (3.13)
└── README.md
```

## Requisitos

- **Python 3.11 ou superior** (o projeto usa 3.13 por padrão, definido em `.python-version`).
- **Uma** das opções abaixo para instalar as dependências:
  - [uv](https://docs.astral.sh/uv/) (recomendado): também baixa o Python certo, se necessário;
  - ou `pip` + `venv`, que já vêm com o Python.

Dependências instaladas (ver `pyproject.toml`):

| Pacote | Para quê |
|---|---|
| `numpy`, `pandas`, `matplotlib` | Bibliotecas usadas nos exercícios |
| `jupyterlab` | Interface do Jupyter no navegador |
| `ipykernel` | Kernel Python que executa as células |
| `nbconvert` | Executar o notebook pela linha de comando e exportar para HTML |

---

## Opção 1: com uv (recomendado)

### 1. Instalar o uv (apenas uma vez)

Windows (PowerShell):

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

Linux / macOS:

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Feche e abra o terminal e confira com `uv --version`.

### 2. Criar o ambiente e instalar as dependências

Na pasta do projeto:

```bash
uv sync
```

Esse comando:
- baixa o Python 3.13 se ele não estiver instalado;
- cria o ambiente virtual em `.venv/`;
- instala exatamente as versões do `uv.lock`.

### 3. Abrir o Jupyter no navegador

```bash
uv run jupyter lab
```

O navegador abre em `http://localhost:8888/lab`. Se não abrir sozinho, copie o link com `?token=...`
que aparece no terminal. Abra `APA_introducao_ciencia_dados.ipynb` e use
**Run → Run All Cells** (ou `Shift+Enter` célula por célula).

Para encerrar o Jupyter: `Ctrl+C` no terminal (confirme com `y` se for perguntado).

> Prefere a interface clássica? `uv run --with notebook jupyter notebook`.

### 4. Executar sem abrir o navegador (opcional)

Executa todas as células e gera um relatório HTML com as tabelas e os gráficos:

```bash
uv run jupyter nbconvert --to html --execute APA_introducao_ciencia_dados.ipynb
```

Gera `APA_introducao_ciencia_dados.html`, que abre em qualquer navegador.

Para salvar os resultados dentro do próprio notebook:

```bash
uv run jupyter nbconvert --to notebook --execute --inplace APA_introducao_ciencia_dados.ipynb
```

Se alguma célula der erro, o comando para e mostra a célula e a mensagem. Por isso, ele também
serve como teste rápido de que tudo funciona.

---

## Opção 2: com pip + venv

### 1. Criar e ativar o ambiente virtual

Windows (PowerShell):

```powershell
py -3.13 -m venv .venv
.\.venv\Scripts\Activate.ps1
```

Windows (cmd):

```bat
py -3.13 -m venv .venv
.venv\Scripts\activate.bat
```

Linux / macOS:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

Com o ambiente ativo, o terminal mostra `(.venv)` no início da linha.

### 2. Instalar as dependências

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

### 3. Abrir o Jupyter

```bash
jupyter lab
```

Execução sem navegador (com o ambiente ativo):

```bash
jupyter nbconvert --to html --execute APA_introducao_ciencia_dados.ipynb
```

Para sair do ambiente virtual: `deactivate`.

---

## Usando no VS Code

1. Rode `uv sync` (ou a Opção 2) para criar o `.venv`.
2. Abra o notebook no VS Code (precisa das extensões **Python** e **Jupyter**).
3. Clique em **Select Kernel** (canto superior direito) → **Python Environments…** → **.venv**.
4. Use **Run All**.

## Usando no Google Colab

No Colab as bibliotecas já vêm instaladas, então nada deste README é necessário:
**Arquivo → Fazer upload de notebook**, escolha o `.ipynb` e use **Ambiente de execução → Executar tudo**.

---

## Problemas comuns

**"Running cells with 'Python 3.x' requires the ipykernel package"** (VS Code)
: O VS Code está usando o Python global. Selecione o kernel do `.venv` (veja *Usando no VS Code*).

**`Activate.ps1 cannot be loaded because running scripts is disabled`** (PowerShell)
: Libere scripts só para o seu usuário e ative de novo:
  `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned`

**`ModuleNotFoundError: No module named 'pandas'`**
: O Jupyter está rodando fora do ambiente virtual. Use `uv run jupyter lab`, ou ative o `.venv`
  antes de rodar `jupyter lab`.

**Porta 8888 em uso**
: Outro Jupyter já está aberto. Feche-o ou use outra porta: `uv run jupyter lab --port 8889`.

**Acentos aparecem estranhos no terminal do Windows**
: É só a exibição do console. O notebook e os arquivos estão em UTF-8 e aparecem corretos no
  Jupyter/VS Code. Se quiser corrigir o terminal, rode `chcp 65001` antes.

**Os gráficos não aparecem**
: Confira se a célula termina com `plt.show()` e se a célula de imports (a primeira) foi executada.

---

## Manutenção das dependências

As dependências ficam em `pyproject.toml`. O `uv.lock` e o `requirements.txt` são gerados a partir dele.

```bash
uv add seaborn                     # adicionar um pacote
uv remove seaborn                  # remover um pacote
uv lock --upgrade                  # atualizar para as versões mais novas permitidas
uv sync                            # aplicar as mudanças no .venv

# regenerar o requirements.txt depois de qualquer mudança
uv export --format requirements-txt --no-hashes --no-header --no-annotate -o requirements.txt
```
