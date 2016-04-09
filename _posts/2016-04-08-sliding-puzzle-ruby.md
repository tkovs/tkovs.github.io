---
layout: post
title:  "Sliding Puzzle em Ruby"
date:   2016-04-08 00:29:30
description: Desenvolvimento de um Sliding Puzzle em Ruby.
categories:
- ruby
permalink: /blog/ruby-sliding-puzzle
---

Nesse post será demonstrando o desenvolvimento de um sliding puzzle, usando a linguagem de
programação Ruby, que será executado em CLI - Command Line Interface. Para uso didático, é um bom
meio de se começar os estudos.

O resultado final será algo [assim](https://github.com/tkovs/sliding-puzzle/tree/master/ruby)

Um trecho do código que escrevi e está no github:

{% highlight ruby %}
def moviment(move)
    if valid?(move)
       /r_ = row _, c_ = column _
        _n = _ next, _c = _ current/
        rc, cc = white_row, white_column
        rn, cn = rc, cc

        if    move == UP_ARROW    then rn += 1
        elsif move == DOWN_ARROW  then rn -= 1
        elsif move == LEFT_ARROW  then cn += 1
        elsif move == RIGHT_ARROW then cn -= 1
        end
        
        @grid[rc][cc], @grid[rn][cn] = @grid [rn][cn], @grid[rc][cc]
        @moves += 1
    end
end

def white_row #row that contains the white space (0 here)
    @grid.find_index{|row| row.include?(0)}
end

def white_column #column that contains the white space (0 here)
    @grid.map{|row| row.find_index(0)}.compact.first
end
{% endhighlight %}

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
céculas) onde cada célula tem um número de 1 a 15. Uma das células não contém nada para que seja
possível a locomoção das outras sobre essa através da troca na vertical ou na horizontal com
células.

##Funcionamento

...
