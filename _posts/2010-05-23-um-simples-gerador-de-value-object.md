Um simples gerador de Value Object
==================================
Published: 2010-05-23 11:36:15

Por necessidade, acabei por desenvolver uma app de terminal simples para
geraçao de Values Object (VO). Ela consistem em um script chamado
appvomaker.php, que recebe como parametros: o **dsn**: voce passa o dsn do seu
banco de dados mysql. Mais pra frente penso em adicionar outros sgdb's o
**login**: o usuario do banco a **senha**: a senha do banco a **ação**: sao 3
as acoes que estao programadas

  1. **'listtbl'** :  listar todas as tabelas do banco para poder ajudar a escolher quais seram processadas
  2. **'*'** : indica que voce quer gerar vos de todas as tabelas do banco
  3. 'tblname'  : voce pode indicar uma tabela um mais(separando por virgula) para criar os vo's

o **outputfolder**: indica a pasta emq ue voce quer que os vo's sejam criados,
por default é a pasta em que esta sendo executado o vomaker um exemplo de uso
seria o abaixo onde me conectao ao dbtest com usuario utest e senha ptest e
gero todos os vo's gravando eles na pasta vos do sistema detalhe: os vos sao
totalmente sobrescritos por enquanto

> php appvomaker.php 'mysql:host=127.0.0.1;dbname=dbteste' 'utest' 'ptest' '*'
'vos/'

Se quiser, fique a vontade para contribuir - criticar e evoluir, o link esta
aqui
[http://code.google.com/p/phpvomaker/](http://code.google.com/p/phpvomaker/)
abraços.

