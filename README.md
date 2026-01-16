# Quantum Finance — data-driven-recommendation-system (FIAP)

Python · Recommender Systems · Notebook · License

# 📋 Visão Geral
Prova de Conceito (PoC) de Sistema de Recomendação para a fintech QuantumFinance, usando dados consentidos do Open Finance para sugerir produtos/serviços financeiros relevantes aos clientes.

Abordagem: User-Based Collaborative Filtering (CF) com Similaridade do Cosseno e Correlação de Pearson, gerando recomendações com explicação simples (clientes semelhantes + contribuição).

---

# 🔑 Key Results

- Construção da matriz usuário × item (intensidade de relação/interesse)
- Recomendações Top-N por cliente com 2 medidas de similaridade (Cosseno e Pearson)
- Saída final: ranking de produtos + score + “por quê” (clientes similares que puxaram a recomendação)
- Estrutura pronta para evoluir para híbrido, conteúdo, métricas offline e A/B tests

---

# 📁 Estrutura do projeto

```
img/                     # Gráficos, tabelas e outputs do notebook
├── 01_dataset_preview.png
├── 02_user_item_matrix_preview.png
├── 03_cosine_similarity_heatmap.png
├── 04_pearson_similarity_heatmap.png
├── 05_topn_recommendations_example.png
└── ...

notebooks/               # Notebook principal do projeto
└── recommendations_systems.ipynb

outputs/                 # Resultados gerados (tabelas recomendação, rankings)
models/                  # (opcional) se guardar artefatos no futuro

README.md                # Documentação do projeto
```

---

# 🧠 Técnicas e Abordagem

- Sistema de recomendação baseado em Filtragem Colaborativa por Usuário (User-Based CF):
- Matriz usuário × item (intensidade)
- Representa quanto cada cliente “tem relação” com um produto (ex.: possui, usa, transaciona, tem volume etc.).
- Medidas de similaridade
- Cosine Similarity (0 a 1): compara padrão de consumo/produtos em vetores normalizados
- Pearson Correlation (-1 a 1): captura similaridade de “tendência” (variações relativas), útil quando escalas diferem
- Geração de recomendações (Top-N)
- Identifica clientes mais similares ao cliente-alvo
- Agrega sinais dos vizinhos para itens não consumidos
- Retorna ranking + score e, quando possível, explicação (quem contribuiu)

---

# 📌 Por que esta técnica?

- Excelente para PoC quando há sobreposição de produtos entre clientes
- Interpretável e fácil de explicar para stakeholders
- Baixo custo computacional para cenários pequenos/médios

---

# 🚀 Como Usar
1) Instalação (requirements.txt)
- Pré-requisitos
- Python 3.8+
- Git (opcional)
- Instalar dependências
- pip install -r requirements.txt

2) Reprodutibilidade
- O notebook principal concentra o fluxo completo (dados → matriz → similaridade → recomendações → outputs).
- Recomenda-se rodar em ambiente limpo (Colab ou venv local).

3) Rodar o projeto
- Opção A — Google Colab (recomendado)
- Abrir o notebook: Open in Colab
- Executar as células em ordem (Runtime → Run all)
- Opção B — Local
- Abrir notebooks/recommendations_systems.ipynb no Jupyter/VS Code
- Garantir dependências: pip install -r requirements.txt

4) Outputs gerados
- Imagens para leitura rápida no GitHub (pasta img/)
- Tabelas de recomendações e rankings (pasta outputs/)

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1ypiJz4l5GtgyZQM-fty0Rh8cxRwpa_vJ?usp=sharing)

---

# 📊 Dataset
- Fonte: Dataset reduzido fornecido na disciplina (Open Finance – handson).
- Formato típico: .txt contendo um dicionário/estrutura com clientes e seus produtos/sinais.
- Obs.: este projeto utiliza apenas dados consentidos e não trabalha com identificadores diretos sensíveis.

---

# 🔎 O que foi feito no notebook
- Importação e leitura da base
- Leitura do arquivo do dataset (estrutura em dict)
- Padronização de chaves e produtos
- Construção do catálogo de produtos
- Lista única de produtos/serviços no ecossistema do dataset
- Matriz usuário × item (intensidade)
- Transformação dos dados brutos em matriz (clientes nas linhas, produtos nas colunas)
- Definição de intensidade (ex.: binário 0/1 ou peso por volume/frequência — conforme dataset)
- Cálculo de similaridade entre usuários
- Similaridade do Cosseno (matriz NxN)
- Correlação de Pearson (matriz NxN)
- Geração de recomendações (Top-N)
- Seleção dos K vizinhos mais próximos
- Score por produto com agregação ponderada pela similaridade
- Remoção de itens já consumidos
- Explicabilidade simples
- Para cada item recomendado: “clientes similares X/Y/Z contribuíram com peso W”
- Exemplos práticos
- Recomendações para um conjunto de clientes-alvo
- Tabela final pronta para colar em apresentação

---

# 🏆 Resultados (Resumo Executivo)
- O protótipo entrega um pipeline completo de recomendação:
- Entrada: clientes + produtos (Open Finance)
- Processamento: matriz usuário×item → similaridade → ranking Top-N
- Saída: lista de recomendações por cliente, com score e explicação simples

---

# 📌 Exemplo de Saída
- Cliente (amostra): Client_007
- Recomendações (Cosine): Cartão Premium, Seguro Vida, Investimento Renda Fixa
- Score: 0.82 | 0.77 | 0.69

- **“Por quê”:** baseado em clientes similares Client_021 (+0.31), Client_112 (+0.28), Client_054 (+0.23)

---

# ✅ Entregáveis

✅ Entregável 1 — Contexto e Objetivo
- Problema: recomendação personalizada de produtos/serviços financeiros
- Valor: elevar relevância, apoiar cross-sell/upsell e melhorar experiência do cliente

✅ Entregável 2 — Protótipo Operacional
- Notebook executável com fluxo completo
- Outputs salvos para leitura rápida no GitHub

✅ Entregável 3 — Modelo e Métricas (base)
- Similaridade calculada (Cosseno e Pearson)
- Validações iniciais (sanity checks, exemplos, consistência)

✅ Entregável 4 — Explicabilidade
- Recomendações com indicação de quais vizinhos contribuíram para cada sugestão

---

# 🔧 Funcionalidades
- Constrói matriz usuário × item (intensidade)
- Calcula similaridade de usuários por Cosseno e Pearson
- Gera recomendações Top-N por cliente
- Fornece “reasons” simples (vizinhos que puxaram a recomendação)
- Exporta tabelas e imagens para uso em slide/relatório

---

# 🔐 Segurança e Privacidade
- Dados tratados como consentidos (Open Finance)
- Evita exposição de identificadores diretos sensíveis
- Explicabilidade simples para auditoria e governança inicial

---

# 📦 Dependências
- Python 3.8+
- NumPy: cálculos
- Pandas: manipulação
- Scikit-learn: cosine_similarity e utilitários
- Matplotlib/Seaborn: visualizações (opcional, para outputs)

---

# 🛣️ Próximos Passos (Evolução realista)
- Métricas offline: Precision@K, Recall@K, MAP@K, NDCG
- Ajuste de intensidade (pesos por frequência/volume/tempo) e normalizações
- Cold-start: recomendações por conteúdo (perfil/segmento)
- Modelo híbrido (CF + conteúdo)
- Recomendação online e experimentos: A/B tests
- Governança: logs, explicações padronizadas e monitoramento de performance

---

# 📚 Referências
- Open Finance Brasil (conceitos e ecossistema)
- Técnicas: User-Based Collaborative Filtering, Cosine Similarity, Pearson Correlation
- Boas práticas: avaliação offline (Precision@K, Recall@K) e testes online (A/B)

---

# 📄 Licença
Este projeto é uma prova de conceito desenvolvida para fins acadêmicos.

---

# 👥 Autores
Projeto desenvolvido para o Case Study de Recommendation Systems (FIAP).

---












# Sistema de Recomendação — Open Finance — QuantumFinance

> **Recommender System (PoC)** usando dados de Open Finance para sugerir produtos/serviços financeiros relevantes aos clientes.  
> Abordagem: **User-Based Collaborative Filtering** com **Similaridade do Cosseno** e **Correlação de Pearson**.

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1ypiJz4l5GtgyZQM-fty0Rh8cxRwpa_vJ?usp=sharing)


---

## 📌 Visão Geral
Este projeto implementa um **Sistema de Recomendação (SR)** para a fintech **QuantumFinance**, explorando dados consentidos do ecossistema **Open Finance** para gerar recomendações personalizadas.

**Objetivo de negócio**
- Aumentar relevância das ofertas (cross-sell/upsell)
- Melhorar experiência do cliente com sugestões contextualizadas
- Criar base para evolução (híbrido, conteúdo, online learning, A/B tests)

---

## 🧠 Técnica Implementada
- **Filtragem Colaborativa Baseada em Usuários (User-Based CF)**
- **Similaridade do Cosseno** (0 a 1)
- **Correlação de Pearson** (-1 a 1)

**Por que esta técnica?**
- Boa para **prova de conceito** quando há sobreposição de produtos entre clientes
- É **interpretável** e fácil de explicar para stakeholders
- Baixo custo computacional para cenários pequenos/médios

---

## 📁 Estrutura do Repositório
```open-finance-recommender/
├── notebooks/
│   └── recommendations_systems.ipynb   # Notebook principal (EDA + SR + recomendações)
├── README.md
└── .gitignore
```

## 🚀 Como executar (rápido)

### Opção A — Abrir no Google Colab
Abra o notebook principal:
- [`notebooks/recommendations_systems.ipynb`](./notebooks/recommendations_systems.ipynb)

> Dica: adicione aqui o botão **Open in Colab** para execução 1-click.



