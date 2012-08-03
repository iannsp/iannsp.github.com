Segurança: PHP + Apache
=======================
Published: 2010-11-17 18:58:48

Segurança na internet é uma preocupação multidisciplinar. Envolve toda a
equipe de um projeto e não só os programadores e analistas. Iniciando com o
time de sysAdmins que implementam o ambiente da aplicação, o mantém atualizado
e monitoram seu comportamento através dos logs e processos e outras tantas
ferramentas disponíveis, passando pelo analista e o programador que, juntos,
selecionam as melhores técnicas para garantir que tudo corra bem e, caso surja
algum problema, o sistema seja capaz de recuperar sem prejuízos para a
operação online.  Juntos, php, apache e mysql, ou LAMP para os que gostam de
acronimos, formam o grupo de softwares mais utilizado na internet para prover
serviços que variam de simples páginas de usuários, blogs, ferramentas de
administração e negócios até serviços de compra e grandes redes de
relacionamento e como tal precisam disponibilizar recursos de segurança para
tornar todos esses serviços confiaveis. Neste artigo irei abordar algumas das
preocupações e medidas que podem ser tomadas buscando essa confiabilidade. No
Apache, por exemplo, você pode utilizar um módulo chamado mod_security, que
garante uma segurança a mais para sua aplicação criando uma interface de
detecção de ataques ao servidor. Usando a suite apt, em uma instalação de
Linux Ubuntu a instalação fica simples:

  1. apt-get install libapache2-mod-security
  2. a2enmod mod-security
  3. apache2ctl reload
Acho que o apt-get não precisa de muitas explicações, mas o a2enmode da linha
2 e o apache2ctl da 3, são, respectivamente o comando para habilitar e
desabilitar modulos do apache e o comando para interagir com o servidor,
requisitanto um reload, por exemplo, que faz com que o servidor olhe novamente
para seu arquivo httpd.conf e redefina as configurações. Vamos dar uma olhada
em algumas das configurações(mod_security.conf) que podem ser feitas para o
mod_security:

  * **SecFilterEngine **(on|off) - habilita ou desabilita o sistema de filtro.
  * **SecFilterCheckURLEncoding **(on|off) - Essa funcionalidade permite verificar se os parametros passados na url estão formatados utilizando o encoding correto, utilizando hexadecimais para representar caracteres como espaços, letras acentuadas e outros(tudo que foge ao US-ASCII). Algumas vezes os ataques são planejados utlizando valores incorretos de hexadecimais na tentativa de causar uma falha1.
  * **SecFilterScanPost **(of|off) - Habilita o filtro a agir não somente nos dados enviados via GET mas também nos enviados via POST.
Essas são configurações gerais da ferramenta. Feito isso podemos adicionar os
filtros especificos utilizando a diretiva SecFilter, abaixo coloco alguns
exemplos retirados do arquivo default de configuração: SecFilter "\.\./" -
_filtra requisições que tentem navegar nos diretorios da aplicação como
http://meuhost.com.br/../../config.php_ SecFilter "<( |\n)*script" - _filtra
requisições que tentam implementar algum tipo de XSS usando tags script_
SecFilter "delete[[:space:]]+from" -_ filtra tentativas de sql injection na
tentativa de apagar dados passando o comando delete pela URL._ SecFilter
"insert[[:space:]]+into" - _filtra tentativas de sql injection na tentativa de
inserir dados passando o comando insert pela URL._ SecFilter "select.+from" -
_filtra tentativas de sql injection na tentativa de visualizar dados passando
o comando select pela URL._ SecFilterSelective "HTTP_USER_AGENT|HTTP_HOST"
"^$" - _Filtra requisições que não tenham user agent e host, duas informações
que muitas vezes não existe nos ataques feitos utilizando CURL2._ O
mod_security não é a unica maneira pela qual você pode dar mais segurança a
sua aplicação. Existem outros cuidados simples, muitos deles descritos pela
própria Apache fundation, que podem ajudar nessa tarefa, como configurar o
host de forma a habilitar somente o que se necessita utilizando uma regra
espartana de ACL - "Desabilite tudo e depois habilite somente o que irá
utilizar" e outras, como segue.

  1. **Nunca rode o Apache usando um usuario com muitos direitos no servidor**. Deixar um serviço como o Apache rodando com um usuário que pode executar comandos como adduser, passwd, rm -rf / e outros não é uma opção, então esqueça rodar o Apache usando root(BIG_SECURITY_HOLE) por que você precisa fazer uma operação de escrita em um arquivo num folder e o usuario default(http|Apache|nobody) não pode fazer isso ou qualquer outra desculpa para isso.
  2. A mesma regra vale para os arquivos da sua aplicação.**Não existe uma desculpa potencial que acoberte um chmod 777 num arquivo de script**.
  3. **Não habilite ExecCGI e FollowSymLinks na diretiva options se não for utilizar**(o sinal de + habilita e o de - desabilita a opção) e a **opção Indexes só é valida em servidores de desenvolvimento**, afinal, você não vai querer se dar ao trabalho de criar .htaccess em todos os diretórios ou criar arquivos index.php (DirectoryIndex index.php) para eles. Caso esse cuidado não seja tomado, os arquivos de sua aplicação estarão expostos.
  4. **Personalize suas páginas de erros do Apache **deformaanãopassar informações sobre o servidor. São dois ganhos pois você deixa de dar informações que podem ser uteis aos mau intencionados e acalma os animos dos usuários de sua aplicação, que terão mensagens muito mais informativas que 400 (Bad Request) ou 506 (Service Unavailable).
E quanto ao PHP? Conceituar segurança em aplicações PHP(ou outra qualquer
linguagem de programação web) é uma tarefa que começa assim: Nunca confie nos
dados que você recebe. Não adianta fazer tudo direito e esquecer de que
existem usuários maliciosos, curiosos e que eles cometem erros. Não vale dizer
que o sistema não teria problemas se não tivesse usuários. Seja via POST ou
GET, os dados recebidos devem ser verificados e caso haja problemas, isso deve
ser tratado, vejamos um exemplo. O mais simples exemplo é o preenchimento de
um formulário de cadastro.Nessa parte, inicialmente simples de uma aplicação,
podem existir, dentre outros, os seguintes problemas. • **Preenchimento
incorreto de dados **(O cpf não ser valido-A data de nascimento ser do ano que
vem - O número de telefone ser preenchido com o endereço). Pode não parecer um
problema inicialmente, mas caso haja implementações de funcionalidades
relacionadas a esses dados, o resultado será, no mínimo, não confiavel, ou
seja as informações não serão válidas/seguras. • Um **campo de comentário que
permita formatação **pode receber código malicioso na tentativa de XSS. • Um
**upload de arquivo de de imagem **pode receber um arquivo com um tamanho
muito maior que o esperado e atrapalhar o processo de criação de miniatura, ou
pior, receber um arquivo com código dentro da anotação exif. Para que esses e
outros problemas não ocorram é primordial dividir seu tempo em 70% de
planejamento e 30%(pensar mais que codificar - quem sabe 80/20) de execução.
Não existe implementação segura que não seja "pensada" antes da implementação.
Sendo assim, o primeiro passo de segurança é deixar sua aplicação fora do
DocumentRoot. No diretório publico do apache deve ficar somente os arquivos
que são publicos. / /app /var/www No diretório /var/www fica somente o
index.php, os diretórios de scripts javascript, de css e imagens, ou seja,
tudo que se precisa para a apresentação. Muito provavelmente seu index.php vai
ser tão complexo quanto o abaixo:

    
    
    <?php
        include '/app/bootstrap.php';
        $AppC = new ApplicationController(); 
        $AppC->dispatch();
    ?>
    

Na linha 2 do index.php o arquivo de bootstrap é carregado e faz o seu
trabalho, que consiste em configurar todo o enviroment da aplicação. Tarefas
como requisitar o arquivo de configuração, definir regras para autoloading das
classes, instanciar as classes responsáveis pelo log e verificar
disponibilidade dos recursos necessários estão definidas nesse arquivo. Na
linha 3 temos a criação de uma instancia do ApplicationController(ou
FrontController) que responde por todas as requisições que seu sistema vai
processar e na linha 4, o metodo de dispatch(ou render) executa a aplicação.
Separar dessa forma a aplicação tem como resultado a segurança de que sua
implementação não será acessivel de outra forma senão por uma invasão ao
próprio servidor, impedindo que seu código seja usado de forma diferente que a
idealizada e gere problemas. Não seria possível, por exemplo, acessar um
script definido por você para uma tarefa específica. Outra item de segurança a
que se refere essa implementação é que o sistema é responsável por(devido ao
autoloading) requerer(require) ou incluir(include) os arquivos onde suas
classes estão definidas, impedindo que ocorra esse tipo de erro. A próxima
coisa a se olhar, agora que temos uma configuração mais segura para a
instalação da aplicação é o lado da entrada de dados do usuário, e por usuário
se entende a pessoa na frente do browser ou outro programador que irá consumir
uma API do seu sistema. No formulário é comum termos a implementação de
validação do lado cliente, usando javascript, cujo novo nome é jQuery3(uma
quase verdade, concorda?), mas isso não implica em deixar de validar os dados
no lado servidor, e uma boa maneira de trabalhar com isso é através de type
hinting4. Claro que existem muito mais ganhos em type hinting do que vou
abordar aqui, mas para nossa explicação, basta saber que ficará impossível
passar um parametro invalido para um método de esse definir a tipagem do
parametro que irá receber, entao, em uma implementação simplista de um caso
para validar os tipos de dados na URL, temos:

    
    
    class UrlParam{
         const INT = 1; const STRING = 2;
         private $dados = Array();
         public function add($type, $value){
              $okvalue = true;
              switch ($type){ 
                   case self::INT:
                        if (!is_int($value)) $okvalue = !$okvalue;
                        break; 
                   case self::STRING:
                        if (!is_string($value)) $okvalue = !okvalue;
                        break;
              }
              if ($okvalue)
                   array_push($this->dados, $value); 
              else
                   throw new Exception('Parametro Invalido.'); 
    }
    
    class Sistema{
         public function ExecutaTarefa(UrlParam $parametros){
         }
    }
    
    $param = new UrlParam();
    $param->add(UrlParam::INT, 10);
    $param->add(UrlParam::STRING, 10);// Lança uma Exception
    // se chegar a passar o parametro, temos dados confiáveis.
    $Sistema->ExecutaTarefa($param);
    ?>
    

O código acima é, para efeito de exemplo, um código simplista tratando uma
demonstração em que são validados os dados uma request, demonstrando uma
aplicação do type hinting, que garante que os dados são validos para um tipo
específico. O último, e não menos importante, item da lista de segurança em
php é partir para implementações de sql statments5 usando bindings e preterir
a concatenação. O binding de parametros permite a validação e colabora na
tarefa de evitar os sql injections, que é uma das maneiras com que um
"usuário" mal intencionado tentaria atacar seu sistema. Enfim, acho que o PHP,
que é hoje a quarta linguagem mais utilizada segundo o TIOBE e o Apache, que
esta presente em 54% dos servidores segundo a netcraft3 estão muito bem
amparados com relação a questão segurança e por consequencia são uma ótima
escolha para o desenvolvimento de aplicações web. referencias:

  1. Encoding URL [http://www.rfc-editor.org/rfc/rfc1738.txt](http://www.rfc-editor.org/rfc/rfc1738.txt)
  2. [](http://www.rfc-editor.org/rfc/rfc1738.txt)Man Page do CURL: [http://curl.haxx.se/docs/manpage.html](http://curl.haxx.se/docs/manpage.html)
  3. Biblioteca JavaScript jQuery:[http://jquery.com/](http://jquery.com/)
  4. Referência na documentação php para type hinting: [http://php.net/manual/en/ language.oop5.typehinting.php ](http://php.net/manual/en/ language.oop5.typehinting.php)
  5. Refenrencia na documentação php para PDO - [http://www.php.net/manual/en/ book.pdo.php](http://www.php.net/manual/en/ book.pdo.php)
  6. relatório NetCraft: [http://news.netcraft.com/archives/web_server_survey.html](http://news.netcraft.com/archives/web_server_survey.html)

