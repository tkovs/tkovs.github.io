---
layout: post
title:  "Programação Funcional"
date:   2016-03-31 22:48:45
description: Iniciação ao paradigma funcional.
categories:
- programação funcional
permalink: /blog/programacao-funcional
---

Primeiramente, devo lembra-lo que um paradigma de programaçao é o modo que construímos um programa,
se tratando da sua estrutura, da forma como se escreve e como seu fluxo de funcionamento é descrito.
É um conceito teórico que embasa, posteriormente, o funcionamento de uma linguagem de programação.
O paradigma tratado nesse texto é baseado no cálculo de funções, diferente do paradigma imperativo na troca de 
estados durante a execução de um programa, e do paradigma Orientado a Objetos que se baseia na 
troca de mensagens entre objetos - dei esses dois exemplos pois são os paradigmas mais comuns.
O paradigma funcional é, naturalmente, um paradigma declarativo, pois os programas se focam mais no
que deve ser feito do que nos passos para o fazer.

### Conceitos

Para compreender esse paradigma, alguns conceitos são fundamentais.

**Funções puras**: São funções sem side-effects - ou efeitos colaterais, em português. Elas não
dependem de nada além daquilo que é passado a elas como argumento e não influenciam diretamente o
resto do programa. Isso vai de encontro à computação paralela, que é a divisão de uma tarefa entre
vários processadores, ou até mesmo máquinas. Um exemplo é você ter uma lista de dados e precisar aplicar
uma função sobre todos os dados: pode-se dividir essa lista em listas menores e, tendo vários
processadores a disposição, atribuir uma lista a cada um e fazê-los trabalharem paralelamente,
otimizando a tarefa.
