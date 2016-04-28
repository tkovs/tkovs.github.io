---
layout: post
title:  "O que é controle de versão?"
date:   2016-04-25
description: Início da série sobre versionamento; filosofia open source; Git e Github; licenças (MIT, Apache, GPL); relação mercado de trabalho e github; grandes projetos de código aberto; tutorial sobre como usar o Git independente e sobre como integrar com o Github.
tags:
- Versionamento
permalink: /blog/versionamento-parte-1
---

## Table of Contents

0. [Introdução](#id-introducao)
1. [Versionamento](#id-versionamento)
2. [Git](#id-git)
    1. [Escolher quais arquivos estão sob versionamento](#id-escolher-arquivos)
    2. [Definir uma nova versão](#id-nova-versao)
    3. [Comparação de versões](#id-comparacao-versoes)
    4. [Navegação entre versões](#id-navegacao-entre-versoes)
3. [Guia de Git para iniciantes](#id-guia-git-iniciantes)

<hr />
<div id='id-introducao'></div>

##Introdução

No decorrer do texto será abordado alguns temas importantes sobre versionamento, seguido de um
tutorial usando o Git e o Github.

<div id='id-versionamento'></div>

##Versionamento

Versionamento é como chamamos o ato de gerenciar diferentes versões de um mesmo arquivo, cada uma 
com um id de identificação - geralmente um número.

Por experiência própria já vi muitos colegas - até mesmo professores - usarem um método de
versionamento muito manual: a cada versão do projeto toda a pasta era salva para um backup em que o
nome era a data ou o número da versão, fazendo com que todos arquivos que não foram alterados fossem
replicados e pesando muito, além de não ter recursos fundamentais que um sistema de controle de
versão tem.

Nesse artigo mostrarei o Git que é um sistema de controle de versão muito usado e exigido por
empresas, além de ser fácil de usar e estar em constante atualização e crescimento.

<div id='id-versionamento'></div>

##Git

Git é uma ferramenta escrita em C de código aberto que foi desenvolvida pra ser o sistema de
controle de versão do Linux. Hoje o Git é amplamente utilizado e é de fundamental importância
conhecê-lo. Pessoalmente, eu o utilizo para desenvolvimento de jogos, modelagem e texturização
e animação 3D, projetos de programação, trabalhos de escola, textos aleatórios, arquivos de 
configuração do linux. Gerencio tudo isso da forma fácil e prática que o Git oferece e propõe, pois
tudo acontece localmente sem necessidade de internet e seu funcionamento é simples para o usuário.

Seu funcionamento se dá, pra início de conversa, com um comando inicial numa pasta. A partir daí,
todo arquivo que for copiado ou criado nessa pasta está sob controle do Git, com algumas exceções.

A seguir, será demonstrado alguns dos recursos oferecidos pelo Git, e mais a frente um tutorial.

<div id='id-escolher-arquivos'></div>

####Escolher quais arquivos estão sob versionamento

Embora o controle de versão do Git gerencie uma pasta específica, você decide quais arquivos dentro
dessa pasta estão sob o controle desse sistema. Logo, não é porque um arquivo está dentro dessa
pasta que ele vai sofrer o **tracking** do Git - tracking é só a supervisão, o policiamento do Git
sobre algo.

<div id='id-nova-versao'></div>

####Definir uma nova versão

A cada vez que você altera arquivos uma nova versão deles está sendo criada, mas pra que os arquivos
que estão sobre o controle do Git sejam salvos numa nova versão é necessário fazer um **commit** dos
arquivos. Ao se executar um commit, você precisa fornecer uma mensagem descrevendo a nova versão.
Na mensagem, você pode dizer, de modo geral, o que foi alterado e porque as alterações foram feitas.
Isso é importante pois após vários commits pode-se listar todos com as descrição sendo exibida, então
você tem algo como uma linha do tempo no projeto.

<div id='id-comparacao-versoes'></div>

####Comparação de versões

Após ter mais de 1 versão do projeto gerenciado pelo Git, você pode comparar versões através do
**diff**. O resultado é a mostra de todas as linhas que foram alteradas.

A seguir há duas versões de um mesmo arquivos, e posteriormente a forma como o git mostra a
diferença entre duas versões.

Primeira versão:

{% highlight text %}
Olé! Como vi você?

Tchau.
{% endhighlight %}

Segunda versão:

{% highlight text %}
Olá! Como vai você?

Tchau.
{% endhighlight %}

Resultado da execução do **diff** entre as duas versões:
![Diferença entre duas versões](../assets/img/diff-ola.png)

<div id='id-navegacao-entre-versoes'></div>

####Navegação entre versões
