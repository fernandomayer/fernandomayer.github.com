---
layout: post
title: "Hello World!"
date: 2012-08-06 23:51
comments: true
categories: [Test, Basics, Octopress]
---

Olá, mundo!

Esse é o primeiro post do blog, e assim como um [programa "Hello World!"](http://pt.wikipedia.org/wiki/Programa_Ol%C3%A1_Mundo), serve para testar se tudo está funcionando como deveria.

Como você pode ver, o blog foi construído através do [Octopress](http://octopress.org) (*A blogging framework for hackers*, como ele mesmo diz), que por sua vez foi baseado no [Jekyll](https://github.com/mojombo/jekyll/), que foi construído para gerar páginas de `HTML` estáticas no [GitHub](https://github.com). Mas isso é assunto para um post inteiro, já que esse é o objetivo do blog ;)

Voltando ao "Hello World" (e ao teste de configuração), na página da [Wikipedia linkada acima](http://pt.wikipedia.org/wiki/Programa_Ol%C3%A1_Mundo) está faltando uma forma de apresentar o programa no `R`! Portanto apresento aqui a maneira mais simples:

``` r
> print("Hello World!")
[1] "Hello World!"
```
Ou, de maneira mais parecida à saída das outras linguagens em geral

``` r
> cat("Hello World!\n")
Hello World!
```

Repare no `\n` no final da sentença. Ele é um [*escape*](http://en.wikipedia.org/wiki/Escape_character) e serve para adicionar uma nova linha ao final, uma herança da linguagem `C`.

E, se quisermos deixar com mais cara de programa, podemos criar uma função, que aqui vou chamar de `hw`

``` r Função para imprimir "Hello World" na tela
hw <- function(){
    cat("Hello World!\n")
}
```

Executando...

``` r
> hw()
Hello World!
```

Assim fica fácil perceber a utilidade de um programa tão simples como esse. Se você não sabia e queria aprender como funciona uma função no `R`, agora fica mais fácil entender, não?

Tão simples quanto o programa, seria se quiséssemos saber a probabilidade $P(\cdot)$ de sortear a letra `L` ao acaso, entre as letras das palavras `HELLO` e `WORLD` juntas. Esta probabilidade seria

$$
P(X = L) = \frac{3}{10} = 0.3
$$

Se você chegou até aqui, parabéns! Você e o Octopress passaram no teste de configuração!

`\V/ LLAP`