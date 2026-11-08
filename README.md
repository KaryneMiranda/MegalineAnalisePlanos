# Qual é o Melhor Plano? – Análise de Receita da Megaline

Projeto da Sprint 4 em que comparo dois planos pré-pagos da operadora de telecomunicações Megaline para descobrir qual deles gera mais receita e orientar o orçamento de publicidade.

## Objetivo

Analisar o comportamento de 500 clientes em 2018 e responder:
- Qual plano gera mais receita: **Surf** ou **Ultimate**?
- A receita dos usuários da região de NY-NJ é diferente da receita das demais regiões?

## Planos

| | Surf | Ultimate |
|---|---|---|
| Mensalidade | US$ 20 | US$ 70 |
| Minutos incluídos | 500 | 3.000 |
| Mensagens incluídas | 50 | 1.000 |
| Internet incluída | 15 GB | 30 GB |
| Minuto extra | US$ 0,03 | US$ 0,01 |
| Mensagem extra | US$ 0,03 | US$ 0,01 |
| GB extra | US$ 10 | US$ 7 |

## Dados

| Arquivo | Conteúdo |
|---|---|
| `megaline_users.csv` | 500 clientes: idade, cidade, plano e datas de cadastro e cancelamento |
| `megaline_calls.csv` | 137.735 chamadas com data e duração |
| `megaline_messages.csv` | 76.051 mensagens com data |
| `megaline_internet.csv` | 104.825 sessões de internet com data e volume em MB |
| `megaline_plans.csv` | Condições e preços dos dois planos |

## Etapas

1. **Preparação dos dados:** conversão de datas para `datetime`, arredondamento da duração das chamadas e conversão de MB para GB
2. **Agregação por usuário e mês:** minutos, mensagens e internet consumidos por cliente em cada mês, reunidos em uma única tabela
3. **Cálculo da receita mensal:** mensalidade do plano mais as cobranças pelo que passou dos limites
4. **Análise do comportamento:** estatísticas descritivas, gráficos de barras, histogramas e boxplots de chamadas, mensagens e internet por plano
5. **Testes de hipóteses:** teste t de Welch, já que as variâncias dos grupos são diferentes

## Principais resultados

- **Chamadas:** a duração média das chamadas é parecida nos dois planos, cerca de 7 minutos.
- **Mensagens:** usuários do Ultimate enviam um pouco mais de mensagens, e nos dois planos o volume cresce ao longo do ano.
- **Internet:** o consumo mediano é igual nos dois planos, mas no Ultimate ele é mais disperso.
- **Receita:**

| Plano | Média | Mediana | Desvio padrão |
|---|---|---|---|
| Surf | US$ 32,47 | US$ 20,00 | US$ 39,45 |
| Ultimate | US$ 71,02 | US$ 70,00 | US$ 7,72 |

O **Ultimate gera mais receita por cliente** e tem uma receita muito mais estável. No Surf, a maior parte dos clientes paga só a mensalidade, mas quem passa dos limites pode pagar bem mais. Isso explica o desvio padrão alto.

### Testes de hipóteses (α = 0,05)

| Hipótese nula (H0) | Valor-p | Resultado |
|---|---|---|
| A receita média dos planos Surf e Ultimate é igual | ≈ 0 | Rejeitamos H0: as receitas são diferentes |
| A receita média da região NY-NJ é igual à das demais regiões | ≈ 0,00005 | Rejeitamos H0: as receitas são diferentes |

## Conclusão

Os dois testes indicam diferenças estatisticamente significativas. O **Ultimate** é o plano mais rentável por cliente e o mais previsível, então é o melhor candidato para receber mais investimento em publicidade.

## Tecnologias

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- SciPy

## Como executar

1. Clone o repositório
2. Instale as dependências:
   ```bash
   pip install pandas numpy matplotlib seaborn scipy jupyter
   ```
3. Abra o notebook:
   ```bash
   jupyter notebook projetosprint4.ipynb
   ```

> Observação: o notebook lê os arquivos em `/datasets/`. Ajuste os caminhos se os CSVs estiverem em outra pasta.
