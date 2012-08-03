Criando VirtualHosts no Mac
===========================
Published: 2011-11-12 17:48:38

[![](http://ianntech.com.br/wp-content/uploads/2011/11/Apache-
Server.jpg)](http://ianntech.com.br/wp-content/uploads/2011/11/Apache-
Server.jpg) &nbsp_place_holder; &nbsp_place_holder; &nbsp_place_holder;
&nbsp_place_holder; &nbsp_place_holder; &nbsp_place_holder; Uma das práticas
que vejo constantemente e que me preocupa é o desenvolvimento de aplicações
utilizando diretórios do localhost. O programador vai criando um diretório
para cada aplicações em que ele esta trabalhando e vai deixando lá, sem a
criação de um host para acessa-la. O motivo disso me preocupar é que ao
utilizar esse recurso, o desenvolvimento acaba sendo diferente do que irá
acontecer quando a aplicação estiver no ar, publicada em uma uri http válida.

> É sabido que quanto mais próximo do ambiente de produção for o ambiente de
desenvolvimento, menor vai ser a chance de ter uma dor de cabeça no momento do
deploy.

E, para diminuir os problemas, o ideal é que você esteja usando a mesma versão
de apache, a mesma de PHP, de SGDB e bibliotecas de programação. Isso tudo
além de uma URI decente. Nada mais chato do que alguém pedindo para ver a
aplicação e você respondendo. Acessa ai:
"Http://192.168.1.30/app/versao2/demo/teste.php" A parte boa é que é simples
resolver isso. Vou mostrar como configurar rapidamente um virtualhost  no
Apache para uma aplicação chamada **HelloWorldBS **que esta localizada no
diretório /_Projetos/HelloWorldBS_  em um Mac OS. Acesse o diretório de
configuração do apache /opt/local/apache2/conf crie um diretório **sites**. A
criação do diretório sites é uma maneira de simplificar a entrada de hosts no
apache. Você pode dizer ao Apache para incluir e ler todos os arquivos de
configuração que estejam no diretório sites e isso é bem mais fácil do que
ficar incluindo os configs no httpd.conf toda vez que precisar criar mais um
virtualhost. Isso vai ficar mais claro adiante no artigo. crie um arquivo
chamado **HelloWorldBS.conf**. edite este arquivo e adicione a configuração
abaixo:

    
    <VirtualHost helloworldbs.dev>
    	ServerAdmin seuemail@servidor
    
    	DocumentRoot /Projetos/HelloWorldBS/public
    	<Directory /Projetos/HelloWorldBS/public>
    		RewriteEngine on
    	    	Options Indexes FollowSymLinks
        		AllowOverride All
        		Order allow,deny
    		Allow from all
    	</Directory>
    
    </VirtualHost>

Se olhar o arquivo de configuração vai reparar que o nome do virtualhost é
hellowordbs.dev. O _.dev_ serve para facilitar a sua vida. Eu explico: Seu
host poderia ter somente o nome da aplicação, mas, como ele esta na sua
máquina, tera que informar o seu browser e rede a não utilizar o proxy para
este host, adicionando o nome dele na configuração do Proxy em sua máquina,
dentro de System Preference>Network - [Advanced Button] - [Proxies].
[![visualização da configuração de proxy informando bypass em alguns
endereços](http://ianntech.com.br/wp-content/uploads/2011/11/Screen-
Shot-2011-11-12-at-10.19.14-PM.png)](http://ianntech.com.br/wp-
content/uploads/2011/11/Screen-Shot-2011-11-12-at-10.19.14-PM.png) Se você não
utilizar algum tipo de prefixo ou sufixo, vai ter de ir até essa configuração
e adicionar o host a cada vez que criar um novo, e, caso utilize, por exemplo,
o .dev, basta adicionar o _*.dev_ como você vê na imagem acima. Agora
precisamos informar ao Apache que precisa lêr este arquivo de configuração e o
arquivo que precisa editar para isso é o httpd.conf que esta no diretório
_conf_ do seu apache, nesse caso é o /opt/local/apache2/conf. Vá até o final
do arquivo e adicione a seguinte linha: Include conf/sites/* Esta linha
informa ao Apache que ele deve carregar todos os arquivos que estiverem no
diretório sites. Novamente, esta é uma maneira de facilitar a sua vida.
Incluindo dessa maneira no  httpd.conf você não vai precisar edita-lo a cada
vez que criar um novo virtualhost. Se você reiniciar o apache nesse momento,
seu host ainda não funcionará. Isso porque o DNS não sabe "resolver" para onde
helloworldbs.dev deve apontar. Vamos resolver isso adicionando na tabela de
hosts do seu sistema operacional o host e o ip para qual ele deve ser
resolvido. Abra o arquivo /etc/hosts e no final do arquivo, adicione a
seguinte linha 127.0.0.1   helloworldbs.dev Pronto, agora no momento que você
reiniar seu apache, ele ira encontrar o host e levantar a aplicação. E você,
desenvolvedor, vai poder trabalhar com um host ao inves de diretórios no
localhost. Se você desejar organizar mais ainda seu ambiente de
desenvolvimento, pode utilizar links simbolicos e extensões para organizar o
que deve ser visto pelo Apache e o que ele deve ignorar, por exemplo, mandando
que ele carregue somente os arquivos *.up Include conf/sites/*.up e criando
links simbolicos para os arquivos de configuração que deseja que sejam hosts
ativos ln -s HelloWorldbs.conf hellowordbs.up E quando desejar que este host
seja desativado, basta apagar o link simbolico com rm hellowordbs.up o arquivo
original de configuração continuará lá, para quando você desejar subir o host
novamente. E isso ai. Abraços.

