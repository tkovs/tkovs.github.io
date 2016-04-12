---
layout: post
title:  "Sliding Puzzle em Ruby"
date:   2016-04-08 00:29:30
description: Desenvolvimento de um Sliding Puzzle em Ruby.
categories:
- ruby
permalink: /blog/ruby-sliding-puzzle
---

Nesse post será demonstrado o desenvolvimento de um sliding puzzle, usando a linguagem de
programação Ruby, que será executado em CLI - Command Line Interface. Para uso didático, é um bom
meio de se começar os estudos.

O resultado final será algo [assim](https://github.com/tkovs/sliding-puzzle/tree/master/ruby).

##Ruby

<img style="float: left; padding-right: 50px;" src="https://s-media-cache-ak0.pinimg.com/originals/e3/28/8b/e3288bdbdf2972ba29a5e6f86ab4755c.jpg">

Por ser uma linguagem muito simples e comum, decidi optar por Ruby. Ela tem uma implementação muito
boa do paradigma orientado a objetos e tem características funcionais, como por exemplo as funções
serem cidadãos de primeira classe. Usar o estilo funcional em Ruby não é sempre recomendado
pois não é o foco da linguagem - que é a orientação a objetos -, e as vezes prejudica a performance
do programa. Um dos motivos é que, embora você possa programar funcionalmente em Ruby usando funções
recursivas sem side-effects e com dados imutáveis, CRuby não dá um bom suporte a threads devido ao
GIL - *Global Interpreter Lock*.

##Sliding Puzzle

<center><img src="http://www.appsgalery.com/pictures/000/122/-uzzle-15--liding--uzzle-122141.png"></center>

Sliding Puzzle é um jogo muito simples. Uma versão comum é um tabuleiro quatro por quatro (16
células) onde cada célula tem um número de 1 a 15. Uma das células não contém nada para que seja
possível a locomoção das outras sobre essa através da troca na vertical ou na horizontal com
células. O tabuleiro começa com as células desordenadas e o objetivo é ordena-las de modo que a
última célula seja o espaço vazio.

##Funcionamento

O funcionamento será o seguinte:

1. Cria-se uma classe que irá gerenciar o tabuleiro NxN onde N é definido pelo usuário
2. O tabuleiro é preenchido de 1 a 15 e logo depois desordenado
3. Mostra-se o tabuleiro ao usuário
4. O usuário insere um comando - *mover pra direita, esquerda, etc* - através das setas
5. Altera-se o tabuleiro de acordo com o comando passado
6. Verifica-se o status do tabuleiro
    1. Se estiver desordenado volta-se ao passo 3
    2. Se estiver ordenado se segue
7. Exibe quanto tempo e quantos movimentos foram necessários para vencer

##Início

Agora vamos dar início ao desenvolvimento do jogo

####Preparação



####Construtor
