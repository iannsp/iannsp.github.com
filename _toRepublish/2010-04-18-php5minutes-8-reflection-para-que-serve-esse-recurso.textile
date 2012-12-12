---
layout: default
title: php5minutes 8 - Reflection - Para que serve esse recurso?
---


php5minutes 8 - Reflection - Para que serve esse recurso?
=========================================================
Published: 2010-04-18 18:32:00

Começo hoje uma nova seria de podcasts do php5minutes e dessa vez o assunto é 
reflection([http://en.wikipedia.org/wiki/Reflection_(computer_science)](http:/
/en.wikipedia.org/wiki/Reflection_(computer_science))). Primeiro vamos a
definição de reflection e minha interpretação é: Reflection é a habilitade de
uma classe olhar para si, internamente(assim como um humano reflete sobre ele,
suas atitude, suas qualidades e seus relacionamentos), ou seja, quando uma
linguagem implementa reflection, significa que uma instancia de um objecto
pode falar sobre ele para você, respondendo pergunta como, quem ele é, o que
ele faz e o que ele sabe.

  1. **O que eu sou?**
  2. **O que eu faço?**
  3. **O que eu sei?**
[![](http://ianntech.com.br/wp-content/uploads/2010/04/rodin-o-pensador-
225x300.jpg)](http://ianntech.com.br/wp-
content/uploads/2010/04/rodin-o-pensador.jpg)E assim, a reflexão de um objecto
permite que ele se observe, como nós olhando em um espelho. E dai vem o nome
do recurso. Tão elucidativo quanto a explicação da propriedade bubões em flex.
e outras linguagens(quem conhece a propriedade sabe do que estou falando). A
época em que comecei a me interessar pro reflexão me leva aos tempos em que
programava em Borland Delphi, ou como queiram os puristas, Object Pascal. Usar
RTTI - _Runtime Type Information_(informação de tipos em tempo de execução)
havia se tornado uma obsessão para mim na época e acho que dai vem a paixão
pelo assunto. Podemos fazer com que um código seja muito mais inteligente ao
usarmos a habilidade que ele mesmo tem em se olhar e se "auto produzir".
Talvez isso tenha a ver com meus fantasmas de programação, mas isso deixa pra
um outro post. Acho que aqui termina minhas reflexões pessoais para entrar
para o assunto de código e finalizo os parágrafos emos com a declaração: "
Imaginação é mais importante que conhecimento(Albert Einstein), logo, não
adianta saber muito sobre algo e não saber refletir isso em toda a concepção
da palavra reflexão." Pronto, acabou o emismo(sic). Vamos abordar as pergunta
que uma linguagem que implementa reflexão é capaz de responder. A primeira -
**O que eu sou?** - é quando uma instância é capaz de responder qual o seu
tipo.

    
     	class MeuObjeto{}
    	$instancia = new MeuObjeto();
    // ai perguntamos: O que é você e a resposta é -Sou uma instancia de classe do tipo "MeuObjeto".

Ainda não vou me alongar de que tipo de ganhos esse tipo de informação traz,
mas creia-me, isso vale ouro.  A segunda - **O que eu faço?** - é quando
conseguimos perguntar a uma classe quais seus métodos, suas ações, então.

    
     class MeuObjeto{}
    $instancia = new MeuObjeto();
    // O que voce faz? - Reposta: Nada.
    	class MeuObjeto{
    		public function sayHello(){
    			 return "Hello";
    		}
    		public function countUntil($until){
    			 $i = 0;
    			 do {
    				 echo $i;
    				 $i++;
    			} while($i<=$until);
    	}
    	$instancia = new MeuObjeto();
    	/*O que voce faz? - Eu sei dizer Hello(sayHello) e contar
    	ate um numero que você disser [countUntil($until)].
    	*/

Novamente, essa informação pode te ajudar em muito na programação. A terceira
- **O que eu sei?** - é quando uma instancia guarda informação/propriedades e
as usa, ou não, para realizar suas tarefas, então…

    
     	class MeuObjeto{
    		public function sayHello(){
    			 return "Hello";
    		}
    		public function countUntil($until){
    			 $i = 0;
    			 do {
    				 echo $i;
    				 $i++;
    			} while($i<=$until);
    	}
    	$instancia = new MeuObjeto();
    	// o que voce sabe? Nada.
    	class MeuObjeto{
    		$name = "Ivo Nascimento";
    		$ateOndeAprendiaContar= 42;
    		public function sayHello(){
    			 return "Hello";
    		}
    		public function countUntil($until){
    			 $i = 0;
    			 do {
    				 echo $i;
    				 $i++;
    			} while($i<=$until); }
    	}
    	$instancia = new MeuObjeto();
    	/* oq eu voce sabe? eu sei mu nome($name) e
    	um numero(ateOndeAprendiaContar).
    	*/

Redundante dizer novamente que isso vai te ajudar na programação com esse
objecto. As três perguntas foram feitas nos exemplos acima somente para as
instancias, mas poderiam ter sido feitas para as classes dessas instâncias
diretamente e muito provamente ela não saberia nada ainda, mas saberia o que
ela era e o que ela sabe fazer. Agora que fomos apresentados de forma bem
simplória[ muito prazer Reflection… o prazer é meu [seuNome] ;) ] podemos
iniciar uma conversa mais dirigida ao PHP. No PHP, o ato de realizar essas
perguntas a códigos já podia ser executado antes da implementação da
funcionalidade de reflexão, e o fato de php ser uma linguagem de tipagem
implicita, que infere o tipo de uma variável ou parametro ([http://c2.com/cgi/
wiki?ImplicitTyping](http://c2.com/cgi/wiki?ImplicitTyping) [http://en.wikiped
ia.org/wiki/Type_inference](http://en.wikipedia.org/wiki/Type_inference) X
http://c2.com/cgi/wiki?ManifestTyping [http://en.wikipedia.org/wiki/Manifest_t
yping](http://en.wikipedia.org/wiki/Manifest_typing)) nunca atrapalhou a
implementação desse tipo de funcionalidade, afinal, no que tange Objetos, não
há como instanciar algo sem dizer que tipo de instancia se deseja, e se voce
pensou em StdClass como algo sem tipo, você errou. Uma observação aqui. Isso
só era possível por que programadores que precisavam dessas informações
dedicaram tempo a implementa-las e como o código PHP recebe contribuições de
todos, que são validadas, eles enviaram o código e os coordenadores dos comits
aceitaram. _Lembre-se disso da próxima vez que alguém lhe questionar sobre a
natureza do PHP onde "não existe ninguém" para culpar por um bug na linguagem
ou falta de recurso_. Partindo de algo que não tem muito a ver com a reflexão
de objetos, mas que esclarece uma coisa que acho interessante. Quando você
declara atribui valor no php, a variável que recebe esse valor, é um zval.
Esse é o nome da estrutura de dados básica do php. Ela é um union de C(não se
martirize se não sabe o que isso significa, mas pega aqui um chicote… 30
chibatadas e 20 horas de estudos como castigo), o que significa que permite
ler um dado usando qualquer um dos tipos declarados, logo, meu caro, no fundo,
seu código é tipado(with lasers) e você não sabe ;). E entenda, isso é bom e é
ruim, mas interprete mais como bom e pro seu bem( [http://en.wikipedia.org/wik
i/Weak_typing](http://en.wikipedia.org/wiki/Weak_typing) ). A declaração do
zval é essa aqui ó...

    
     typedef union _zvalue_value {
            long lval;
            double dval;
            struct {
                    char *val;
                    int len;
            } str;
            HashTable *ht;
            zend_object obj;
    } zvalue_value;

(lembre-se das chibatadas) Bem, esse é o artigo inicial da série sobre
Reflection em PHP. Ao todo eu não sei quantos artigos e podcasts serão, mas
tenho certeza que no mínimo serão 4, cada um falando de um recurso específico
e procurando ser rico em exemplos, pq a pergunta principal a ser respondida é
como e para que usar Reflection. Ouça o cast aqui
[podcast]http://ianntech.com.br/wp-content/plugins/download-
monitor/download.php?id=29[/podcast] ou faça o download [link para
download](http://ianntech.com.br/wp-content/plugins/download-
monitor/download.php?id=30)
http://en.wikipedia.org/wiki/Reflection_(computer_science)
http://en.wikipedia.org/wiki/Metaprogramming

