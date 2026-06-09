# MidWest Logistics S/A - Alocação Ótima de Motoristas às Rotas

## Integrantes

* Adriano Macedo das Mercez Filho - Código
* Nathália Estouco Melo - Código
* Gabriel Bandeira Gonzaga - Slides 
* Lucas Henrique Fogaça Pimenta - Slides 

**Disciplina:** Projeto e Análise de Algoritmos I

---

# 1. Descrição do Problema

A MidWest Logistics S/A é uma operadora logística que atua na região Centro-Oeste do Brasil, possuindo um Centro de Distribuição (CD) em Anápolis-GO e diversos hubs regionais.

Diariamente a empresa precisa definir qual motorista será responsável por cada rota disponível, buscando minimizar os custos operacionais.

O problema consiste em encontrar a melhor atribuição possível entre motoristas e rotas, garantindo que cada motorista execute apenas uma rota e que cada rota seja atribuída a apenas um motorista.

Para resolver esse problema foram implementadas duas abordagens:

* Algoritmo Guloso
* Algoritmo Húngaro

Os resultados obtidos pelas duas abordagens são comparados ao final da execução.

---

# 2. Modelagem Formal do Problema

## Instância

Dado:

* Um conjunto de motoristas:

M = {m₁, m₂, ..., mₙ}

* Um conjunto de rotas:

R = {r₁, r₂, ..., rₙ}

* Uma matriz de custos C, onde:

C(i,j) representa o custo de atribuir o motorista mᵢ à rota rⱼ.

## Objetivo

Encontrar uma atribuição entre motoristas e rotas que minimize o custo total da operação.

Matematicamente:

Minimizar:

Σ C(i,j)

para todas as atribuições realizadas.

## Restrições

* Cada motorista deve ser atribuído a exatamente uma rota.
* Cada rota deve ser atribuída a exatamente um motorista.
* Todas as rotas devem ser atendidas.
* Nenhuma atribuição pode ser repetida.

---

# 3. Estrutura dos Dados

Os dados são armazenados em arquivos CSV.

## motoristas.csv

Contém os motoristas disponíveis.

Campos:

* id_motorista
* nome
* experiencia_anos

## rotas.csv

Contém as rotas disponíveis.

Campos:

* id_rota
* descricao
* origem
* destino

## custos.csv

Contém a matriz de custos.

Campos:

* id_motorista
* id_rota
* custo

Quanto menor o valor do custo, melhor é a combinação motorista-rota.

---

# 4. Algoritmos Implementados

## 4.1 Algoritmo Guloso

A estratégia gulosa seleciona sempre a combinação de menor custo disponível naquele momento.

Passos:

1. Ordenar todos os custos em ordem crescente.
2. Escolher o menor custo disponível.
3. Verificar se motorista e rota ainda não foram utilizados.
4. Realizar a atribuição.
5. Repetir até completar todas as rotas.

### Vantagens

* Implementação simples.
* Execução rápida.

### Desvantagens

* Não garante a solução ótima.

---

## 4.2 Algoritmo Húngaro

O Algoritmo Húngaro é um método clássico para resolver problemas de atribuição ótima.

Ele encontra a combinação de menor custo possível entre os elementos dos dois conjuntos.

### Vantagens

* Garante solução ótima.
* Amplamente utilizado em logística e pesquisa operacional.

### Desvantagens

* Maior custo computacional.

---

# 5. Invariantes e Ideia de Correção

## Algoritmo Guloso

Durante toda a execução:

* Nenhum motorista recebe mais de uma rota.
* Nenhuma rota é atribuída a mais de um motorista.

O algoritmo mantém uma solução válida, porém não necessariamente ótima.

## Algoritmo Húngaro

Durante toda a execução:

* As transformações realizadas na matriz preservam a solução ótima.
* O problema permanece equivalente ao original.

Ao final, o algoritmo produz um matching perfeito de custo mínimo.

---

# 6. Complexidade Computacional

## Algoritmo Guloso

Tempo:

O(n² log n)

Espaço:

O(n²)

A complexidade é dominada pela ordenação da lista de custos.

## Algoritmo Húngaro

Tempo:

O(n³)

Espaço:

O(n²)

Onde n representa a quantidade de motoristas e rotas.

---

# 7. Limitações Conhecidas

## Algoritmo Guloso

* Não garante a solução ótima.
* Pode tomar decisões locais que prejudicam o resultado global.
* Em alguns cenários produz custos significativamente maiores que a solução ótima.

## Algoritmo Húngaro

* Possui complexidade O(n³).
* Pode apresentar maior tempo de execução em instâncias muito grandes.
* Requer a construção completa da matriz de custos.

---

# 8. Testes Realizados

## Teste 1 – Instância Pequena (4x4)

Objetivo:

Validar manualmente as atribuições e comparar os algoritmos.

Dados:

* 4 motoristas
* 4 rotas

Resultado esperado:

O Algoritmo Húngaro deve produzir custo menor ou igual ao algoritmo guloso.

Exemplo:

| Método  | Custo |
| ------- | ----- |
| Guloso  | 58    |
| Húngaro | 53    |

---

## Teste 2 – Instância Média (10x10)

Objetivo:

Avaliar desempenho e escalabilidade.

Dados:

* 10 motoristas
* 10 rotas

Métricas analisadas:

* Custo total obtido.
* Tempo de execução.
* Diferença entre solução gulosa e ótima.

---

# 9. Como Executar

## Ambiente Utilizado

O projeto foi desenvolvido e executado utilizando o Google Colab.

## Instalação das Dependências

Execute a célula abaixo:

```python
!pip install pandas numpy scipy
```

## Upload dos Arquivos CSV

Faça o upload dos seguintes arquivos para o ambiente do Colab:

### Instância Pequena

* motoristaspequeno.csv
* rotaspequeno.csv
* custospequeno.csv

### Instância Média

* motoristasmedio.csv
* rotasmedio.csv
* custosmedio.csv

Os arquivos devem ficar armazenados no diretório padrão do Colab (`/content`).

## Execução

Após realizar o upload dos arquivos, execute todas as células do notebook.

O programa executará automaticamente:

1. Teste Pequeno (4x4)
2. Teste Médio (10x10)

Para cada teste serão exibidos:

* Resultado do Algoritmo Guloso;
* Resultado do Algoritmo Húngaro;
* Custo total de cada solução;
* Economia obtida pela solução ótima;
* Tempo de execução dos algoritmos.

---

# 10. Exemplo de Saída

```text
==================================================
SOLUÇÃO GULOSA
==================================================

M4 -> R2 | 7
M1 -> R1 | 10
M3 -> R3 | 16
M2 -> R4 | 25

Custo Total: 58

==================================================
SOLUÇÃO ÓTIMA (HÚNGARO)
==================================================

M1 -> R4 | 18
M2 -> R1 | 12
M3 -> R3 | 16
M4 -> R2 | 7

Custo Total: 53

COMPARAÇÃO

Guloso: 58
Húngaro: 53
```

---

# 11. Conclusão

O problema de alocação de motoristas às rotas foi modelado como um problema clássico de atribuição.

Foram implementadas duas abordagens: uma heurística gulosa e uma solução ótima baseada no Algoritmo Húngaro.

Os resultados mostraram que a estratégia gulosa pode produzir soluções subótimas, enquanto o Algoritmo Húngaro garante a minimização do custo total das atribuições.

Dessa forma, para aplicações logísticas reais, o Algoritmo Húngaro é a alternativa mais adequada quando se busca qualidade da solução, mesmo possuindo maior custo computacional.
