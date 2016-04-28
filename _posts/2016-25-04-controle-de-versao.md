---
layout: post
title:  "Versionamento e iniciando no Git!"
date:   2016-04-25
description: Início da série sobre versionamento; filosofia open source; Git e Github; licenças (MIT, Apache, GPL); relação mercado de trabalho e github; grandes projetos de código aberto; tutorial sobre como usar o Git independente e sobre como integrar com o Github.
tags:
- Versionamento
permalink: /blog/versionamento-git
---

## Tabela de conteúdo

0. [Introdução](#id-introducao)
1. [Versionamento](#id-versionamento)
2. [Plataforma](#id-plataforma)
3. [Git](#id-git)
    1. [Escolher quais arquivos estão sob versionamento](#id-escolher-arquivos)
    2. [Definir uma nova versão](#id-nova-versao)
    3. [Comparação de versões](#id-comparacao-versoes)
    4. [Navegação entre versões](#id-navegacao-entre-versoes)
    5. [Ramificações](#id-ramificacoes)
    6. [Gerenciando vários contribuidores num mesmo projeto](#id-gestao-usuarios)
4. [Guia de Git para iniciantes](#id-guia-git-iniciantes)
    1. [Instalação do Git](#id-instalacao-git)
    2. [Configurando seu usuário no git](#id-configurando-usuario)
    3. [Iniciando gerência do git sob uma pasta](#id-git-init)

<hr />
<div id='id-introducao'></div>

##Introdução

No decorrer do texto será abordado alguns temas importantes sobre versionamento, seguido de um
tutorial usando o Git no terminal.

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
id-plataforma

<div id='id-plataforma'></div>

##Plataforma

Independente da plataforma que você atue, há sistemas de controle de versão para Linux, Mac OS X,
Windows, Solaris e o que mais houver. Sempre haverá implementações de softwares com esse objetivo em
diferentes linguagens, tanto privados quanto de código aberto.

Pessoalmente eu uso o Git no Arch Linux. Minha área de trabalho:
![Arch Linux](../assets/img/arch-linux.png)

<div id='id-git'></div>

##Git

Git é uma ferramenta escrita em C, de código aberto, que foi desenvolvida pra ser o sistema de
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

A cada vez que você altera arquivos, uma nova versão deles está sendo criada teoricamente falando,
mas para que os arquivos que estão sobre o controle do Git sejam salvos numa nova versão é 
necessário fazer um **commit** dos arquivos. Ao se executar um commit, você precisa fornecer uma
mensagem descrevendo a nova versão. Na mensagem, você pode dizer, de modo geral, o que foi alterado
e porque as alterações foram feitas. Isso é importante pois após vários commits pode-se listar todos
com as descrição sendo exibida, então você tem algo como uma linha do tempo no projeto.

<div id='id-comparacao-versoes'></div>

####Comparação de versões

Após ter mais de 1 versão do projeto gerenciado pelo Git, você pode comparar versões através do
**diff**. O resultado é a mostra de todas as linhas que foram alteradas.

A seguir há duas versões de um mesmo arquivo, e posteriormente a forma como o git mostra a
diferença entre essas duas versões.

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

Embora você passe a esmagadora maioria do tempo navegando no seu projeto em seu estado atual, você
pode visita-lo a qualquer momento em que um commit foi feito. No exemplo abaixo, o comando cat exibe
o conteúdo de um arquivo. Usando o comando cat duas vezes no mesmo arquivo ele mostra conteúdo
diferente, mas por quê? Porque entre as duas execuções o projeto foi alterado pra versão anterior,
então todos os arquivos foram alterados pro estado que estavam no commit anterior.

![Versões diferentes](../assets/img/navegando-versoes-antigas.png)

<div id='id-ramificacoes'></div>

####Ramificações

Quando você precisar fazer alterações no projeto, mas quiser manter uma cópia segura, não
precisa copiá-lo para algum lugar como um backup. Quando quiser adicionar um novo recurso ou alterar
um arquivo sem riscos de corromper o projeto atual e ter dificuldades de reverter para o estado em
que funcionava, você não precisa salvar uma cópia do seu projeto
como backup. Ao invés de um backup, o Git cria uma ramificação do projeto em paralelo à ramificação
principal para que se trabalhe em linhas diferentes. Elas são independentes e podem simplesmentes não
se unirem no futuro. Ao se finalizar as alterações necessárias, o Git
faz o **merge** de duas ramificações, que adiciona as alterações de uma ramificação em outra, dando a
você controle total sobre o projeto e as alterações feitas. E é claro, a qualquer momento você pode
navegar por diferentes ramificações, que no git são chamadas de **branchs**.

![Feature-x](../assets/img/feature-x.png)

<div id='id-gestao-usuarios'></div>

####Gerenciando vários contribuidores num mesmo projeto

Usando o merge, diferentes pessoas podem trabalhar num mesmo projeto de modo organizado, cada um
com sua ramificação própria atrás de um fim específico, desse modo ao não trabalharem num mesmo
arquivo a junção das alterações é feita rapidamente sem problemas. Caso você tente juntar diferentes
versões de um arquivo, com problemas de compatibilidade, o Git avisa quais são os dados que estão
entrando em conflito e aí fica por sua conta quais dados terão prioridade sobre outros no resultado
final.

<div id='id-guia-git-iniciantes'></div>

##Guia de Git para iniciantes

A seguir, um tutorial enxuto sobre como usar o Git na prática, com apoio de imagens e gifs.

![Git logo](../assets/img/git-logo.png)

<div id='id-instalacao-git'></div>

####Instalação do Git

Faça o download do Git para o seu sistema operacional seguindo os passos no próprio
[site](https://git-scm.com/download/) da ferramenta. A instalação é muito simples e leva pouco
tempo, além de ter muitos tutoriais na internet ensinando a fazê-lo.

<div id='id-configurando-usuario'></div>

####Configurando seu usuário no git

Após instalar, abra o terminal. Se você executar ```git --version```, e não obtiver a versão do git, algo
deu errado na instalação, mesmo que seja a adição do git no $PATH do seu sistema operacional.

Quando fizer commits, seu email fica atrelado a ele, então você precisa informar ao Git seu nome e
seu email. Isso também se faz necessário para se conectar ao Github, mas deixarei isso para outro
artigo.

**Seu usuário**

{% highlight console %}
$ git config --global user.name "tkovs"
$ git config --global user.email "victor.rdg@hotmail.com"
{% endhighlight %}

**Seu editor**

{% highlight console %}
$ git config --global core.editor vim
{% endhighlight %}

E para verificar se está tudo certo, execute o comando abaixo. No meu notebook o resultado foi esse:

{% highlight console %}
$ git config -l
user.email=victor.rdg@hotmail.com
user.name=tkovs
core.repositoryformatversion=0
core.filemode=true
core.bare=false
core.logallrefupdates=true
remote.origin.url=git@github.com:tkovs/tkovs.github.io.git
remote.origin.fetch=+refs/heads/*:refs/remotes/origin/*
branch.master.remote=origin
branch.master.merge=refs/heads/master
branch.source.remote=origin
branch.source.merge=refs/heads/source
{% endhighlight %}

<div id='id-git-init'></div>

####Iniciando gerência do git sob uma pasta

Em breve...
