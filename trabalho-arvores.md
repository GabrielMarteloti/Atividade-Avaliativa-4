# Atividade-Avaliativa-4
Atividade Avaliativa de Estrutura de Dados

## Parte 1 - Tipos de árvores
### 1. Árvore AVL

### Conceito
As árvores AVL, que receberam esse nome em homenagem aos seus inventores, Adelson-Velsky e Landis, resolvem esse problema de se tornar desbalanceadas, levando a uma queda de desempenho em alguns cenários, mantendo o equilíbrio independentemente da ordem em que os dados são inseridos.

### Características
**Fator de Balanceamento (FB):** Cada nó calcula a diferença de altura entre o seu lado esquerdo e o seu lado direito.
* **Regra Rígida:** Para estar balanceada, o FB de cada nó só pode ser -1, 0 ou 1.
* **Auto-correção:** Se um nó passar disso, a árvore faz uma operação chamada "rotação" para voltar a alinhar-se.

### Vantagens
* **Busca Extremamente Eficiente:** Por manter-se sempre perfeitamente distribuída e balanceada, a localização de qualquer informação dentro dela é feita no menor tempo possível.
* **Previsibilidade e Consistência:** A altura da árvore é rigidamente controlada, o que garante que o tempo de pesquisa permaneça estável e não sofra variações drásticas.

### Desvantagens
* **Custo Elevado na Inserção e Remoção:** O acréscimo ou a retirada de itens demanda um esforço maior do processador, pois exige reavaliações frequentes dos fatores de balanceamento e a execução de rotações (os "giros") para reequilibrar a estrutura.

  #### Exemplo Ilustrado
```text
