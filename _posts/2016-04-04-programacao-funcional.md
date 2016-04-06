---
layout: post
title:  "Programação Funcional"
date:   2016-03-31 22:48:45
description: Iniciação ao paradigma funcional.
categories:
- programação funcional
permalink: /blog/programacao-funcional
---

*Esse artigo é recomendado para quem já tem experiência com programação*

Primeiramente, devo lembra-lo que um paradigma de programaçao é o modo que construímos um programa,
se tratando da sua estrutura, da forma como se escreve e como seu fluxo de funcionamento é descrito.
É um conceito teórico que embasa, posteriormente, o funcionamento de uma linguagem de programação.
O paradigma tratado nesse texto é baseado no cálculo de funções, diferente do paradigma imperativo na troca de 
estados durante a execução de um programa, e do paradigma Orientado a Objetos que se baseia na 
troca de mensagens entre objetos - dei esses dois exemplos pois são os paradigmas mais comuns.
O paradigma funcional é, naturalmente, um paradigma declarativo, pois os programas se focam mais no
que deve ser feito do que nos passos para o fazer.

### Haskell

A linguagem escolhida para demonstração de exemplos foi Haskell, uma linguagem puramente funcional e
muito reconhecida academicamente. Em breve escrevo uma postagem sobre ela apenas com as informações
necessárias para o entendimento dessa introdução à programação funcional. Caso queira estudar
Haskell por conta própria, recomendo os seguintes materiais:

- [**Programming in Haskell** *by Graham Hutton*](http://www.cs.nott.ac.uk/~pszgmh/book.html)
- [**Wiki Haskell**](https://wiki.haskell.org/)

### Conceitos

Para compreender esse paradigma, alguns conceitos são fundamentais.

**Funções puras**: São funções sem side-effects - ou efeitos colaterais, em português. Elas não
dependem de nada além daquilo que é passado a elas como argumento e não influenciam diretamente o
resto do programa. Isso vai ao encontro da computação paralela, que é a divisão de uma tarefa entre
vários processadores, ou até mesmo máquinas. Um exemplo é você ter uma lista de dados e precisar aplicar
uma função sobre todos os dados: pode-se dividir essa lista em listas menores e, tendo vários
processadores a disposição, atribuir uma lista a cada um e fazê-los trabalharem paralelamente,
otimizando a tarefa. Outro conceito que contribui para paralelização é a imutabilidade.

**Imutabilidade**: Ao se definir o valor de um dado, ele não pode ter seu valor alterado. Ao invés
de se alterar o valor existe, cria-se uma cópia para se trabalhar, um dado novo, baseado no velho.
Ao manipular dados, você não precisa se preocupar em alterar dados, pois novos sempre são criados
quando você precisa fazer isso.

No exemplo abaixo, imagine que nesse programa escrito em C a variável `tamanho` já tenha sido
declarada e contenha o tamanho do `vetor`, e `soma` já tenha sido declarada anteriormente também. Se o
conteúdo de `vetor[indice]` for alterado antes da soma terminar, o resultado será incorreto.

{% highlight c %}
soma = 0;

for (int indice = 0; indice < tamanho; indice++)
    soma += vetor[indice]
}

Outro exemplo do uso de programação paralela é na renderização de imagens. Há milhões de pixels que
devem ser renderizados. Todos eles podem ser renderizados individualmente, sem depender um do outro.
A ideia é mais ou menos essa. Logo, dividir a tarefa agiliza demais o processo.

printf ("%d", soma);
{% endhighlight %}

**Recursão**: O único meio de iteração ao se programar de um jeito puramente funcional é usando recursão.
Recursão, na computação, é como definimos o comportamento de uma função que invoca a si mesma.
Devido ao paralelismo, o resultado é otimizado, porém como recursão está em constante uso, as vezes
acaba pesando, mesmo com os recursos de otimização, por isso há outros meios que contribuem para 
isso, como por exemplo usar recursão de cauda.
Mas antes de entrar nesse assunto será demonstrado aqui o uso da recursão para funções comuns.

{% highlight haskell %}
-- Soma de uma lista
sum :: [Num] -> Num
sum [] = 0
sum (x:xs) = x + sum xs

-- sum [1,2,3,4,5]
-- 15

-- Fatorial de um número
fat :: Int -> Int
fat 1 = 1
fat x = x * fat (x-1)

-- fat 5 
-- 120
{% endhighlight %}

Recursão de cauda, ou **tail call** em inglês, é como uma subcategoria da recursão, e é usada pois
na recursão comum o número de chamadas à função aumenta, dessa forma a pilha acaba estourando.
Explicando isso de uma maneira simples, uma função com recursão de cauda é uma função onde a chamada
a si mesma ocorre apenas no final da função, pois a cauda de uma função é sua última ação, seu
último cálculo, dessa forma não é preciso manter na pilha de chamada os valores de retorno. É
verdade que funções recursivas podem ser mais custosas do que iterações, mas normalmente os
compiladores de linguagens funcionais transformam chamadas a funções com recursão em cauda em laços,
o que dá a eficiência de um loop, o código provavelmente ficará mais legível, e as chamadas à função
podem ser divididas entre processadores/máquinas.

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

{% highlight haskell %}
-- Fibonacci com tail call
fib :: Int -> Int
fib x = fib_aux (x, 0, 1)

fib_aux :: (Int, Int, Int) -> Int
fib_aux (0, current, _)    = current
fib_aux (x, current, next) = fib_aux(x-1, next, current + next)

{-
-> Execução do código acima para x = 6
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

**Transparência referencial**: Não importa quantas vezes uma função seja chamada, se o parâmetro for
o mesmo o retorno também será, e a essa propriedade se dá o nome de transparência referencial.
Dessa forma, facilmente se prova que uma função está funcionando como
deveria, e consequentemente, constroe-se funções mais complexas e seguras. Isso parece óbvio, mas em
outros paradigmas, é comum a mesma expressão poder resultar em diferentes valores em diferentes
momentos dependendo do estado de execução do programa. Como a [wiki do
Haskell](https://wiki.haskell.org) mostra, se `y = f x` e `g = h y y`, poderia substituir y por f x
de modo que g fosse descrito por `g = h (f x) (f x)` e se obter o mesmo resultado.
