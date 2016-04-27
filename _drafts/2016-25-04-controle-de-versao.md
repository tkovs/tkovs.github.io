---
layout: post
title:  "O que é controle de versão?"
date:   2016-04-25
description: Início da série sobre versionamento; filosofia open source; Git e Github; licenças (MIT, Apache, GPL); relação mercado de trabalho e github; grandes projetos de código aberto; tutorial sobre como usar o Git independente e sobre como integrar com o Github.
categories:
- Versionamento
permalink: /blog/versionamento-parte-1
---

##Introdução

O controle de versão está ligado a tudo que desenvolvemos e que pode ter uma lista de momentos de
seu estado com o decorrer do tempo. Ao escrevermos um texto, temos ele em diferentes momentos: um
inicial quando havia apenas o título; o pós-inicial quando o primeiro parágrafo foi finalizado; o
momento de inspiração quando metade do texto foi escrita rapidamente, e assim vai. Essa lógica
também se aplica à cozinhar: num momento inicial temos os ingredientes separados e organizados; num
momento x alguns ingredientes já passaram por diferentes processos e o estado atual do processo já
foi alterado. E aí surge a dúvida: onde entra o controle de versão?

Um sistema de controle de versão tem a capacidade de acompanhar um processo em andamento, de modo que
a cada momento (checkpoint), à mando do usuário, ele salve o estado de todas as variáveis envolvidas,
assim como informações essenciais sobre a alteração de variáveis - como quem alterou, o quê e quando.
Também deve ter a capacidade de comparar dois checkpoints do processo mostrando todas as diferenças,
e não apenas comparar dois checkpoints mas também fornecer uma visão completa do processo num 
checkpoint específico.

Na computação, um momento ou checkpoint em um sistema de controle de versão é chamado de commit. 
Ao se iniciar um projeto de programação
o commit inicial ocorre logo após a criação dos primeiros arquivos. A cada implementação de novas
funções novos commits devem ser feitos. Se em algum momento aparecer um bug, o sistema de controle
de versão pode mostrar todas as linhas que foram alteradas desde um commit específico, e é claro:
você vai comparar o estado atual que tem um bug com um commit que não tem o bug e ver o que mudou.
Além de mostrar o que mudou o sistema também mostra quando os arquivos foram alterados e por quem.
Junto com um sistema assim há também repositórios online onde projetos sob versionamento podem ser
expostos para trabalho em conjunto da comunidade.

##Filosofia open source

##Git

Git é uma ferramenta escrita em C de código aberto que foi desenvolvida pra ser o sistema de
controle de versão do Linux devido a alguns problemas envolvendo a ferramenta anterior de
versionamento por ser privada.

Hoje o Git é amplamente utilizado e é de fundamental importância conhecê-lo. Pessoalmente, eu o
utilizo para desenvolvimento de jogos, modelagem e texturização e animação 3D, projetos de
programação, trabalhos de escola, textos aleatórios, arquivos de configuração do linux. Gerencio
tudo isso da forma fácil e prática que o Git oferece propõe.

Abaixo, conceitos importantes para prosseguimento do artigo.

####Status

####Commit

####Branch

####Merge

##Github
