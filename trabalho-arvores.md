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
  
               (30) [Preto]
              /     \
      [Vermelho] (20)   (40) [Vermelho]
            /
       [Preto] (10)

## 2. Árvore Rubro-Negra (Red-Black Tree)

#### Conceito
A Árvore Rubro-Negra é uma variação de Árvore Binária de Busca auto-balanceada que utiliza um esquema de coloração de nós (cada nó é colorido como Vermelho ou Preto) para garantir o balanceamento aproximado da estrutura. Ao contrário da AVL, ela não exige um equilíbrio rígido de altura, o que reduz o número de rotações necessárias durante modificações.

#### Regras de Coloração
Para ser classificada como Rubro-Negra, a árvore deve obedecer restritamente a cinco regras fundamentais:
* Todo nó é vermelho ou preto.
* A raiz é sempre preta.
* Todas as folhas (nós nulos/NIL) são pretas.
* Se um nó é vermelho, ambos os seus filhos devem ser pretos (não pode haver dois nós vermelhos consecutivos na vertical).
* **Caminho Preto Constante:** Para cada nó, todos os caminhos lineares dele até as folhas descendentes devem conter exatamente o mesmo número de nós pretos.

#### Vantagens
* **Inserções e Remoções Eficientes:** Como o critério de balanceamento é mais flexível que o da AVL, as modificações exigem muito menos rotações. No pior caso, a inserção requer no máximo duas rotações.
* **Desempenho Geral Consistente:** Mantém um excelente equilíbrio entre velocidade de busca, inserção e remoção, operando consistentemente em $O(\log n)$.

#### Desvantagens
* **Busca Ligeiramente Mais Lenta que a AVL:** Devido ao balanceamento aproximado, a árvore pode ficar até duas vezes mais alta que uma árvore AVL perfeitamente balanceada com o mesmo número de nós.
* **Complexidade de Implementação:** As regras de reconfiguração (recoloração e rotação baseadas nos tios do nó) geram muitos casos de teste e uma lógica de código complexa.

#### Exemplo Ilustrado
           (30) [Preto]
              /     \
    [Vermelho] (20)   (40) [Vermelho]
            /
        [Preto] (10)





## Parte 3 – Aplicação Prática

### Aplicação escolhida: Sistema de Banco de Dados (Índices)

## Sistemas de banco de dados relacionais (como PostgreSQL, MySQL e SQLite) precisam localizar registros rapidamente em tabelas que podem conter milhões de linhas. Para isso, utilizam índices, que internamente costumam ser implementados como variações de Árvores B / Árvores B+, que são uma especialização das Árvores N-árias.

### Justificativa

* Desempenho: como cada nó de uma Árvore B/B+ pode armazenar diversas chaves e ponteiros (não apenas dois), a árvore consegue manter uma altura muito menor do que uma árvore binária equivalente. Isso reduz drasticamente o número de acessos a disco necessários para localizar um registro, já que cada nível da árvore corresponde, em geral, a uma leitura de bloco de disco.

* Organização dos dados: as Árvores B+ mantêm todos os dados (ou ponteiros para os dados) ordenados nas folhas, e os nós internos servem apenas como índice de navegação. Essa organização favorece tanto buscas por chave exata quanto buscas por intervalo (BETWEEN, >, <), muito comuns em consultas SQL.

* Operações realizadas pelo sistema: bancos de dados realizam constantemente inserções, exclusões e, principalmente, buscas. As Árvores N-árias balanceadas (como a B+) garantem que essas operações permaneçam em complexidade próxima de O(log n), mesmo com tabelas muito grandes, sem o crescimento descontrolado de altura que ocorreria em uma BST simples.

## Embora árvores AVL e Rubro-Negra também sejam balanceadas e eficientes, elas são mais indicadas para estruturas em memória (como índices de coleções dentro de uma aplicação). Para bancos de dados, que trabalham com grandes volumes de dados persistidos em disco, a estrutura N-ária (Árvore B/B+) é mais adequada, pois minimiza o número de acessos a disco — o recurso mais caro nesse contexto.
