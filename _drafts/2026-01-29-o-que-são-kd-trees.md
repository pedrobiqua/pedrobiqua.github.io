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
description: Nesse post vou descrever o que é uma *k*-d tree, mostrar como é a sua estrutura, operações básicas e aplicações que é utilizada.
---

## O que são árvores?
Antes de se aprofundar em *k*-d tree precisamos entender a estrutura de uma árvore, no livro Algoritmos do Thomas Cormen[^algoritmos_cormen] é nos mostrado essa estrutura de dados, ela apresenta 2 nós que apontam para o lado esquerdo e direito e temos a chave, que é o valor armazenado, ela é dinâmica e apresenta diversas operações, como `inserção`, `remoção`, `busca`, `minimo`, e `maximo`, recomendo a leitura do livro para entender bem essas operações. Ela é capaz de fazer essas operações de forma rápida. Na imagem abaixo apresenta um exemplo bem simples de árvore binária.

// Adicionar foto do exemplo
## O que são *k*-d trees?
A árvore kd-tree foi inicialmente proposta no artigo *"Multidimensional binary search trees"* pelo Bentley (1975)[^kdtree_bentley], é basicamente uma árvore binária onde ao invés de ter apenas um valor como chave temos uma instancia com $d$ dimensões   em um nó, esses nós podemos representar eles como uma árvore binária e para duas e três dimensões podemos colocá-las em um plano cartesiano. Nas imagens temos um plano cartesiano e a representação como uma árvore binária.

// adicionar árvore
// adicionar plano cartesiano
## Como construir uma *k*-d tree?

## Como inserir uma instância?

## Tem como remover um nó?

## Como buscar na *k*-d tree?

### Busca do vizinho mais próximo

---
### Referências

[^algoritmos_cormen]: AL, Thomas H. Cormen et. **Algoritmos**. _[S.l.]_: Elsevier, 2011.
[^kdtree_bentley]: BENTLEY, Jon Louis. Multidimensional binary search trees used for associative searching. **Communications of the ACM**, v. 18, n. 9, p. 509–517, set. 1975.
