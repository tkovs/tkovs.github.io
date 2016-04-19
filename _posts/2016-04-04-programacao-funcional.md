---
layout: post
title:  "Programação Funcional"
date:   2016-03-31 22:48:45
description: Iniciação ao paradigma funcional.
categories:
- programação funcional
permalink: /blog/programacao-funcional
---

## Table of Contents

0. [Introdução](#id-introducao)
1. [Haskell](#id-haskell)
2. [Conceitos](#id-conceitos)
    1. [Funções puras](#id-funcoes-puras)
    2. [Imutabilidade](#id-imutabilidade)
    3. [Recursão](#id-recursao)
    4. [Transparência referencial](#id-transparencia-referencinal)
    5. [Funções](#id-funcoes)
    6. [Funções anônimas](#id-funcoes-anonimas)
    7. [Avaliação preguiçosa](#id-avaliacao-preguicosa)
3. [Então, o que é programação funcional?](#id-o-que-e)
4. [Uso](#id-uso)

<hr />
<div id='id-introducao' />
## Introdução

*Esse artigo é recomendado para quem já tem experiência com programação*

Um paradigma de programação é um modo de se classificar linguagens de programação, definindo os
recursos que elas disponibilizam e o seu funcionamento. Linguagens de programação podem estar
embasadas em apenas um paradigma, e podem ser multiparadigmas. Os mais comuns são o **orientado a
objetos**, o **imperativo**, e o **funcional**.

Há conceitos que devem ser compreendidos para se programar funcionalmente, e eles serão
abordados no decorrer do texto.

<div id='id-haskell' />
## Haskell

A linguagem escolhida para demonstração de exemplos foi Haskell, uma linguagem puramente funcional e
muito reconhecida academicamente. Em breve irei fazer o
port para a linguagem Ruby ou Javascript dos códigos usados aqui, assim facilita o entendimento para o maior
público. Deixarei os exemplos em Haskell no código mas ficarão em segundo plano. 
Caso queira estudar Haskell por conta própria, recomendo os seguintes materiais:

- [**Programming in Haskell** *by Graham Hutton*](http://www.cs.nott.ac.uk/~pszgmh/book.html)
- [**Wiki Haskell**](https://wiki.haskell.org/)

<div id='id-conceitos' />
## Conceitos

Para compreender esse paradigma, alguns conceitos são fundamentais.

<div id='id-funcoes-puras' />
####Funções puras

São funções sem side-effects - ou efeitos colaterais, em português. Elas não
dependem de nada além daquilo que é passado a elas como argumento e não influenciam diretamente o
resto do programa. Isso vai ao encontro da computação paralela, que é a divisão de uma tarefa entre
vários processadores, ou até mesmo máquinas. Um exemplo do porque programação funcional é bastante
relacionado à computação paralela é você ter uma lista de dados e precisar aplicar
uma função sobre todos os dados: pode-se dividir essa lista em listas menores e, tendo vários
processadores a disposição, atribuir uma lista a cada um e fazê-los trabalharem paralelamente,
otimizando a tarefa. Isso é completamente viável porque uma execução não vai influenciar em outra
paralela.

Outro conceito que contribui para paralelização é a imutabilidade.

<div id='id-imutabilidade' />
####Imutabilidade

Ao se definir o valor de um dado, ele não pode ter seu valor alterado. Ao invés
de se alterar o valor existe, cria-se uma cópia para se trabalhar, um dado novo, baseado no velho.
Ao manipular dados, você não precisa se preocupar em alterar dados, pois novos sempre são criados
quando você precisa fazer isso. Isso seria inviável na programação imperativa que se baseia em ações
e estruturas que modificam as variáveis que definem um programa.

**Exemplo de uso**:

No exemplo abaixo, imagine que nesse programa escrito em C a variável `tamanho` já tenha sido
declarada e contenha o tamanho do `vetor`, e `soma` já tenha sido declarada anteriormente também. Se o
conteúdo do `vetor` for alterado por alguma ação paralela no resto do programa antes da soma terminar,
o resultado será incorreto.

{% highlight c %}
...
...

for (int indice = 0; indice < tamanho; indice++)
    soma += vetor[indice]
}

printf ("%d", soma);

...
...
{% endhighlight %}

Outro exemplo do uso de programação paralela é na renderização de imagens. Há milhões de pixels que
devem ser renderizados. Todos eles podem ser renderizados individualmente, sem depender um do outro.
A ideia é mais ou menos essa. Logo, dividir a tarefa agiliza o processo.

<div id='id-recursao' />
####Recursão

O único meio de iteração ao se programar funcionalmente é usando recursão.

Recursão em funções, na computação, é como definimos o comportamento de uma função que invoca a si mesma.
Devido ao paralelismo, o resultado é otimizado, porém como recursão está em constante uso, as vezes
acaba pesando, mesmo com os recursos de otimização, por isso há outros meios que contribuem para 
isso, como por exemplo usar recursão de cauda.

Mas antes de entrar nesse assunto, será demonstrado aqui o uso da recursão para funções comuns.

{% highlight haskell linenos %}
-- Soma de uma lista
sum :: [Num] -> Num
sum [] = 0
sum (x:xs) = x + sum xs

-- Funcionamento
-- sum [1,2,3,4,5]
-- 1 + sum [2,3,4,5]
-- 1 + 2 + sum [3,4,5]
-- 1 + 2 + 3 + sum [4,5]
-- 1 + 2 + 3 + 4 + sum [5]
-- 1 + 2 + 3 + 4 + 5 + sum []
-- 1 + 2 + 3 + 4 + 5 + 0
-- 15

-- Fatorial de um número
fat :: Int -> Int
fat 1 = 1
fat x = x * fat (x-1)

-- Funcionamento
-- fat 5
-- 5 * fat 4
-- 5 * 4 * fat 3
-- 5 * 4 * 3 * fat 2
-- 5 * 4 * 3 * 2 * fat 1
-- 5 * 4 * 3 * 2 * 1
-- 120
{% endhighlight %}

Recursão de cauda, ou **tail call** em inglês, é como uma subcategoria da recursão, e é usada pois
na recursão comum o número de chamadas à função aumenta, consequentemente estourando a pilha.
Explicando isso de uma maneira simples: uma função com recursão de cauda é uma função onde a chamada
a si mesma ocorre apenas no final da função, não precisando manter na pilha de chamada os valores de
retorno. É verdade que funções recursivas podem ser mais custosas do que iterações, mas normalmente os
compiladores de linguagens funcionais transformam chamadas a funções com recursão de cauda em loops.

> O código abaixo mostra a escrita e o funcionamento da função fibonacci sem usar tail call.

{% highlight haskell linenos %}
-- Fibonacci sem tail call
fib :: Int -> Int
fib 0 = 0
fib 1 = 1
fib x = fib (x-1) + fib (x-2)

{-
-> Execução do código acima para x = 6
-> fib 6
-> (fib 5) + (fib 4)
-> ((fib 4) + (fib 3)) + ((fib 3) + (fib 2))
-> (((fib 3) + (fib 2)) + ((fib 2) + (fib 1))) + (((fib 2) + (fib 1)) + ((fib 1) + (fib 0)))
-> ((((fib 2) + (fib 1)) + ((fib 1) + (fib 0))) + (((fib 1) + (fib 0)) + 1)) + ((((fib 1) + (fib 0)) + 1) + (1 + 0))
-> (((((fib 1) + (fib 0)) + 1) + (1 + 0)) + ((1 + 0) + 1)) + (((1 + 0) + 1) + (1 + 0))
-> ((((1 + 0) + 1) + 1) + (1 + 1)) + ((1 + 1) + 1)
-> (((1 + 1) + 1) + 2) + (2 + 1)
-> ((2 + 1) + 2) + 3
-> (3 + 2) + 3
-> 5 + 3
-> 8
-}
{% endhighlight %}

> O código abaixo mostra a escrita e o funcionamento da função fibonacci usando tail call e uma função
auxiliar.

{% highlight haskell linenos %}
-- Fibonacci com tail call
fib :: Int -> Int
fib x = fib_aux (x, 0, 1)

fib_aux :: (Int, Int, Int) -> Int
fib_aux (0, current, _)    = current
fib_aux (x, current, next) = fib_aux(x-1, next, current + next)

{-
-> Funcionamento
-> fib 6
-> fib_aux(6, 0, 1)
-> fib_aux(5, 1, 1)
-> fib_aux(4, 1, 2)
-> fib_aux(3, 2, 3)
-> fib_aux(2, 3, 5)
-> fib_aux(1, 5, 8)
-> fib_aux(0, 8, 13)
-> 8
-}
{% endhighlight %}

<div id='id-transparencia-referencial' />
####Transparência referencial

Não importa quantas vezes uma função seja chamada, se o parâmetro for
o mesmo o retorno também será, e a essa propriedade se dá o nome de transparência referencial.
Dessa forma, facilmente se prova que uma função está funcionando como
deveria, e consequentemente, constrói-se funções mais complexas e seguras. Isso parece óbvio, mas em
outros paradigmas, é comum a mesma expressão poder resultar em diferentes valores em diferentes
momentos dependendo do estado de execução do programa. Como o exemplo da [wiki do
Haskell](https://wiki.haskell.org) mostra, se `y = f x` e `g = h y y`, poderia substituir y por f x
de modo que g fosse descrito por `g = h (f x) (f x)` e se obter o mesmo resultado.

<div id='id-funcoes' />
####Funções

Uma das características desse paradigma é que funções são cidadãs de primeira classe.
Isso implica no fato de que funções não são usadas apenas para serem declaradas e chamadas. Elas
agora suportam muitas operações comuns a outros objetos, como serem passadas para funções como
parâmetros, serem retornadas por funções, e serem atribuídas a uma variável.
Daí, temos 2 conceitos novos: **high order functions** e **currying**. Esses dois termos
podem ser confundidos mas a verdade é que estão intrisecamente ligados: uma high order function é
uma função que recebe uma função como parâmetro, enquanto curried functions são funções que retornam
funções como parâmetros.
Através desse recurso, qualquer função com múltiplos parâmetros pode ser escrita com apenas um. Para
exemplo será usado o código abaixo:

{% highlight haskell linenos %}
add :: Int - (Int -> Int)
add x y = x + y
{% endhighlight %}

Observando a declaração da função, ela recebe 1 inteiro e retorna uma função que recebe um inteiro e
retorna outro inteiro. No corpo da função diz-se que recebe 2 parâmetros e retorna a soma deles.
Isso ocorre porque a função acima recebe um inteiro e retorna uma função, que recebe um inteiro y e
retorna o resultado de x + y.

Com esses recursos é possível escrever funções definitivamente úteis que são muito comuns em linguagens
funcionais e que costumam receber um port para a biblioteca padrão de linguagens não funcionais. Entre elas, há a
função map é uma função para manipulação de listas. Ela recebe uma função e uma lista genérica,
aplica a função sobre cada elemento da lista retornando uma nova lista com as modificações.

{% highlight haskell linenos %}
-- Usando recursão
map :: (a -> b) -> [a] -> [b]
map f []     = []
map f (x:xs) = f x : map f xs

-- Usando list comprehension
map :: (a -> b) -> [a] -> [b]
map f x = [f x | x <- xs]
{% endhighlight %}

<div id='id-funcoes-anonimas' />
####Funções anônimas

Conforme já vimos, funções são cidadãs de primeira classe. Valores de vários tipos podem ser
escritos de forma literal, sem obrigação de ser dar um nome, por exemplo ```10``` ```"Vitor"```
```[1,2,3]```, e agora funções também, que no caso de haskell ficaria assim: ```\x -> 2 * x``` - uma
função que recebe um valor e retorna seu dobro. Funções anônimas apenas são funções sem nome, também
conhecidas como **lambda functions**.

São usadas para conter uma funcionalidade que não precisa de um nome ou que tem um uso muito
curto e rápido, sendo um objeto temporário. Esse recurso evita a escrita de funções de uma linha só
que seriam usadas apenas uma vez, por exemplo:

{% highlight haskell linenos %}
something :: Num x => x -> x
something x = (x *3 + 2) * x

map something [1,2,3]
-- Retorno: [5,16,33]
{% endhighlight %}

ficaria assim:

{% highlight haskell linenos %}
map (\x -> (x * 3 + 2) * x) [1,2,3]
-- Retorno: [5,16,33]
{% endhighlight %}

<div id='id-avaliacao-preguicosa' />
####Avaliação preguiçosa

Lazy Evaluation. Em breve.

<div id='id-o-que-e' />
##Então, o que é programação funcional?

A programação funcional é um paradigma de programação que 
se baseia em funções e é muito semelhante à matemática. Até mesmo um
programa é uma função. Não há um identificador para o ponto de partida, como na linguagem C
onde se começa pela função main(). O retorno de uma função se baseia inteiramente no que lhe é
passado e o momento em que a mesma função é chamada não é importante. O software desenvolvido
segundo esse paradigma funciona através da interação entre essas funções que, devido ao paradigma,
focam no que se deve fazer e não como fazer para se chegar ao resultado. Ou seja, o objetivo é
definir uma função que, trabalhando em cima de outras funções, vistas como expressões, gere um 
valor de retorno.

Você pode escrever código funcional em qualquer linguagem que dê suporte à funções de primeira
classe, como Ruby e Javascript, mas há linguagens focadas nisso, como Haskell e Elixir.

Há um nível de abstração muito alto, principalmente quando funções são utilizadas, e devido
à modularização, o código cresce rápido e de forma segura, de forma que a escrita de grandes funções
se dá através da composição de funções menores, o que evita a reescrita.
Os programas podem ser avaliados em diferentes ordens pois não há dependência nas operações de
atribuição, o que também garante aos programas serem mais simples de se provar e analisar 
matematicamente do que programas procedurais.

Como as funções são mais fáceis de serem avaliadas isoladamente, é mais fácil encontrar erros e
bugs e, aliás, contribuir com projetos open-source, mesmo sem um grande envolvimento.

Códigos funcionais são, geralmente, mais curtos e mais fáceis de entender do que sua 
implementação no
paradigma imperativo. É muito mais fácil de se trabalhar com paralelização de tarefas devido à
imutabilidade e às funções puras. O resultado final é um código bastante modularizado e conciso,
e sua manutenção é muito mais fácil do que em um código que permite side-effects e trabalha com
dados mutáveis, assim como a otimização do código e trabalho e equipe se tornam mais simples.

<div id='id-uso' />
##Uso

O sistema operacional **[Linspire](http://homepages.inf.ed.ac.uk/wadler/realworld/linspire.html)**, baseado no Debian, tem uma equipe que trabalha usando programação
funcional em algumas tarefas como a **detecção de hardware**, **criação de CDs de instalação** e
**aplicações web internas**. Inicialmente usaram O'Caml, depois decidiram por usar Haskell também.

O **[xmonad](http://xmonad.org/)**, um gerenciador de janelas "tile-based" dinâmico para o X foi completamente desenvolvido
usando Haskell.

O **[Darcs](http://darcs.net/)**, um software para controle de versão distribuida, assim como o git e o svn, 
com muitos recursos, que inicialmente foi escrito em C++, mas logo depois foi portado pra Haskell.

**[Pandoc](http://pandoc.org)**, uma ferramenta para conversão de um arquivo num formato de marcação para outro. Suporta
HTML, LaTeX, OPML, Org-mode, DocBook, Wiki markup, inDesign ICML, ebooks, e vários formatos TeX.
Desenvolvido em Haskell.

O Facebook tem a implementação de um
**[anti-spam](http://www.wired.com/2015/09/facebooks-new-anti-spam-system-hints-future-coding/)** feita em Haskel.

**[Yesod](http://www.yesodweb.com/)**, uma framework para aplicações web de alta performance e alto
nível, com performance próxima à do C com acesso direto à memória. Desenvolvida em Haskell.

A linguagem de programação **[Hack](http://hacklang.org/)**, desenvolvida pelo Facebook, é um
dialeto do PHP. Sua implementação é open-source, e seu compilador foi escrito em O'Caml.

Há o [**Zero Install (0Install)**](0install.net) é um gerenciador de pacotes multiplataforma,
desenvolvido em O'Caml. Se você tem um web-site, você pode distribuir seu software criando um pacote
que funciona em qualquer lugar, com manipulamento de dependências e atualizações automáticas.

**[FramaC](http://frama-c.com/)** é uma framework para analise modular de programas escritos em C.
Um analisador estático que ispenciona programas em executalos. Implementada em O'Caml.

**[Haxe](http://haxe.org/)** é uma linguagem de programação de alto nível e multiplataforma com um
compilador que produz aplicações e código fonte para diferentes plataformas através de um código
base. Seu commpilador é escrito em O'Caml.

##Referências

- [Departamento de Informática (DIN) da Universidade Estadual de Maringá (UEM)](http://din.uem.br/ia/ferramentas/lisp/lisp3.htm)
- [**Programming in Haskell** *by Graham Hutton*](http://www.cs.nott.ac.uk/~pszgmh/book.html)
- [Wiki Haskell](https://wiki.haskell.org/Functional_programming)
- [Wikipedia](https://en.wikipedia.org/wiki/Functional_programming)
- [Smashing Magazine](https://www.smashingmagazine.com/2014/07/dont-be-scared-of-functional-programming/)
- [StackOverflow](http://pt.stackoverflow.com/questions/13372/programa%C3%A7%C3%A3o-funcional-e-programa%C3%A7%C3%A3o-orientada-a-objetos-o-que-s%C3%A3o-e-quais-suas)
- [Caelum](http://blog.caelum.com.br/comecando-com-o-calculo-lambda-e-a-programacao-funcional-de-verdade/)
- [Instituto de Computação UFF](http://www2.ic.uff.br/~bazilio/cursos/lp/material/ProgFuncional.pdf)
