---
layout: post
title:  "Trabalhando com listas"
date:   2016-03-31 22:43:16
description: Uso do tipo lista na programação do dia a dia.
categories:
- programacao
permalink: /blog/trabalhando-com-listas
---

### Introdução

Muita gente não sabe, mas existem utilidades e meios de se trabalhar com listas que facilitam muito
a vida do programador, agilizando o trabalho e facilitando a leitura do código final. Isso se dá por
meio de conceitos matemáticos que deram origem à programação funcional.

### Programação funcional

[*Você pode pular essa parte*](#por-que-listas)

A programação funcional é um conceito teórico de programação que funciona essencialmente com
funções, não procedimentos nem objetos. Dentro de um código funcional qualquer função pode ser
chamada a qualquer momento, elas não dependem de nada além do que é passado a elas, não há
**side-effects** - devido às **funções puras** - nem mutabilidade. Vale lembrar que não há loops -
estrutura de repetição - mas sim recursão.
O código é muito mais fácil de ser mantido pois você focar a melhora de cada função; como as funções
têm objetivos curtos e específicos, o código fica bastante modularizado e a escrita de funções
grandes é feita através da composição de funções menores, o que evita a reescrita; localizar bugs e
ações indesejadas é mais fácil; testar as funções independentemente das outras, não precisa se
preocupar se vai modificar algum valor fora da função ou não pois não há side-effects, ou seja, suas
ações sobre uma função não refletem no resto do programa, sem efeitos colaterais - isso se dá também
graças a **imutabilidade**, que significa que um dado não pode ser alterado depois de criado. 

Um exemplo simples de uma função sem side-effects é uma função que retorna a soma dos elementos de
uma lista. O código está em Haskell.

{% highlight haskell %}
{- Linha 1: A função é declarada com o nome sum, recebendo uma lista de inteiros [Int] e retornando 1 inteiro Int.
 - Linha 2: Quando a função receber uma lista vazia o retorno é zero.
 - Linha 3: Onde a lista tem conteúdo, está escrito que o retorno é a soma do primeiro elemento com o retorno da função recebendo o resto da lista - a cauda.
-}
sum :: [Int] -> Int
sum [] = 0
sum (x:xs) = x + sum xs -- (x:xs) representa uma lista onde x é o primeiro elemento e xs o resto da lista
{% endhighlight %}

Não importa quantas vezes a função acima seja chamada, passando-se o mesmo valor pra função o
retorno sempre será o mesmo e não haverá alterações em outra parte do programa executando ela.

Outra vantagem desses aspectos é o **paralelismo**. Quando há vários processadores independentes,
podemos dividir um grande problema em vários problemas menores para que os processadores trabalhem
paralelamente em conjunto, dessa forma fazendo com que o programa se divida em vários fluxos de
execução. Isso é mais difícil de se fazer quando as funções têm efeitos colaterais - comum em
outros paradigmas de programação - pois as ações de um processador afetam as ações de outro
trabalhando em conjunto, o que resulta em imprevistos.

Não vou me aprofundar em programação funcional nesse artigo, melhor separar para outro. Agora vamos
dar continuidade ao assunto?

### Por que listas?

Lista é um tipo de dado abstrato muito usado na matemática e definitivamente útil na programação -
principalmente na programação funcional.

Geralmente uma lista é um conjunto de objetos do mesmo tipo, podendo conter elementos ou estar vazia.

**Concluíndo...**
