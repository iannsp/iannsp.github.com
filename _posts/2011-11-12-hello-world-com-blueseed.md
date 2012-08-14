Hello World com BlueSeed
========================
Published: 2011-11-12 19:45:17

[![](http://ianntech.com.br/wp-
content/uploads/2011/07/blueseed-2-300x99.png)](http://ianntech.com.br/wp-
content/uploads/2011/07/blueseed-2.png) &nbsp_place_holder;
&nbsp_place_holder; &nbsp_place_holder; &nbsp_place_holder;
&nbsp_place_holder; Utilizar o BlueSeed no desenvolvimento de uma aplicação é
simples e este artigo vai apresentar como deve ser feita a instalação e como
usar no Desenvolvimento. Vamos criar uma aplicação com o objetivo de fazer um
Hello World. Mais clássico que isso, impossível.Mãos a obra então. O Projeto
BlueSeed esta no github como projeto public e você pode acessá-lo através do
link [github.com/iannsp/BlueSeed](https://github.com/iannsp/BlueSeed). Para
criarmos a Aplicação de hello World, podemos utilizar [git://github.com/iannsp
/Hello-World-BlueSeed.git](https://github.com/iannsp/Hello-World-BlueSeed) Va
até seu diretório de projetos e faça o clone do repositório acima. git clone
https://github.com/iannsp/Hello-World-BlueSeed O Projeto acima já tem toda a
estrutura da Aplicação montada e vai permitir que foquemos no BlueSeed, porém,
gostaria de falar rapidamente dos diretórios dentro de Application. Os
primeiros 3 diretórios(**Controller**, **Model** e **View**) são relacionados
ao padrão **MVC** e não precisam de apresentações, mas caso você queira saber
mais sobre este padrão, veja este[ link sobre
MVC](http://pt.wikipedia.org/wiki/MVC) na Wikipedia. O diretério **Vo** é
utilizados para organizar seus objetos de dados, que posteriormente o BlueSeed
utiliza para persistencia de dados com ActiveRecord. O diretório **Vendor** é
onde você organiza os códigos "externos" a sua aplicação e é nele que você ira
instalar o BlueSeed dessa vez(você pode instalar o BlueSeed em um outro
diretório do sistema e somente criar o link para ele em Vendor para poder
reutilizar a instalação em outros projetos). Seguindo a configuração da
aplicação, o próximo passo é configuração do host. Caso você tenha
dificuldades para criar o host, dê uma olhada em [Criando VirtualHost no
Mac](http://ianntech.com.br/2011/11/12/criando-virtualhosts-no-mac/). Criado o
host, esta na hora de instalar o BlueSeed. No diretório raiz da Aplicação
temos o diretório de scripts. Entre nele e execute o execute o script
installBlueSeed.sh Ele irá executar o clone do BlueSeed diretamente no
diretório de Vendor. Pronto, temos a aplicação de demonstração instalada Feito
isso, é hora de usar o browser e digitar http://helloworldbs.dev Neste momento
a mensagem de hello World deve estar aparecendo para você, se não, os erros
mais prováveis são na configuração do host do projeto. Vamos aos **como
funciona**: Sua requisição ao projeto foi recebida pelo index.php e esse
carregou o BlueSeed e fez o dispatch, executando a tarefa de interpretar a
requisição. Como você não indicou nada na URL, o ApplicationController
concluiu que sua requisição é ao IndexController no método index que deve
existir obrigatóriamente nos controllers de sua Application. O método Index do
Controller IndexController fez duas coisas básicas de view, como segue:

    
            View::set('data', "Hello World");
            View::render('helloword');

Primeiro ele atribuiu a mensagem "Hello World" para a variavel data de
contexto da View e depois mandou renderizar a view HelloWorld. O BlueSeed
localizou o arquivo helloworld.php na raiz do diretorió de views, este
indicado pela configuração que esta no bootstrap da Application. Claro que tem
muito mais recurso a ser apresentado, mas este artigo é focado nessa tarefa,
então, ai temos o Hello World. &nbsp_place_holder;

