---
layout: post
title:  "Introdução básica à linguagem C"
date:   2016-03-31
description: Material produzido para revisão básica da linguagem C. O público alvo é de pessoas que precisam aprender C mas sem se aprofundar - Institutos Federais com curso técnico de informática, por exemplo.
categories:
- linguagem c
permalink: /blog/introducao-linguagem-c
---

####Tipos de dados

**Int**: Número inteiro. Sem casas decimais.
> Ex: 0 -543 2015

**Char**: Letra. Apenas 1, se quiser mais é necessário criar um vetor, o que daria uma string.
> Ex: 'a' '%' 'Z' '+'

**Float**: Número real. Com casas decimais.
> Ex: 0.5 -5.43 20.15

**Void**: Tipo vazio. Por enquanto você não precisa saber muito sobre esse tipo.

####Comentários

Comentários podem ser escritos de duas formas: linha única ou várias linhas.

{% highlight c linenos %}
int idade; // Variável para guardar uma idade

/* Um comentário simplesmente pra dizer que o
   comentário de uma linha acima é inútil pois
   o nome da variavel já diz tudo...
*/
{% endhighlight %}

####Função main

Se seu programa será um executável ele precisará da função main que sempre é a primeira a ser chamada. O esqueleto básico que, provavelmente, todos seus programas iniciais terão, é o seguinte:

{% highlight c linenos %}
// Biblioteca com funções printf e scanf (e muitas outras, é claro).
#include <stdio.h>

// Função main. Retorna um valor inteiro. Recebe nenhum valor.
int main(void) { // O 'abre chaves' indica o começo da função

    // Código aqui
    // Código aqui

    // Retorna 0 se chegar até essa linha do código.
    return 0;
} // O 'fecha chaves' indica o fim da função.
{% endhighlight %}

####Bibliotecas

Você pode criar um arquivo e nele escrever funções para um determinado propósito. Esse arquivo não tem o main() pois não é um executável, não é um programa, é uma biblioteca. Por exemplo, se você não quisesse escrever a mesma função em vários programas - *calcular área de um triangulo, por exemplo* - você a escreveria em apenas um arquivo, e no seu começo dos seus próximos algoritmos você incluiria tal arquivo no seu programa. A função **printf** e a **scanf** estão na biblioteca *stdio*, por isso você costuma adicionar essa biblioteca nos programas. Exemplo:

{% highlight c linenos %}
#include <stdio.h>

int main(void) {
    // Se não tivesse adicionado a stdio nesse código, daria um erro na próxima linha.
    printf ("Hello, world!");

    return 0;
}
{% endhighlight %}

####Escopo

Um escopo é o que delimita o código que pertence a uma função, é o que diz a o quê tal código pertence. Um código não pode acessar variáveis que pertencem a um escopo que não seja o próprio ou um anterior.

{% highlight c linenos %}
#include <stdio.h>

int main(void) { // Início do escopo do main.

    int i = 1;
  
    if (i == 1) { // Início do escopo do if.
        int j;
        // A seguinte linha não dá erro.
        j = 10;
        // É possível exibir a variável j aqui usando printf.
        // Não ocorre um erro na próxima linha pois o escopo do if está dentro do escopo do main, ou seja, o escopo do main é um escopo anterior ao do if.
        i = 0; 
    } // Fim do escopo do if.
  
    // Erro na linha abaixo, pois a variavel j não existe fora do escopo do if.
    j = 10;

    return 0;
} // Fim do escopo do main.
{% endhighlight %}

####Declarando variáveis & Vetor & String

Um vetor é apenas uma variável capaz de conter vários valores do mesmo tipo. É como se uma variável comum fosse um pedaço de papel (uma página) e um vetor fosse um livro (conjunto de páginas). A seguir, um "tipo de dado" chamado string.

**String**: Na verdade não há o tipo string, o que existe é um vetor de char onde o último elemento sempre deve ser o '\0' que indica o fim da string. Sendo assim, se quiser uma variável pra armazenar a string "panda" seriam necessários 6 espaços no vetor: 5 para o nome "panda", e 1 para o '\0'.
> Ex:

{% highlight c linenos %}
// Fazer isso:
char s[6] = "panda";

// É a mesma coisa que fazer isso:
s[0] = 'p';
s[1] = 'a';
s[2] = 'n';
s[3] = 'd';
s[4] = 'a';
s[5] = '\0';
{% endhighlight %}

Declaração de variáveis

{% highlight c linenos %}
#include <stdio.h>

int main(void) {
    // Variável do tipo inteiro chamada i.
    int i = 10;
    // Variável do tipo float chamada f.
    float f = 1.83; // Usa-se ponto para separar as casas decimais. Cuidado pra não usar vírgula, dará erro.
    // Parece se declarar um vetor, usa-se colchetes depois do nome da variavel com o tamanho de elementos.
    // Uma string por exemplo, é um vetor de char. Logo, pra guardar o nome panda, como visto anteriormente, bastaria o seguinte:
    char s[6] = "panda";
    
    return 0;
}
{% endhighlight %}

####Funções de leitura e escrita (printf / scanf)

Para escrever algo na tela (uma mensagem ao usuário ou o resultado de uma conta) é necessário usar a função **printf**. Para ler um valor do usuário, a função **scanf**.

{% highlight c linenos %}
#include <stdio.h>

int main(void) {
    int i;
    char c;
    char s[20];
    
    // Scanf
    // Parece receber uma informação do usuário usa-se a função scanf. Ela recebe uma string e as variáveis que receberão o valor.
    // Na string, informamos os tipos dos dados que serão lidos e, separadas por vírgula, as variáveis.
    // %d - inteiro / %f - float / %c - char / %s - string
    
    // O & antes da variável é necessário pois a função precisa saber o endereço da variável i para salvar o valor lá.
    scanf ("%d", &i); // %d entre aspas pois é uma string, e a variável após a vírgula.
    
    // Leitura de uma letra.
    scanf ("%c", &c);
    
    // Leitura de uma string. O & não é necessário pois essa variável não é como as outras, é um vetor, e ao usar seu nome já se está dizendo seu endereço.
    scanf ("%s", s);
    
    // A função printf recebe uma string e, se necessário, valor de variáveis na string.
    // Parece exibir o conteúdo de variáveis não é necessário o &.
    printf ("Numero informado pelo usuario: %d", i);
    printf ("Tchau!");

    return 0;
}
{% endhighlight %}

####Operadores && Aritmética

{% highlight c linenos %}
#include <stdio.h>
/*
+ soma
- subtração
/ divisão
* multiplicação
% resto

== igual
!= diferente
< menor
> maior
<= menor ou igual
>= maior ou igual
! negação
*/

int main(void) {
    // Exemplo:
    float a, b;

    printf ("Insira dois valores: ");
    scanf ("%f %f", &a, &b);
    
    printf ("Soma: %f\n", a + b);
    printf ("Subtracao: %f\n", a - b);
    printf ("Multiplicacao: %f\n", a * b);
    printf ("Divisao: %f\n", a / b);
    printf ("Resto da divisao: %f\n", a % b);

    return 0;
}
{% endhighlight %}

####Condição (if)

O **if** é uma palavra-chave em C para se tomar decisões, fazer comparações.

{% highlight c linenos %}
#include <stdio.h>

int main(void) {
    int a, b;
    
    // O usuário insere o valor de a e o valor de b.
    scanf ("%d %d", &a, &b);
    
    // if (condição) { código }
    // Aqui é comparado a e b.
    if (a == b) { // Início do escopo do if
        printf ("Valores iguais.");
    } // Fim do escopo do if
    
    if (a != b) { // Início do escopo do if
        printf ("Valores diferentes.");
    } // Fim do escopo do if.
    
    // Não é necessário fazer duas condições pois existe o else. Else é o senão, é onde está o código que será executado caso a condição não seja satisfeita.

    // Comparação. O código do escopo do if será executado apenas se a condição do if for verdadeira.
    if (a == b) { // Início do escopo do if
        printf ("Valores iguais.");
    } // Fim do escopo do if
    // Se a condição do if for falsa, o código do else será executado.
    else if (a > b) { // Início do escopo do else
        printf ("a maior que b.");
    } // Fim do escopo do else.
    else { // Início do escopo do else
        printf ("a menor que b"); // Se a não é igual a b, não é maior, então é menor.
} // Fim do escopo do else.
    
    return 0;
}
{% endhighlight %}

####Loops (repetição)

Para usar esse recurso existem algumas palavras-chave como while, for e do/while. Na while só é necessária uma condição e, toda vez que ela for verdadeira, o código no escopo do while é executado.

{% highlight c linenos %}
#include <stdio.h>

int main(void) {
    int i = 100;
    
    while (i > 0) {
        printf ("i maior que 0");
    }

    printf ("i menor ou igual a 0");
    return 0;
}
{% endhighlight %}

Para se usar o for 3 definições são necessárias possíveis. Atribuição, condição, ação.

{% highlight c linenos %}
#include <stdio.h>

int main(void) {
    int i;
    
    // Esqueleto: for (atribuição; condição; ação) { código }
    // A atribuição ocorre apenas 1 vez
    // A condição é checada toda vez que o for é executado ou seu escopo acaba. Se a condição for verdadeira ele será executado novamente (a ação também)
    // A ação ocorre toda vez após a condição ser checada. A ação só acontece a partir da segunda vez que o for é executado.
    for (i = 1; i <= 10; i++) {
        printf ("%d\n", i);
    }

    return 0;
}
{% endhighlight %}

O do/while é como o while, porém sem comparação inicial. Diferente do while que só roda a primeira vez que a condição for verdadeira, no do/while sempre vai executar o código de seu escopo pelo menos 1 vez.

{% highlight c linenos %}
#include <stdio.h>

int main(void) {
    int i = 0;
    
    do {
        printf ("Valor de i: %d\n", i);
        i = i + 1; // Ou i++
    } while (i < 10);

    return 0;
}
{% endhighlight %}

####Funções

Funções são muito úteis, inicialmente, para modularizar seu código. Um meio de separar trechos de códigos que têm um mesmo objetivo em um lugar separado do resto do código. Funções são como empregados, onde cada um tem uma função específica a fazer e, ao ser necessário que x trabalho seja realizado você não o reescreve no código, simplesmente chama a função encarregada de realizar a tarefa x.

Funções são escritas de acordo com a seguinte sintaxe: <tipo de retorno> <nome função>(<tipo parametro> <nome parametro, ...) { <codigo> }

{% highlight c linenos %}
#include <stdio.h>

// <tipo_retorno> <nome> (<parametros>)
// {
//    <codigo>
//    <codigo>
//
//    return <valor>; // return apenas se o tipo de retorno não for void
// }

// Exemplo:

void saudacao(void) {
    printf ("Oi pessoa!");
}

int soma(int a, int b) {
    return a + b;
}

int main(void) {
    saudacao();
    printf ("5 + 3 = %d", soma(5, 3));

    return 0;
}
{% endhighlight %}
