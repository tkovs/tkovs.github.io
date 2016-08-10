---
layout: post
title:  "Comandos básicos do Terminal"
date:   2016-05-15
description: Esse post não foca nenhum distro em específico. Aqui, iremos ver comandos básicos mas importantes para um bom manuseio e aproveitamento do terminal, além de quebrar o preconceito e acabar com o medo de muitos têm dessa ferramenta simples e poderosa.
tags:
- Linux
permalink: /blog/introducao-terminal
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
    5. [Info](#id-dicas-info)
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
    2. [Data e Hora](#id-comandos-gerais-data-e-hora)
    3. [Limpar tela do terminal](#id-comandos-gerais-limpar-tela)
    4. [Histórico de comandos](#id-comandos-gerais-historico-comandos)
7. [Conclusão](#id-conclusao)

<hr />
<div id='id-introducao'></div>

## Introdução

A ideia desse post surgiu quando eu vi a dificuldade que minha turma no 4º ano de informática no
IFAL tem com o terminal. Há ainda uma visão ruim sobre ele, que é difícil e que interface
gráfica é mais "fácil", mas é apenas costume, eu trabalho mais rápido no terminal que usando o mouse.

<div id='id-terminal'></div>

## Terminal

![Terminal Linux](../assets/img/terminal-padrao.png)

Em primeiro lugar, observe o terminal. Na configuração do meu, o texto que aparece antes de qualquer
comando que eu insira é ```[tkovs@toby Downloads]$ ```. O que isso significa? Antes do @,
aparece o nome do usuário atual: **tkovs**. Imediatamente após o @, o nome da máquina: **toby**. Por
último, após o nome da máquina, informa-se a pasta atual que o terminal está acessando, que nesse
exemplo é a pasta **Downloads**. Eu poderia trocar essa informação, mudar a forma que ela
aparece, exibir a hora, mostrar o caminho completo da pasta, data atual, etc.

É através do terminal que você geralmente irá trabalhar, executando comandos.

<div id='id-comando'></div>

## Comando

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

## Dicas

Algumas dicas para lhe ajudar no uso do Terminal.

<div id='id-dicas-autocomplemento'></div>

#### Autocomplemento

Recurso importante, completa automaticamente o nome de um comando ou arquivo conhecido pelo
Terminal apertando a tecla **tab**, caso haja apenas uma possibilidade. Do contrário, ele lista
todas as possibilidades de comando ou arquivo conforme o texto que você inseriu antes de apertar
o tab.

<div id='id-dicas-manual'></div>

#### Manual

O Linux tem um manual da maioria dos comandos e dos programas que você instala. Para usa-lo,
basta executar ```man nome_comando```. Se quer conhecer mais sobre o comando ls, que lista
diretórios, execute ```man ls``` e verá uma explicação completa. Para sair do manual, pressione q.
O manual fica localizado em /etc/share/man, e é dividido em seções para organizar os tipos de
comandos, que vão desde chamadas do sistema (kernel) a comandos relacionados a jogos.

<div id='id-dicas-ajuda'></div>

#### Ajuda

Muitos comandos têm por padrão a opção **--help** para que uma breve explicação sobre ele seja
retornada. Também há o comando ```help``` que exibe informações de alguns comandos que lhe são
passados como argumento.

Exemplo da opção **--help**:

{% highlight text %}
[tkovs@toby ~]$ mkdir --help
Uso: mkdir [OPÇÃO]... DIRETÓRIO...
Create the DIRECTORY(ies), if they do not already exist.

Mandatory arguments to long options are mandatory for short options too.
  -m, --mode=MODE   set file mode (as in chmod), not a=rwx - umask
  -p, --parents     no error if existing, make parent directories as needed
  -v, --verbose     print a message for each created directory
  -Z                   set SELinux security context of each created directory
                         to the default type
      --context[=CTX]  like -Z, or if CTX is specified then set the SELinux
                         or SMACK security context to CTX
      --help     mostra esta ajuda e finaliza
      --version  informa a versão e finaliza

GNU coreutils online help: <http://www.gnu.org/software/coreutils/>
Report mkdir translation bugs to <http://translationproject.org/team/>
Full documentation at: <http://www.gnu.org/software/coreutils/mkdir>
or available locally via: info '(coreutils) mkdir invocation'
{% endhighlight %}

<div id='id-dicas-sudo'></div>

#### Permissão

As vezes, você não conseguirá executar alguns comandos, pois para isso precisará de privilégios que
não tem. Privilégios esses que outro usuário tem, geralmente o administrador. Para usa-los, existe o
comando ```sudo```. Digite sudo antes do comando que precisa de permissão e o termina irá lhe pedir
a senha de seu usuário, insira ela e aperte enter, o comando ira ser executado.

Exemplo:

{% highlight text %}
[tkovs@toby ~]$ fdisk -l
fdisk: não foi possível abrir /dev/sda: Permissão negada
[tkovs@toby ~]$ sudo fdisk -l
[sudo] senha para tkovs: 
Disco /dev/sda: 465,8 GiB, 500107862016 bytes, 976773168 setores
Unidades: setor de 1 * 512 = 512 bytes
Tamanho de setor (lógico/físico): 512 bytes / 4096 bytes
Tamanho E/S (mínimo/ótimo): 4096 bytes / 4096 bytes
Tipo de rótulo do disco: gpt
Identificador do disco: BE149545-D8A3-4D79-9A8E-7F3D8A4CC935

Dispositivo    Início       Fim   Setores Tamanho Tipo
/dev/sda1        2048    616447    614400    300M Windows ambiente de recuperaçã
/dev/sda2      616448    821247    204800    100M Sistema EFI
/dev/sda3      821248   1083391    262144    128M Microsoft reservado
/dev/sda4     1083392 306280447 305197056  145,5G Microsoft dados básico
/dev/sda5   306280448 307202047    921600    450M Windows ambiente de recuperaçã
/dev/sda6   307202048 516917247 209715200    100G Linux raiz (x86-64)
/dev/sda7   516917248 967804927 450887680    215G Linux home
{% endhighlight %}

<div id='id-dicas-info'></div>

#### Info

Outro meio de se obter informações sobre comandos é através do ```info```. Basta passar o nome do
comando que você quer obter detalhes para o info e ele abrirá um programa semelhante ao man.

Exemplo de um ```info cd```:

{% highlight text %}
CD(1P)                     POSIX Programmer's Manual                    CD(1P)

PROLOG
       This  manual  page is part of the POSIX Programmer's Manual.  The Linux
       implementation of this interface may differ (consult the  corresponding
       Linux  manual page for details of Linux behavior), or the interface may
       not be implemented on Linux.

NAME
       cd — change the working directory

SYNOPSIS
       cd [−L|−P] [directory]

       cd −

DESCRIPTION
       The cd utility shall change the working directory of the current  shell
       execution  environment  (see Section 2.12, Shell Execution Environment)
       by executing the following steps in sequence. (In the following  steps,
       ...
       ...
{% endhighlight %}

<div id='id-navegacao'></div>

## Navegação

Para os exemplos, usarei a estrutura de diretórios abaixo.

{% highlight text %}
.
├── include
│   └── cbrainfuck.h
├── LICENCE
├── main.c
├── Makefile
├── README.md
├── samples
│   ├── 666.bf
│   ├── beer.bf
│   ├── gameoflife.bf
│   ├── helloworld.bf
│   ├── print.bf
│   ├── squares.bf
│   └── triangle.bf
└── source
    └── cbrainfuck.c
{% endhighlight %}

<div id='id-navegacao-listar-diretorios'></div>

#### Listar

Para listar as pastas contidas no diretório atual, basta executar ```ls -d */```.

Exemplo:

{% highlight text %}
[tkovs@toby cbrainfuck]$ ls -d */
include/  samples/  source/
{% endhighlight %}

<div id='id-navegacao-navegar-entre-pastas'></div>

#### Navegar entre pastas

A navegação entre pastas acontece de forma simples. O comando ```cd``` leva o terminal para o
diretório passado como argumento. Para voltar para um diretório acima, se passa **..** para o
cd, e para voltar para o diretório anterior, se passa **-**, já o **~** leva-o para o diretório
principal de seu usuário.

No exemplo abaixo, o terminal stá na pasta cbrainfuck. O ```cd source``` leva-o até a pasta source,
e o comando seguinte retorna-o para cbrainfuck.

Exemplo:

{% highlight text %}
[tkovs@toby cbrainfuck]$ cd source
[tkovs@toby source]$ cd ..
[tkovs@toby cbrainfuck]$ 
{% endhighlight %}

<div id='id-navegacao-criar-diretorio'></div>

#### Criar

O comando ```mkdir``` cria uma nova pasta, se ela não existe. Caso diretórios pais precisem ser criados,
deve-se usar a opção **-p** no uso do mkdir.

Exemplo:

{% highlight text %}
vs@toby cbrainfuck]$ ls -d */
include/  samples/  source/
[tkovs@toby cbrainfuck]$ mkdir test
[tkovs@toby cbrainfuck]$ ls -d */
include/  samples/  source/  test/
{% endhighlight %}

<div id='id-navegacao-apagar-diretorio'></div>

#### Apagar

Semelhante ao mkdir, há o ```rmdir```. Enquanto mkdir resume *Make Directories*, rmdir resume *Remove
Directories*. Basta passar o nome de um diretório como argumento. Caso haja arquivos dentro do
diretório, faz-se necessário o uso da opção ```--ignore-fail-on-non-empty```.

Exemplo:

{% highlight text %}
[tkovs@toby cbrainfuck]$ ls -d */
include/  samples/  source/  test/
[tkovs@toby cbrainfuck]$ rmdir test/
[tkovs@toby cbrainfuck]$ ls -d */
include/  samples/  source/
{% endhighlight %}

<div id='id-navegacao-renomear-diretorio'></div>

#### Renomear

O comando ```rename``` renomeia um arquivo ou uma pasta e funciona de um jeito simples. Ele
substitui a primeira ocorrência de **expressao** pela sua **substituição** no **arquivo** escolhido,
de modo que o comando é escrito assim: ```rename expressao substituição arquivo```.

Exemplo:

{% highlight text %}
[tkovs@toby cbrainfuck]$ ls -d */
include/  samples/  source/
[tkovs@toby cbrainfuck]$ mkdir tst01
[tkovs@toby cbrainfuck]$ ls -d */
include/  samples/  source/  tst01/
[tkovs@toby cbrainfuck]$ rename tst01/ test01/ tst01/
[tkovs@toby cbrainfuck]$ ls -d */
include/  samples/  source/  test01/
{% endhighlight %}

<div id='id-manipulacao-arquivos'></div>

## Manipulação de arquivos

Para os exemplos, usarei a estrutura de diretórios abaixo.

{% highlight text %}
.
├── include
│   └── cbrainfuck.h
├── LICENCE
├── main.c
├── Makefile
├── README.md
├── samples
│   ├── 666.bf
│   ├── beer.bf
│   ├── gameoflife.bf
│   ├── helloworld.bf
│   ├── print.bf
│   ├── squares.bf
│   └── triangle.bf
└── source
    └── cbrainfuck.c
{% endhighlight %}

<div id='id-manipulacao-arquivos-listar-arquivos'></div>

#### Listar

Para se listar apenas os arquivos de um diretório, execute ```ls -p | grep -v */```

Exemplo:

{% highlight text %}
[tkovs@toby cbrainfuck]$ ls -p
include/  LICENCE  main.c  Makefile  README.md  samples/  source/
[tkovs@toby cbrainfuck]$ ls -p | grep -v /
LICENCE
main.c
Makefile
README.md
{% endhighlight %}

<div id='id-manipulacao-arquivos-criar-arquivos'></div>

#### Criar

O modo mais simples de se criar um arquivo vazio que eu conheço é através do comando ```touch```.
Basta passar o nome do arquivo para o comando touch.

Exemplo:

{% highlight text %}
[tkovs@toby cbrainfuck]$ ls -p | grep -v /
LICENCE
main.c
Makefile
README.md
[tkovs@toby cbrainfuck]$ touch fofao.hs
[tkovs@toby cbrainfuck]$ ls -p | grep -v /
fofao.hs
LICENCE
main.c
Makefile
README.md
{% endhighlight %}

<div id='id-manipulacao-arquivos-deletar-arquivos'></div>

#### Deletar

Deletar um arquivo se dá através do comando ```rm``` passando para ele o caminho do arquivo.

Exemplo:

{% highlight text %}
[tkovs@toby cbrainfuck]$ ls -p | grep -v /
fofao.hs
LICENCE
main.c
Makefile
README.md
[tkovs@toby cbrainfuck]$ rm fofao.hs
[tkovs@toby cbrainfuck]$ ls -p | grep -v /
LICENCE
main.c
Makefile
README.md
{% endhighlight %}

<div id='id-manipulacao-arquivos-copiar-arquivos'></div>

#### Copiar

Para copiar um arquivo, basta passar o caminho do arquivo a ser copiado, e o caminho do arquivo a ser
criado com o conteúdo do outro arquivo, para o comando ```cp```. Seu uso fica assim: ```cp fonte
destino```.

Exemplo:

{% highlight text %}
[tkovs@toby cbrainfuck]$ ls -p | grep -v /
LICENCE
main.c
Makefile
README.md
[tkovs@toby cbrainfuck]$ cp main.c main.c.backup
[tkovs@toby cbrainfuck]$ ls -p | grep -v /
LICENCE
main.c
main.c.backup
Makefile
README.md
{% endhighlight %}

<div id='id-manipulacao-arquivos-mover-arquivos'></div>

#### Mover

Para mover um arquivo de um lugar a outro basta usar o ```mv``` do mesmo jeito que se usa o
```cp```, a diferença é que o arquivo fonte será apagado.

<div id='id-manipulacao-arquivos-renomear-arquivos'></div>

#### Renomear

Como explica o ```man``` quanto ao ```rename```: passa-se a **expressão** a ser substituída pela
**substituição** no **arquivo** destino. Usando, fica assim: ```rename expressão substituição
arquivo```.

Exemplo:

{% highlight text %}
[tkovs@toby cbrainfuck]$ ls -p | grep -v /
LICENCE
main.c
main.c.backup
Makefile
README.md
[tkovs@toby cbrainfuck]$ rename Make Bang Makefile 
[tkovs@toby cbrainfuck]$ ls -p | grep -v /
Bangfile
LICENCE
main.c
main.c.backup
README.md
{% endhighlight %}

<div id='id-manipulacao-arquivos-exibir-conteudo'></div>

#### Exibir conteúdo

O comando ```cat``` concatena um arquivo para a saída padrão. No terminal, quando um arquivo é
passado como argumento para o comando cat, seu conteúdo é exibido no próprio terminal.

Exemplo:

{% highlight text %}
[tkovs@toby cbrainfuck]$ cat main.c
#include <stdio.h>
#include <stdlib.h>

#include "include/cbrainfuck.h"

int main(int argc, char ** argv) {
    char *s;
    s = interpreter(argv[1], (argc > 2 ? argv[2]:"/dev/stdin"));

    if (_ERRORS_) {
        fprintf(stderr, "%s\n", _MESSAGE_);
        return 1;
    } else {
        printf ("%s", s);
        free(s);
    }

    return 0;
}
[tkovs@toby cbrainfuck]$ 
{% endhighlight %}

Também há o ```more```, que divide o conteúdo de um arquivo em páginas. Para se navegar, use o
**espaço** para continuar a leitura e o **b** para voltar uma página. Para fechar, pressione **q**.

<div id='id-comandos-gerais'></div>

## Comandos gerais

Comandos sem um objetivo em específico.

<div id='id-comandos-gerais-pausa'></div>

#### Pausa

Existe um comando que simplesmente faz uma pausa por um tempo específico. É o comando ```sleep```.
Para usado, basta passar a quantidade de segundos como argumento para o sleep. Exemplo: ```sleep
5``` pausa por 5 segundos. Mas pra que usar? Bom, 2 comandos podem ser executados um após o outro,
basta usar o **&&** entre os comandos. Exemplo: ```sleep 3600 && reboot``` faz com que o terminal
espere por 3600 segundos, equivalente à 1 hora, e então reinicia a máquina.

<div id='id-comandos-gerais-data-e-hora'></div>

#### Data e Hora

Para obter a data e a hora atual, usa-se o comando ```date```.

Exemplo:

{% highlight text %}
[tkovs@toby ~]$ date
Dom Mai 15 20:42:46 BRT 2016
[tkovs@toby ~]$ 
{% endhighlight %}

<div id='id-comandos-gerais-limpar-tela'></div>

#### Limpar a tela do terminal

Para limpar a tela do terminal, pressione Ctrl + L.

<div id='id-comandos-gerais-historico-comandos'></div>

#### Histórico de comandos

Você pode acessar suas últimas centenas de comandos digitados no terminal. Apenas execute o
comando ```history```.

<div id='id-conclusao'></div>

## Conclusão

Espero que com esse guia você esteja mais familiarizado com o terminal, e tenha perdido um pouco do
medo que é comum quando se trata de trabalhar apenas com texto, sem ajuda de interface gráfica.

Quando **eu** estou no Linux eu sempre uso terminal. É difícil eu não deixa-lo aberto. Uso o
terminal para programar (vim), para controlar versões (git), para copiar/mover/renomear/procurar
arquivos, configurar o sistema por completo, etc. Não espero que você chegue na mesma situação, mas
que ao menos se familiarize com ele. Boa sorte :)
