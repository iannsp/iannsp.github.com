Stored Procedure é interessante para uma aplicação?
===================================================
Published: 2011-05-01 13:55:59

[![PostgreSQL Database](http://ianntech.com.br/wp-content/uploads/2011/05/logo
pg701-300x237.gif)](http://www.postgresql.org/about/)Os Sistemas Gerenciadores
de Banco de dados atuais estão longe de ser  somente administradores de dados,
ou melhor, gerenciadores. Como sabemos, eles tem mecanismos complexos de
interpretação que lhes permitem implementar o recurso de Stored
procedure(procedimentos armazenados) e com eles podemos aplicar lógica aos
nossos dados além da que já existe com chaves primarias e estrangeiras e
restrições de operações. A pergunta que não quer calar é: Isso é interessante
para uma aplicação?  Tenho certeza de que já se perguntou isso, mas não vale a
pena reorganizar a pergunta e faze-la novamente de uma maneira mais direta. O
que eu ganho e/ou perco ao utilizar stored procedures? E a resposta pode gerar
discussões homéricas, como as que já tive com várias pessoas da comunidade,
com destaque para as que tive com os defensores mais ferrenhos de que não se
deve usar esse recurso. Começar por onde então… vamos pelo começo. O primeiro
argumento contra as stored procedures(a partir de agora SP, ok) é: **1- Esse
tipo de recurso você vai ficar preso ao SGDB.** Natural pensar assim por que
uma aplicação pode ter de mudar de SGDB no meio do caminho. No caminho do
sucesso, onde ela sai de um único usuário(admin) para N*10^24
usuarios/clientes com certeza os requisitos mudam. A requisição de performance
muda. Tudo começa a ficar cada vez mais exigente. Mais banda, mais tps, mais e
mais de cada recurso utilizado na aplicação. Mas basear-nos nesse raciocínio
nos levaria, no final das contas, a usar como modo de persistencia os arquivos
textos e eles também impõem algum tipo de restrição, então, não podemos
exagerar nesse pensamento. Nós escolhemos um SGDB por algumas caracteristicas
que fazem ele diferente dos outros. Por isso temos que **fazer uma escolha**.
E se a escolha for consciente e calculada, o SGDB irá prover os recursos
necessários por um bom tempo através de tunnings. O segundo argumento contra
SP’s é: **2- especialização do profissional.** Para que o software tenha boas
SP’s é necessário que exista alguém no time que saiba escreve-las, que entenda
a engine do SGDB, que conheça de planos de execução e se mantenha antenado as
novidades desse tipo de recurso, ou seja, tudo aquilo que os profissionais de
PHP(e de outras linguagens) já fazem diariamente com relação a sua linguagem
de programação. É dobrar o trabalho, alguns diriam. E por último, para me ater
a somente três dos motivos clássicos que as pessoas me apresentam quando entro
em uma discussão desse tipo: **3- A lógica da aplicação terá que ser mantida
em dois lugares diferentes.** O analista terá de lidar com requisitos
implementados em locais diferentes. A equipe de teste terá de lidar com testes
em componentes diferentes e o arquiteto, se defensor desse tipo de abordagem,
terá que se desdobrar para conseguir incluir nos softwares a execução dessas
SP’s. Revendo, então, aqui vão os três dos motivos que já ouvi para não
utilizar SP’s em uma aplicação:

  1. Ficar preso a um SGDB.
  2. Necessidade de um profissional treinado em desenvolvimento de SP’s na equipe.
  3. Lógica de aplicação “espalhada” em vários lugares.
Esses três motivos na maioria das vezes impedem que o software se beneficie
das SP’s no que ela foi criada para fazer.

Veja, manipular dados pode ter dois objetivos, a saber,** manipular os dados
para manter integridade**, automatizar processos de normalização e outras
tarefas que não afetam como os dados são recuperados ou gravados pelo
usuario/desenvolvedor e o outro objeto é **influenciar exatamente a maneira
como o usuario/desenvolvedor manipula essas informacoes**(mais conhecido como
regras de negocio).

O medo de todos os desenvolvedores esta na segunda opção. Stored procedures
são recursos de programação como outro qualquer. Eles simplesmente não são
built in da sua linguagem de programação predileta, mas _TAMBÉM_ são uma
maneira inteligente de lidar com os dados, assim como você instala uma
extensão especializada em lidar com o dado complexo chamado e-mail, ou para
atender requisições remotas(RPC) usando SOAP. Para exemplificar, vou falar de
PostgreSQL, de longe meu SGDB preferido e isso se dá muito devido as SP’s, que
podem ser escritas em php, shell, tcl, java, pgsql, sql e tantas outras. _
“Você pode levar seu conhecimento para dentro do SGDB”_ No caso de SP’s em php
no postgreSQL, de uma olhada aqui ([https://public.commandprompt.com/documents
/5](https://public.commandprompt.com/documents/5)) e veja até onde você pode
ir com o conhecimento a equipe tem, mas para quem não quiser ir até lá, aqui
tem um exemplo simples:  Ok, agora você tem a informação de que pode escrever
SP’s em PHP no PostgreSQL, mas ainda sobra a d**úvida de por que Escrever
código no SGDB**. A principal razão é: “_Centralizar um algorítmo que sera
utilizado por um sistema com N clientes(interfaces).”_ Quantas vezes você já
presenciou um mesmo sistema com interface iPhone, iPad, i_N_, Android, Web,
Desktop e vai saber que outro tipo de cliente pode ser criado para a mesma
aplicação dependendo dos desejos de dominação mundial do produto? Quando isso
acontece o time de desenvolvedores, sabiamente, antes de criar o projeto pensa
em uma API e dessa forma conseguia reduzir o trabalho nessas aplicações de
linguagens diferentes compartilhando algoritmos centralizados. Esse é o mesmo
raciocínio por trás das Stored Procedures que trabalham com regras de negócio.
A única diferença é que você encapsula o código dentro do banco de dados e
isso fica transparente, até mesmo caso você não tenha tido tempo para
desenvolver uma API. Ainda não esta convencido de que usar SP’s é uma boa
ideia? Vou dar outro motivo:"Observers". Você pode atrelar as SP’s a eventos
do banco de dados, normalmente executando alguma tarefa quando os dados sofrem
alteração(Insert, delete, update) e pode escrever sp’s para responder
exclusivamente a selects, te entregando informações(e não dados - uma grande
diferença). E por fim, para aqueles que insistirem em dizer que isso mudará a
forma como o desenvolvedor trabalha, pois ele farão requisições ao banco de
dados diferentes daquelas com que esta acostumado aqui vai um projeto bem
simples que pensa nisso. Novamente para PostgreSQL, ao pensar nesse problema,
acabei por criar um projeto chamado **pl2method** ([http://ianntech.com.br/200
8/10/30/pl2methods/](http://ianntech.com.br/2008/10/30/pl2methods/)) que
permite continuar programando PHP usando as SP’s como se fossem métodos comuns
de uma classe PHP. O desenvolvedor pode criar um facade sobre isso e dar ao
sistema maior transparencia e segurança caso resolva trocar detalhes da SP, um
uso simples esta descrito no artigo, porém, vou repeti-lo aqui:  No exemplo
acima é criada uma classa p que acessa o Schema Testes de uma banco de dados
dbdemo e requisita uma stored procedure chamada Teste. O pl2method permite
criticar os parametros passados, verificando tipagem, por exemplo e retorna
para a requisição as informações seguindo o sistema da PDO.
&nbsp_place_holder; É isso pessoal, espero que gostem. Um grande abraço a
todos. &nbsp_place_holder;

