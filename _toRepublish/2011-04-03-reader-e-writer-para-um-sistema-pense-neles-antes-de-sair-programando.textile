Reader e Writer para um sistema. Pense neles antes de sair programando
======================================================================
Published: 2011-04-03 15:26:31

Ler dados e escrever são tarefas comuns a todos os sistemas. O que muda é a
natureza da entrada e a maneira como o resultado é escrito. Ler dados, por
exemplo, pode ser receber um parametro via linha de comando, um arquivo via
upload, dados passados em uma query string, e assim vai. Escrever dados é
apresentar um resultado, pode ser em formato html, csv, xml, json, pode ser
que não use "formato algum" e apresente um texto. O importante é que via de
regra um sistema inicialmente tem um formato de entrada e um formato de saida.
O cliente esta ávido para ter um software que realize as necessidades básicas
e cabe ao programador fazer isso acontecer dentro do prazo combinado. Mas vai
caber ao mesmo programador, ou outro, depois de passado o momento de extase da
entrega, "adaptar" o sistema para receber outros formatos e entregar outros
formatos. Se a gente levar em conta que **um sistema se especializa em um tipo
de entrada de dados e atende demandas de apresentação dessas informações**,
vamos perceber que trabalhamos "modelos de entrada" diferentes para o mesmo
tipo de dado e que o mesmo acontece com a saida de dados. Temos o mesmo
"modelo de dados" resultante do trabalho de inteligencia do software sobre os
dados de entrada e o apresentamos de várias maneiras, conforme a demanda do
cliente.  Esse processo todo é comum, como falei anteriormente e, mesmo assim,
a grande maioria dos sistemas não se prepara para ele e deixa para fazer as
alterações conforme elas são necessárias. Um exemplo simples, seria o abaixo:
Os problemas começam a surgir quando surgem os formatos opcionais, e acredite,
isso sempre acontece. Vamos supor que agora temos que aceitar o formato csv
que usa separador como a barra vertical. Lembre-se de que o código aqui é para
explicação de um conceito e não é de produção.  O código se duplicou. Tudo bem
que se eu melhorasse um pouco o código eu teria uma solução mais "limpinha",
mas não se pode aceitar uma sistema que para adicionar suporte a novos tipos
de leitura tem que receber manutenção, para adicionar algoritmo. O switch, que
parece tão interessante numa primeira olhada, é uma armadinha nesse tipo de
casos. A conclusão de ver um switch nesse tipo de código é a de que você tera
a mesma estrutura de switch, com as mesmas opções, copiada em outros trechos
de código. Vou ficar por aqui na quantidade de suporte, mas imagine que ao
menos bimestralmente surgisse um novo cliente com um novo formato de dados. E
seja criativo, imagine que vai ter cliente que vai querer mandar seus dados,
cada um em um slide de powerpoint. Isso já é suficiente para conseguir
imaginar o inferno de manutenção que temos aqui e a "quantidade de
responsabildiade" presa em uma parte do algortimo ao invés de ser delegada.
Tudo Isso para falar de readers e writes. Vamos ao código e depois ao
comentário:  Como esse código é somente para a apresentação do conceito,
coloquei as classes no mesmo código, mas elas estariam em seus respectivos
arquivos e também adicionei um array de formatos que não deve ser utilizado
numa implementação final pois deve haver transparencia na escolha da classe de
reader. Usando classes especializadas em interpretar cada formato, o código do
algoritmos de apresentação passa a ser especializado no algoritmo de "delegar
responsabilidades de interpretação" e não mais em realizar interpretações.
Isso vai fazer com que ele tenha um tamanho administravel, seja simples,
contenha somente as delegações de tarefas e receba pouca ou nenhuma
manutenção. A ideia se extende aos writers. Para cada tipo de saida eu tenho
uma classe especializada nesse modelo de saida para o tipo de dado no qual a
aplicação é especializada. Conclusão: Utilizar esse pattern vai te ajudar a
não ser conhecido como o PAI daquele código monstruoso que ninguém entende,
mas que funciona. E vai te tornar amigo de seus pares de programação. Toda a
empresa ganha por que esse é o tipo de código que dá agilidade a um software.
É isso ai, fazia tempo que não escrevia nada. Feito (sob a pressão de 2
pomodoro).

