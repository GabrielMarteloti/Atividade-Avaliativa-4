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


### 3. Árvore N-ária (Árvore Geral)

#### Conceito
Uma Árvore N-ária é uma estrutura de dados hierárquica na qual cada nó pode possuir, no máximo, *N* filhos. Ela rompe a limitação tradicional das árvores binárias (que restringem o grau de saída a no máximo 2), permitindo mapear estruturas ramificadas de forma mais natural e flexível.

#### Diferenças em relação às árvores binárias
* **Grau de Saída:** Em uma árvore binária, o limite de filhos por nó é estritamente 2. Em uma árvore N-ária, esse limite é definido pelo parâmetro fixo ou dinâmico *N* (por exemplo, uma árvore 4-ária pode ter até 4 filhos por nó).
* **Estrutura do Nó:** O nó de uma árvore binária possui apenas dois ponteiros (`esq` e `dir`). Um nó de árvore N-ária armazena uma coleção, lista encadeada ou array de ponteiros para referenciar seus múltiplos filhos.

#### Vantagens
* **Modelagem Direta de Estruturas Reais:** Perfeita para representar conceitos de agrupamento multifacetado, como sistemas de diretórios e categorizações taxonômicas.
* **Redução de Altura:** Ao expandir a quantidade de filhos por nível, a altura total da árvore diminui drasticamente, diminuindo o número de saltos em disco ou memória para acessar dados folha.

#### Desvantagens
* **Desperdício Potencial de Memória:** Se os nós forem alocados com arrays estáticos de tamanho *N* e a maioria tiver poucos filhos, haverá um grande volume de ponteiros nulos (`null`) desperdiçados.
* **Complexidade de Percurso:** Algoritmos clássicos de percurso em ordem tornam-se ambíguos ou consideravelmente complexos se comparados à simplicidade do pré/pós/em-ordem binários.

#### Exemplo Ilustrado (Árvore 3-ária / Ternária)

                      [ Raiz ]
                     /   |    \
                  [A]   [B]   [C]
                 /   \         |
               [D]   [E]      [F]

#### Aplicações Práticas
As árvores N-árias (e suas variantes especializadas como Árvores B, B+ e Tries) são largamente aplicadas em:

* **Sistemas de Arquivos (Filesystems):** Organização de pastas e subpastas em sistemas operacionais (NTFS, ext4).
* **Motores de Busca e Autocompletar:** Árvores Trie (um tipo de árvore N-ária de prefixos) para busca textual e indexação de dicionários.
* **Documentos Estruturados:** Modelagem do DOM (Document Object Model) em páginas HTML e na validação sintática de arquivos XML/JSON.

### 1. Rotação Simples à Direita (Right Rotation - LL)

Objetivo
Reduzir a altura da subárvore esquerda elevando o filho esquerdo à posição de novo nó pai, restabelecendo o equilíbrio após uma inserção ou remoção que deixou o nó original pendendo excessivamente para a esquerda.

Situação em que é utilizada
É utilizada quando um nó fica desbalanceado com $FB = +2$ e o seu filho esquerdo possui $FB = +1$ ou $0$. Isso caracteriza um desalinhamento do tipo "Esquerda-Esquerda" (Left-Left).

Exemplo Antes e Depois

    Antes da Rotação (Nó A com FB = +2)            Depois da Rotação
                 (A)                                      (B)
                 /                                       /   \
               (B)                                     (C)   (A)
               /
             (C)

### 2. Rotação Simples à Esquerda (Left Rotation - RR)

Objetivo
Reduzir a altura da subárvore direita elevando o filho direito à posição de novo nó pai, corrigindo o desbalanceamento vertical do lado oposto.

Situação em que é utilizadaDisparada quando um nó apresenta fator de balanceamento $FB = -2$ e o seu filho direito apresenta $FB = -1$ ou $0$. Indica um desalinhamento do tipo "Direita-Direita" (Right-Right).

Exemplo Antes e Depois

    Antes da Rotação (Nó A com FB = -2)            Depois da Rotação
                 (A)                                      (B)
                   \                                     /   \
                   (B)                                 (A)   (C)
                     \
                     (C)


### 3. Rotações Duplas

### Rotação Dupla Esquerda-Direita (Left-Right - LR)
*Cenário: Ocorre quando um nó está desbalanceado com $FB = +2$, mas o seu filho esquerdo está inclinado para a direita ($FB = -1$).
*Como funciona: Primeiro, executa-se uma Rotação Simples à Esquerda no filho esquerdo (transformando o cenário em "Esquerda-Esquerda"). Logo em seguida, executa-se uma Rotação Simples à Direita no nó pai original desbalanceado.

### Rotação Dupla Direita-Esquerda (Right-Left - RL)
*Cenário: Ocorre quando um nó está desbalanceado com $FB = -2$, mas o seu filho direito está inclinado para a esquerda ($FB = +1$).
*Como funciona: Primeiramente, realiza-se uma Rotação Simples à Direita sobre o filho direito (alinhando o ramo como "Direita-Direita"). Na sequência, aplica-se uma Rotação Simples à Esquerda no nó pai desbalanceado para finalizar.

Exemplos Ilustrados (Caso LR)

    [Original: LR]         [1ª Rotação: RR no Filho]     [2ª Rotação: LL no Pai]
         (30)                        (30)                         (25)
         /                           /                            /  \
       (20)      --------->        (25)       --------->        (20) (30)
         \                         /
         (25)                    (20)

### 4. Inversão / Espelhamento (Invert / Mirror)

###Conceito
A operação de inversão consiste em transformar uma árvore binária em sua imagem espelhada. Estruturalmente, o algoritmo percorre recursivamente todos os nós da árvore e troca a referência do filho esquerdo com o filho direito.

Aplicação
* Sistemas de Computação Gráfica: Inversão bidimensional de coordenadas ou matrizes hierárquicas de renderização.
* Questões de Lógica Algorítmica: Muito utilizada em testes e provas conceituais de manipulação profunda de ponteiros e recursividade.

Exemplo Antes e Depois 
            
            Árvore Original                              Árvore Espelhada
                 (10)                                         (10)
                 /  \                                         /  \
               (5)  (15)        -- Inversão -->            (15)  (5)
               /                                               \
             (2)                                               (2)

## Parte 3 – Aplicação Prática

### Aplicação escolhida: Sistema de Banco de Dados (Índices)
Sistemas de banco de dados relacionais (como PostgreSQL, MySQL e SQLite) precisam localizar registros rapidamente em tabelas que podem conter milhões de linhas. Para isso, utilizam índices, que internamente costumam ser implementados como variações de Árvores B / Árvores B+, que são uma especialização das Árvores N-árias.

## Justificativa

* Desempenho: como cada nó de uma Árvore B/B+ pode armazenar diversas chaves e ponteiros (não apenas dois), a árvore consegue manter uma altura muito menor do que uma árvore binária equivalente. Isso reduz drasticamente o número de acessos a disco necessários para localizar um registro, já que cada nível da árvore corresponde, em geral, a uma leitura de bloco de disco.

* Organização dos dados: as Árvores B+ mantêm todos os dados (ou ponteiros para os dados) ordenados nas folhas, e os nós internos servem apenas como índice de navegação. Essa organização favorece tanto buscas por chave exata quanto buscas por intervalo (BETWEEN, >, <), muito comuns em consultas SQL.

* Operações realizadas pelo sistema: bancos de dados realizam constantemente inserções, exclusões e, principalmente, buscas. As Árvores N-árias balanceadas (como a B+) garantem que essas operações permaneçam em complexidade próxima de O(log n), mesmo com tabelas muito grandes, sem o crescimento descontrolado de altura que ocorreria em uma BST simples.

Embora árvores AVL e Rubro-Negra também sejam balanceadas e eficientes, elas são mais indicadas para estruturas em memória (como índices de coleções dentro de uma aplicação). Para bancos de dados, que trabalham com grandes volumes de dados persistidos em disco, a estrutura N-ária (Árvore B/B+) é mais adequada, pois minimiza o número de acessos a disco — o recurso mais caro nesse contexto.
