---
layout: post
title:  "Comandos básicos do Terminal (Linux) (em progesso)"
date:   2016-05-12
description: Esse post não foca nenhum distro em específico pois há comandos característicos de distro, como o gerenciador de pacotes. Aqui, iremos ver comandos básicos mas importante para um bom manuseio e aproveitamento do terminal, além de quebrar o preconceito e acabar com o medo de muitos têm dessa ferramenta simples e poderosa.
tags:
- Linux
permalink: /blog/comandos-terminal
---

## Tabela de conteúdo

0. [Introdução](#id-introducao)
1. [Terminal](#id-terminal)
2. [Comando](#id-comando)
3. [Dicas](#id-dicas)
    1. [Autocomplemento](#id-dicas-autocomplemento)
    2. [Manual](#id-dicas-manual)
    3. [Ajuda](#id-dicas-ajuda)
    4. [Permissão](#id-dicas-sudo)
4. [Navegação](#id-navegacao)
    1. [Listar](#id-navegacao-listar-diretorios)
    2. [Navegar entre pastas](#id-navegacao-navegar-entre-pastas)
    3. [Criar](#id-navegacao-criar-diretorio)
    4. [Apagar](#id-navegacao-apagar-diretorios)
    5. [Renomear](#id-navegacao-renomear-diretorios)
5. [Manipulação de arquivos](#id-manipulacao-arquivos)
    1. [Listar](#id-manipulacao-arquivos-listar-arquivos)
    2. [Criar](#id-manipulacao-arquivos-criar-arquivos)
    3. [Deletar](#id-manipulacao-arquivos-deletar-arquivos)
    4. [Copiar](#id-manipulacao-arquivos-copiar-arquivos)
    5. [Mover](#id-manipulacao-arquivos-mover-arquivos)
    6. [Renomear](#id-manipulacao-arquivos-renomear-arquivos)
    7. [Exibir conteúdo](#id-manipulacao-arquivos-exibir-conteudo)
6. [Comandos gerais](#id-comandos-gerais)
    1. [Pausa (sleep)](#id-comandos-gerais-pausa)
    2. [Informações sistema operacional](#id-comandos-gerais-informacoes-so)
    3. [Data e Hora](#id-comandos-gerais-data-e-hora)
    4. [Limpar tela do terminal](#id-comandos-gerais-limpar-tela)
    5. [Histórico de comandos](#id-comandos-gerais-historico-comandos)

<hr />
<div id='id-introducao'></div>

##Introdução

A ideia desse post surgiu quando eu vi a dificuldade que minha turma no 4º ano de informática no
IFAL tem com o terminal. Há ainda uma visão ruim sobre ele, que é difícil e que interface
gráfica é mais "fácil", mas é apenas costume, eu trabalho mais rápido no terminal que usando o mouse.

<div id='id-terminal'></div>

##Terminal

![Terminal Linux](../assets/img/terminal-padrao.png)

Em primeiro lugar, observe o terminal. Na configuração do meu, o texto que aparece antes de qualquer
comando que eu insira é ```[tkovs@toby Downloads]$ ```. O que isso significa? Antes do @,
aparece o nome do usuário atual: **tkovs**. Imediatamente após o @, o nome da máquina: **toby**. Por
último, após o nome da máquina, informa-se a pasta atual que o terminal está acessando, que nesse
exemplo é a pasta **Downloads**. Eu poderia trocar essa informação, mudar a forma que ela
aparece, exibir a hora, mostrar o caminho completo da pasta, data atual, etc.

<div id='id-comando'></div>

##Comando

Dentro do Terminal, você tem a oportunidade de executar os comandos que achar necessário. Basta
digitar o nome do comando e seus argumentos. Por exemplo, para listar os arquivos do diretório
atual, basta um ```$ls``` para que uma lista seja retornada. Se você quiser listar os arquivos, e
antes de cada um exibir seu tamanho, basta usar a opção **s**. O comando fica assim: ```$ls -s```,
ou na forma mais longa: ```ls --size```. Normalmente, opções têm a forma curta e a longa. Para usar
a curta usa-se 1 traço, e na longa, 2.

No exemplo abaixo mostro o comando ls de duas formas: na primeira usando sua forma sem argumentos, e
na segunda listando os arquivos em ordem de modificação onde os mais recentes aparecem primeiro.

![Arch Linux](../assets/img/ls-argumento.png)

<div id='id-dicas'></div>

##Dicas

Algumas dicas para lhe ajudar no uso do Terminal.

<div id='id-dicas-autocomplemento'></div>

####Autocomplemento

Recurso importante, completa automaticamente o nome de um comando ou arquivo conhecido pelo
Terminal apertando a tecla **tab**, caso haja apenas uma possibilidade. Do contrário, ele lista
todas as possibilidades de comando ou arquivo conforme o texto que você inseriu antes de apertar
o tab.

<div id='id-dicas-manual'></div>

####Manual

O Linux tem um manual com a maioria dos comandos e dos programas que você instala. Para usa-lo,
basta executar ```man nome_comando```. Se quer conhecer mais sobre o comando ls, que lista
diretórios, execute ```man ls``` e verá uma explicação completa. Para sair do manual, pressione q.

Continua...
