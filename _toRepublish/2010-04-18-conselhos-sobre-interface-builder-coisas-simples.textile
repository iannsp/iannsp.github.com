---
layout: default
title: Conselhos sobre Interface Builder - coisas simples
---


Conselhos sobre Interface Builder - coisas simples
==================================================
Published: 2010-04-18 12:54:00

Se você tem um Mac e se interessou pelo Xcode e programação de softwares com
interface, com certeza já se assustou(e depois superou o susto) com o
Interface Builder. Este software é o que vai te ajudar a criar interfaces, ou
formulários, como alguns dizem, que depois você irá linkar com sua
programacão. Nesse artigo, vou falar de algumas coisas que me encheram o saco
no início, por não estar acostuma com o IB e que dificultaram as coisas e me
fizeram proferir alguns impropérios. ;) vamos a elas então. **

  * Estabeleça uma ordem de trabalho, a memorize e repita sempre.
** Uma dos erros mais comuns quando voce esta programando com a dupla Xcode + Interface Builder pode ser definido pela seguinte sequencia.. _Colocar o objeto na interface, criar o IBOutlet, programar, compilar, clicar no botão e começar a reclamar que não ta funcionando bulhufas._ O que aconteceu? Simples meu caro Watson, você esqueceu um dos passos do mantra do Interface Builder, linkar o IBOutlet com o objeto da interface e o IBAction com a ação de clique ou seja lá qual ação voce desejava, assim como no video abaixo.  Parece simples, e é... mas meu, a maioria das vezes que algo não funciona na interface, é por causa desse pequeno esquecimento. Dura essa vida né. ;) ** ** ** ** ** ** ** ** ** ** ** ** ** ** **

  * **Salve as alterações do interface Builder, não ache que ele ira salvar antes de fazer um novo build pq, não vai.** :(
** Você vai lá e configura os IBOutlet e IBAction, faz o build e nada de funcionar ainda. Com certeza você esqueceu de gravar as alterações que você fez. O Xcode vai gravar automaticamente as alterações de código mas as alterações de interface estão por sua conta. ** ** ** ** ** ** ** ** ** ** ** ** ** ** **

  * **Organize as janelas do Interface Builder.**
** Curiosamente, a Apple que faz tantas interface magnificas, deixou o interface Builder se espalhar pela janela(eu sei isso é um modelo de organização de janelas, ok). Então, organize cada um dos itens de janela de uma forma padrão e mantenha assim, lógico, vá melhorando isso, organizando melhor, por que isso vai estar ligado diretamente a sua produtividade. É isso, e até a próxima. 

  * **Tenha no mínimo 2 monitores.**
Pois é, essa é a realidade, só com o monitor do MacBook você vai ficar maluco
programando, um segundo monitor vai te dar um conforto que vai fazer valer
cada um dos reais que você pagou nele. Enfim, é isso, meu primeiro post sobre
esses caras que comecei a usar agora. Já fiz softwares usando AppleScript mas
somente agora comecei a levar mais a sério o **Objective C **e estou gostando
muito dela, apesar de achar a linguagem com métodos descritivos de mais, coisa
que realmente dispensa comentários no código, ou quase. Um Abraço e até a
próxima.

