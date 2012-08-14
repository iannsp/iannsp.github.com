---
layout: default
title: php5minutes 9 - Reflection Class- Me diga de que classe é que te direi quem és ;)
---


php5minutes 9 - Reflection Class- Me diga de que classe é que te direi quem és ;)
=================================================================================
Published: 2010-04-20 06:37:09

Vamos para a segunda parte da série do php 5 minutes sobre Reflection, e vamos
começar com um link que pode ser útil para hoje. E dá-lhe
[docs.php.net](http://docs.php.net) [Reflection
Class](http://docs.php.net/manual/en/class.reflectionclass.php) Pronto, agora
que você ja clicou no link e deu uma olhada no assunto de hoje, a gente pode
começar a bater um papo, meio de louco ou maluco, se é que me entende. Muitas
vezes quando estamos programando, procuramos soluções para problemas ligados
ao "saber com que tipo de informação estamos trabalhando" e isso acaba, em
algumas das vezes, nos fazendo descriminar algum tipo de propriedade para
descrever essas informações, um caso bem simples é o de uma classe que
representa uma informação em uma tabela do banco de dados, vulgo, um VO ou
mais pra frente, um model(se quiser, pode ouvir sobre model no podcast do
[php5minutes de número 5](http://ianntech.com.br/2010/02/21/php5minutes-5-o-m
-do-mvc/)). Nesses casos, duas abordagens são comumente utilizadas para ligar
o objeto ao o que ele representa. A primeira delas é colocar uma propriedade
que indique a que tabela aquele objeto esta linkado, como abaixo:

    
    
    namespace byCommon;
    
    class Discovery{
    	public static function Type($obj){
    		return $obj->getTableName();
    	}
    }
    
    class Usuario{
    	private $tableName = "Usuario";
    	public function getTableName(){
    		return $this->tableName;
    	}
    }
    

A outra é usar de reflection para perguntar a instancia, de que tipo ela é.
Ambas necessitam de um padrão de codificação. Você nao podera dizer que
tablename é "user" quando a tabela chama usuario e nao podera criar uma classe
chamada User quando ela na verdade representa uma entrada de dados da tabela
do tipo usuario, porem, ao utilizar reflection para verificar o tipo que a
instancia representa voce poupa seu código de mais uma propriedade que não tem
nada a ver com o objetivo dele.

    
    
    namespace byReflection;
    class Discovery{
    	
    	public static function Type($obj){
    		$rObj = new \ReflectionClass($obj);
    		return $rObj->getName();
    	}
    }
    
    class Usuario{
    	
    }
    

Os dois modelos acima resolvem o problema de “identificar um tipo”, mas eu
penso no modelo que informa o tableName como uma propriedade privada como um
modelo que te obriga a adicionar uma informação que não pertence muito ao que
voce deseja fazer, é mais uma informação do sistema do que uma informação
valida do objeto. Já a opção que usa reflection me deixa livre para Programar
baseado unicamente num padrão que já é comum, dar a variavel ou classe um nome
que a descreva. Eu usei o ReflectionClass, que é o assunto desse cast para
somente recuperar o nome da classe origem da instancia. A função utilizada é a
getName que retorna o nome todo do objeto e se você executou o codigo([que
esta aqui para download](http://ianntech.com.br/wp-content/plugins/download-
monitor/download.php?id=31)), deve ter percebido um pequeno detalhe, vejamos o
código:

    
    
    require_once 'discovery.class.php';
    require_once 'usuario.php';
    
    $a = new byReflection\Usuario;
    echo "O objeto a é do tipo: ".byReflection\Discovery::Type($a)."\n";
    //ou
    
    $a = new byCommon\Usuario;
    echo "O objeto a é do tipo: ".byCommon\Discovery::Type($a)."\n";
    

retorna

    
    
    O objeto a é do tipo: byReflection\Usuario
    O objeto a é do tipo: Usuario
    

O retorno quando utilizamos a getName sobre objetos que estão sendo
organizados em namespaces é esse, o namespace completo. Para resolver esse
problema temos uma outra função de Reflection, a getShortName, e ai o código
fica assim.

    
    
    namespace byReflection;
    class Discovery{
    	
    	public static function Type($obj){
    		$rObj = new \ReflectionClass($obj);
    		return $rObj->getShortName();
    	}
    }
    

Caso a classe não esteja em um namespace, não vai haver problema não. A função
getShortName esta lá para te dar o nome raiz da classe. Agora vamos a uma
outra questão, sera que seu código é confiável? Humm, calma lá, não to falando
da segurança na relação software/usuário e sim se uma classe é confiavel, ai
você pensa: “Claro que é, foi você quem escreveu!!;)” A pergunta é outra, voce
implementa um sistema que precisa confiar em uma classe, assinar um contrato
com ela de que ela tem algumas funcionalidades que o sistema precisa. Contrato
é coisa que se implementa com interface, correto. Se o cara faz implements X,
ele vai ter de implementar o que ta declarado na interface. divagando um
pouco.Você ja parou para pensar de por que somente métodos publicos entram
numa interface? Quando você assina um contrato, o objeto do contrato é algo
com relação a outros, uma empresa ou pessoa. Essa relação só se dá através do
que você faz publicamente, ou seja, de suas ações com relação a outrem. Essa é
a ideia de contrato. Vamos então ao codigo:

    
    
    interface Documento{
    	public function save();
    	public function getInfo();
    }
    
    class XmlDoc implements documento{
    	
    	public save(){
    		// salva o documento no local adequado e realiza as acoes necessarias, como gravar no db, criar link, enviar um email de aviso e etc...
    	}
    	public getInfo(){
    		// retorna um stdClass com dados do documento e cada documento tem um conjunto diferente de informacoes e compartilha outras que são comuns.
    	}	
    }
    
    class CsvDoc{
    	
    }
    
    class processaDocumento{
    	
    	public function exec($Documento){
    		$Documento->save();
    	}
    }
    

No mundo perfeito, o código acima deveria ser confiavel. Você se deu ao
trabalho de criar uma interface para aplicar nos documentos e a usou no
XmlDoc, mas outro programador não implementou a interface no CsvDoc. O
problema é que o método do processador de Documentos usa o método Save, que
ele jura de pé junto que existe e quando não existir, vai dar problema. Ao
usarmos o codigo acima, como nesse exemplo:

    
    
    require_once 'documento.interface.php';
    require_once 'xmldoc.class.php';
    require_once 'csvldoc.class.php';
    require_once 'processadocumento.class.php';
    
    $a = new XmlDoc;
    $b = new CsvDoc;
    processaDocumento::exec($a);
    processaDocumento::exec($b);
    

é lançado um erro

    
    
    PHP Fatal error:  Call to undefined method CsvDoc::Save() in processadocumento.class.php on line 6
    
    Fatal error: Call to undefined method CsvDoc::Save() in processadocumento.class.php on line 6
    

A forma que todos resolvemos isso é usando o typehint, fica assim então, a
nova versao de processaDocumento:

    
    
    class processaDocumento{
    	
    	public static function exec(Documento $Documento){
    		$Documento->Save();
    	}
    }
    

E ao rodarmos novamente temos outro erro:

    
    
    PHP Catchable fatal error:  Argument 1 passed to processaDocumento::exec() must implement interface Documento, instance of CsvDoc given, called in file2.php on line 10 and defined in processadocumento.class.php on line 4
    

Ja melhorou, temos agora que simplesmente o erro foi lançado pq CsvDoc não
implementava a interface necessaria (sim, da pra testar interface com type
hinting e não somente o tipo da classe). basta agora tratarmos esse erro,
correto? aqui vai.

    
    
    function errorHandler($errno, $errstr, $errfile, $errline) {
     if ( E_RECOVERABLE_ERROR===$errno ) {
    	echo "tratar Erro aqui";
    	return false;
      }
      return true;
    }
    set_error_handler('errorHandler');
    
    require_once 'documento.interface.php';
    require_once 'xmldoc.class.php';
    require_once 'csvldoc.class.php';
    require_once 'processadocumento.class.php';
    
    $a = new XmlDoc;
    $b = new CsvDoc;
    processaDocumento::exec($a);
    processaDocumento::exec($b);
    

Mas voce tambem pode implementar um teste que garanta que as classes da pasta
documento tenham a interface implementada e rodar esse teste depois de cada
commit para garantir a integridade do código(afora permitir um papinho com o
dev que deixou de fazer o que ele devia ;) ) algo como abaixo:

    
    
    $dirname = "docclass";
    require_once 'documento.interface.php';
    $dir = new DirectoryIterator($dirname);
    foreach ($dir as $fileinfo) {
        if (!$fileinfo->isDot()) {
    		$detalhe = new SplFileInfo($fileinfo->getFilename());
    		require_once $dirname."/".$fileinfo->getFilename();	
    		$rClass = new ReflectionClass( ucfirst($detalhe->getbaseName('.class.php')) );
    		if( ! in_array( 'Documento',$rClass->getInterfaceNames())){
    			throw new ErrorException("Interface Documento não implementada na classe ".ucfirst($detalhe->getbaseName('.class.php')));
    		} 
        }
    }
    

E ai ir dormir mais tranquilo sabendo que você consegue testar se o que voce
precisa esta la no código, do jeito que você planejou. No código acima, com
relação a reflection, tem o getinterfaceNames, retornando um array com o nome
das interfaces que foram utilizadas na classe e asism você consegue planejar
metodos para teste utilizando reflection também. acho que o artigo já esta
longo demais, vamos ao podcast, então. [download do
código](http://ianntech.com.br/wp-content/plugins/download-
monitor/download.php?id=31)

[download do zip do podcast](http://ianntech.com.br/wp-content/plugins
/download-monitor/download.php?id=33) [podcast]http://ianntech.com.br/wp-
content/plugins/download-monitor/download.php?id=32[/podcast]

