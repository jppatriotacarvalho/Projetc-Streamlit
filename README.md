# Dashboards de Aluguel por Temporada na América Latina

Projeto da disciplina **Análise e Visualização de Dados (AVD)** — CESAR School, 2026.2.

App em Streamlit com dois dashboards construídos a partir de uma EDA de anúncios de aluguel por temporada (tipo Airbnb) em cidades da América Latina:

- **Dashboard 1:** correlação e distribuição das variáveis quantitativas.
- **Dashboard 2:** KPIs para um público-alvo.

O deploy é feito via **Streamlit Community Cloud**.

**Link do app:** (em breve)

## Setup

Comandos para Windows, rodados na raiz do projeto:

| Passo | Comando |
|---|---|
| Criar o ambiente virtual | `py -m venv .venv` |
| Ativar no PowerShell | `.venv\Scripts\Activate.ps1` |
| Ativar no cmd | `.venv\Scripts\activate.bat` |
| Instalar dependências | `python -m pip install -r requirements.txt` |
| Instalar as skills do Streamlit | `streamlit skills --yes` |
| Rodar o app | `streamlit run app.py` |

> **Dica:** se o PowerShell bloquear a execução de scripts ao ativar o venv, rode uma vez:
> `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned`

## Dados: `data/raw` vs `data/clean`

- **`data/raw/`** — dado bruto (`listings.csv`, `past_rates.csv`). **Não é versionado**: os arquivos são grandes e contêm dados sensíveis, como o ID do anfitrião e a localização exata dos imóveis. No Git fica só o `.gitkeep`.
- **`data/clean/`** — dado tratado e anonimizado (`dataset.csv`), exportado pelo notebook de EDA. **É versionado de propósito**: o app no Streamlit Community Cloud só enxerga o que está no repositório do GitHub.

Fluxo: `data/raw` → notebook (EDA + tratamento) → `data/clean/dataset.csv` → `src/data_loader.load_data()` → `app.py`.

## Estrutura do projeto

```
streamlit_avd_pratica/
├── app.py                    ← o app inteiro: sidebar + dashboards, roda de cima pra baixo
├── src/
│   ├── __init__.py           ← vazio, só transforma src/ em pacote
│   └── data_loader.py        ← load_data() lê data/clean/dataset.csv com @st.cache_data
├── data/
│   ├── raw/                  ← dado bruto (listings.csv, past_rates.csv): NÃO vai pro Git
│   └── clean/                ← dado tratado (dataset.csv): VAI pro Git (o deploy só enxerga o repo)
├── notebooks/                ← eda.ipynb + eda-com-downloads.ipynb (exporta raw/clean)
├── entregas/                 ← rascunhos dos dashboards + justificativa das métricas
├── prompts/                  ← template de prompt + declaração de uso de IA
├── .streamlit/config.toml    ← tema / identidade visual
├── requirements.txt
├── README.md
└── .gitignore
```
