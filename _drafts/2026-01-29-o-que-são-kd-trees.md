---
layout: post
categories:
  - Blog
  - Notas de Laboratório
author: pedro
tags:
  - kdtrees
title: O que são KD-trees?
math: true
mermaid: false
date: 2026-01-29T14:55:00
description: Nesse post vou descrever o que é uma k-d tree, mostrar como é a sua estrutura, operações básicas e aplicações que é utilizada.
---

## O que são árvores?
Antes de se aprofundar em *k*-d tree precisamos entender a estrutura de uma árvore, no livro Algoritmos do Thomas Cormen[^algoritmos_cormen] é nos mostrado essa estrutura de dados, ela apresenta 2 nós que apontam para o lado esquerdo e direito e temos a chave, que é o valor armazenado, ela é dinâmica e apresenta diversas operações, como `inserção`, `remoção`, `busca`, `minimo`, e `maximo`, recomendo a leitura do livro para entender bem essas operações. Ela é capaz de fazer essas operações de forma rápida. Na imagem abaixo apresenta um exemplo bem simples de árvore binária.

![Desktop view](/assets/img/uploads/DiagramasKDTREE-Árvore binária.drawio.png)
_Exemplo de Árvore Binária_

## O que são *k*-d trees?
![Desktop view](/assets/img/uploads/DiagramasKDTREE-Exemplo KD-tree.drawio.png){: .w-50 .left}

A árvore kd-tree foi inicialmente proposta no artigo *"Multidimensional binary search trees"* pelo Bentley (1975)[^kdtree_bentley], é basicamente uma árvore binária onde ao invés de ter apenas um valor como chave temos uma instancia com $d$ dimensões em um nó. Na imagem ao lado temos um exemplo de árvore kd-tree, repare que a sua estrutura é muito parecida com uma árvore binária.

![Desktop view](/assets/img/uploads/plano_cartesiano.png){: .w-50 .right}

Com os nós da árvore podemos representar eles em um plano cartesiano em 2 e 3 dimensões. Na imagem ao lado temos a representação de uma kd-tree, o interessante dessa visualização é que podemos reparar que nesse espaço podemos separar eles em quadrantes, essa representação fica mais facil de visualizar isso ao inves da árvore.


## Como construir uma *k*-d tree?
Podemos construir uma árvore *k*-d tree inserindo instância por instância, na próxima [sessão](#inserção) irei demonstrar como efetuar inserções na árvore. Para construir quando temos um conjunto de dados precisamos respeitar a escolha das dimensões, pois são elas que repartem o espaço, escolhendo a dimensão, ordenamos os valores daquela dimensão pegamos a mediana e essa mediana será o nó, depois separamos as instancias que estão antes e depois da mediana, as que estão antes repassamos via recursão para formar o nó da esquerda, e as instâncias que estão depois da mediana formaram a sub-árvore da direita assim montando a árvore balanceada.

## Como inserir uma instância? {#inserção}
Para inserir o nó estou utilizando como referência o livro *"Data structures and algorithms in C++"* escrito pelo Drozdek (2013)[^algorithms_drozdek], o algoritmo proposto é esse, conforme mostra o pseudo código abaixo.

```
insert(el)
	i = 0;
	p = root;
	prev = 0;
	while p ≠ 0
		prev = p;
		if el.keys[i] < p->el.keys[i]
			p = p->left;
		else p = p->right;
		i = (i+1) mod k;
	if root == 0
		root = new BSTNode(el);
	else if el.keys[(i-1) mod k] < p->el.keys[(i-1) mod k]
		prev->left = new BSTNode(el);
	else prev->right = new BSTNode(el);
```

O algoritmo é semelhante a inserção em uma árvore binária, a principal diferença é que como temos $d$ dimensões precisamos escolher com base no nível da árvore qual será a dimensão que será usada como separador e com base no valor dessa dimensão escolhemos o lado esquerdo ou direito igual a uma árvore binária.

## Tem como remover um nó?
// escrever isso
Sim, porém é mais complicado do que em uma árvore binária . . .

## Como buscar na *k*-d tree?
// refazer esse inicio de pauta
Com esse tipo de estrutura podemos realizar vários tipos de busca, porém nesse post irei demonstrar focar na busca do vizinho mais próximo e na busca de uma instância especifica.

### Busca de uma instância
// escrever melhor essa parte
Para realizar a busca de uma instância, conforme mostrado no livro do Drozdek (2013)[^algorithms_drozdek] basta percorrer a árvore usando o mesmo critério usado na inserção, que nesse caso é com base na profundidade da árvore para determinar a dimensão de separação que com o valor dessa dimensão podemos escolher o lado certo para fazer a busca na árvore para encontrar a instância.

### Busca do vizinho mais próximo
// deixar essa parte mais clara
Para realizar essa busca precisamos chegar até o nó folha utilizando recursão, verificamos se o nó atual é o mais próximo da instancia que estamos buscando, depois verificamos se precisamos olhar o outro ramo em relação aquele nó, se estiver próximo precisamos realizar a busca naquela sub-árvore;

### Existem outras maneiras de montar a árvore?
Existe, no MOA (*Machine Learning for Data Streams*) eles usam uma outra politica de separação, eles usam como base o *"ANN Programming Manual"* do David Mount (2006)[^ann_mount] onde nesse manual apresenta diversas formas de separar os nós de uma árvore $k$-d tree e a forma que eles usam é a *"sliding-midpoint rule"*, no MOA a árvore é montada de forma que ajuda na hora de fazer buscas do $k$ vizinhos mais proximos, para fazer isso eles usaram como base o artigo *"An Algorithm for Finding Best Matches in Logarithmic Expected Time"* pelo Bentley e Finkel (1977)[^best_matches_bentley], nessa árvore os nós não armazenam apenas 1 instância e sim um conjunto delas o que no artigo eles chamam de *"bucket"*, e a maioria das instâncias ficam nos nós, as instâncias que ficam nos nós estão proximas no espaço assim facilitando a busca quando temos muitas instâncias assim apenas percorrendo aquele nó buscando a instância.

---
## Referências
[^algoritmos_cormen]: AL, Thomas H. Cormen et. **Algoritmos**. _[S.l.]_: Elsevier, 2011.
[^kdtree_bentley]: BENTLEY, Jon Louis. Multidimensional binary search trees used for associative searching. **Communications of the ACM**, v. 18, n. 9, p. 509–517, set. 1975.
[^algorithms_drozdek]: DROZDEK, Adam. **Data structures and algorithms in C++**. Fourth edition ed. Boston, MA: Cengage Learning, 2013.
[^ann_mount]: MOUNT, David M. ANN, Version 1.1.1 Copyright, 2006 David M. Mount. [S.d.].
[^best_matches_bentley]: FRIEDMAN, Jerome H.; BENTLEY, Jon Louis; FINKEL, Raphael Ari. An Algorithm for Finding Best Matches in Logarithmic Expected Time. ACM Transactions on Mathematical Software, v. 3, n. 3, p. 209–226, set. 1977.

