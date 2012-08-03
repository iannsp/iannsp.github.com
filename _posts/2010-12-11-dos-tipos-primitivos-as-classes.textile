dos tipos primitivos as Classes
===============================
Published: 2010-12-11 21:44:03

Todo programador, ao iniciar o seu aprendizado, recebe a informação de que
existem os tipos primitivos de dados, a saber:

  * inteiro
  * caracter
  * ponto flutuante
  * boolean

A lista muda, para mais ou para menos e também sofre efeito da maneira como a
linguagem trata esses tipos(forte, fraca, estatica, dinamica), mas permanece
com uma caracteristica, a de que, cada um desses formatos de dados são
maneiras de anotar somente um (1) dado em cada variavel do tipo. Isso é o que
caracteriza um tipo de dado como primitivo.

Com esses tipos o programador começa a trabalhar. Não importa a linguagem,
essa é a premissa básica para conseguir começar a brincar. Entender os tipos
de variáveis possíveis e como atribuir e ler valores a ela.

O tempo passa e o programador vai aprendendo uma coisa aqui, outra acolá. Até
que ele reconhece que sem o conceito de conjunto ele pouco irá fazer.

A primeira vez em que ele "coleciona" valores co-relacionados é usando um
array. E novamente ele aprende coisas novas e mais coisas novas sobre
trabalhar utilizando essa maravilha de tipo de dados.

O Array é nosso primeiro tipo de dado composto... composto de outros tipos de
dados.

Claro que existem outras estruturas de manipulação de conjunto de dados, como
as listas, mas array fica lá, sendo utilizado durante muito tempo para lidar
com esses dados parecidos.

Se vai guardar um monte de nomes e telefones, chama o array de listaTelefonica
e pronto.

É ponto comum que isso resolve o problema, imagino eu. Você pode "iterar" pelo
array e manipular os dados, imprimir e tudo o mais que achar necessário.

Tudo vai bem enquanto se cria softwares simples e dependendo do nível de
organização proposto no software, continua bem até nos sistemas complexos,
porém, agora você tem alguns problemas.

  1. Os dados estão todos preenchidos ?
  2. O array que tenho é do tipo que eu espero ter?
  3. Preciso adicionar um campo, o impacto vai ser grande?

A resposta para todas esses perguntas esta baseada, totalmente, na confiança.
Você confia em uma série de algoritmo para responder essas perguntas. Eles
manipulam o array e seus registros, validam, iteram e todo o mais, mas
convenhamos, o sistema baseado somente em confiança já foi tentando em outras
áreas e graças a suas falhas temos os advogados, os auditores, os juízes de
futebol e outras categorias que estão lá primordialmente para garantir que a
confiança seja algo real ou seja penalizada.

A confiança evoluiu para contratos e regras, todos eles aplicados no objeto em
que se confia.

Você confia em uma prestação de serviço pq tem um contrato para garantir isso
e da mesma forma você deve ter mecanismos de garantia para seu tipo de dados
(viajei muito ?)

Não da para programar somente na confiança. Até dava quando os sistemas eram
isolados, mas não mais.

Então o próximo passo é procurar por maneiras de representar melhor esses
dados. Não vamos aqui falar de um struct(ou vamos?). Vamos no focar na maneira
de representar dados de maneira assertiva, na qual o dado pode ser garantido
por ele mesmo e não por uma porção de código externa a ele.

vamos a um exemplo.

[caption id="attachment_760" align="alignnone" width="300" caption="array para
objeto"][![](http://ianntech.com.br/wp-
content/uploads/2010/12/01-300x207.png)](http://ianntech.com.br/wp-
content/uploads/2010/12/01.png)[/caption]

O que é melhor?

Alguns vão dizer que no caso acima não mudou nada, tanto faria usar um array
ou uma classe.

Vamos pensar no código que gira em torno desse Produto tão precioso.

Alguns tarefas são básicas, todas elas ligadas a confiança lembra?

**1 . Os dados estão todos preenchidos?**

quando for utilizar a representação do seu produto para, por exemplo, gravar
na tabela de itensdeVenda num tiquete feliz no supermercado.

[caption id="attachment_764" align="aligncenter" width="471" caption="array e
objeto metodo Gravar"][![array e objeto metodo Gravar](http://ianntech.com.br
/wp-content/uploads/2010/12/03.png)](http://ianntech.com.br/wp-
content/uploads/2010/12/03.png)[/caption]

Um comentário antes de continuar. As funções estão aqui para facilitar a
apresentação do exemplo.

Repare que para o caso usando Array eu adicionei no metodo de gravação uma
validação, que teria que ser adicionada também no método para apagar, alterar,
e talvez até no selecionar(ja que o banco de dados pode não estar completo).

O código de validação pode ficar centralizado, concordo, em uma função
exatamente para isso, concordo novamente, aproveito e pergunto, você esta me
propondo escrever uma biblioteca de código que trate de produto, correto?

**O array que tenho é do tipo que eu espero ter?**

Além do problema de validar, pode ser que venham campos adicionais, indices
associativos que algum outro programador colocou lá para facilitar a
manipulação. Qualquer coisa pode acontecer quando se trabalha confiando nos
dados, por engano ou intencional os dados pode ser alterados de maneira que o
processo de manipulação seja cheio de validações pelo meio do caminho,
complicando cada vez mais.

**Preciso adicionar um campo, o impacto vai ser grande?**

Outra coisa é, adiciona ai pra mim mais um campo chamado marca, e imagina o
impacto dessa adição simples de um campo em todo o sistema.

Já no exemplo da função que trabalha com Objeto temos que ela pode confiar
plenamente no parametro recebido, pq o programador não usou somente de
confiança ;), ele usou um dispositivo para garantir que a confiança não fosse
traida, forçando o tipo de dados.

E também pode passar direto para o passo de gravação sem testar se os campos
estão preenchidos simplesmente por que o construtor do objeto Produto obriga
passar todos os valores, nada ali era opcional.

> Trocar confiança por controle.

Com relação aos dados que uma aplicação manipula, a frase acima reflete o que
significa a troca de tipos de dados como array e os primitivos para um
dado(instancia) definido utilizando um modelo (classe).

Os impactos são somente positivos, numa espécie de delegação do controle dos
dados da aplicação para a própria classe que defini o dado, assim, o sistema
pode cuidar do fluxo da informação e sua manipulação ligada ao Core Bussines
para qual foi criada, ao invés de ficar preocupada em validar os dados o tempo
todo.

Esse artigo foi escrito com o intuito simples de levar os programadores que
hoje usam o conteito de OO de uma forma incipiente a refletir sobre os ganhos
que terão ao passar a utilizar um modelo OO cada vez mais próximo do completo.

Até mais ver.

