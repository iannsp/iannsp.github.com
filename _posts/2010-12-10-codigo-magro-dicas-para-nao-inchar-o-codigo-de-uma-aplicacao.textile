Código Magro - Dicas para não inchar o código de uma aplicação
==============================================================
Published: 2010-12-10 15:09:03

Código magro é aquele código que contém exatamente a massa que ele precisa ter
para conseguir realizar o trabalho para o qual foi desenvolvido. Esse é o
código ideal - magro e eficiente. Técnicamente, todo projeto, ao nascer, se
encontra assim. Ele implementa todo o necessário para realizar suas tarefas,
maior parte das vezes de forma eficiente. Mas ai surgem os novos pedidos de
funcionalidades e pronto. O código começa a engordar, inchar, receber mais
código para cobrir a nova funcionalidade e a cada ciclo de desenvolvimento ele
vai se tornando mairo até chegar no elefante branco do qual nenhuma linguagem
pode se dizer livre e com o qual ao menos uma vez na vida qualquer
desenvolvedor vai lidar. Esse artigo trata de algumas atividades que ajudam a
impedir que isso não ocorra.

> “Se esta funcionando, não mexa.”

O efeito de aumento de linhas no projeto é diretamente ligado a essa máxima de
engenharia tão comum e estressante. Reflexo das pressões por prazos curtos de
análise e implementação e também por caracteristicas de metodologias aplicadas
a fabricas de software, essa máxima faz com que as novas funcionalidades sejam
adicionadas ao software sem um processo de consolidação tanto do conceito
quanto do código. Olhar o código antigo no momento de acionar o novo é
obrigação do desenvolvedor, mas, abrir espaço na agenda que permita ir além de
desenvolver a nova funcionalidade, se preocupando com a qualidade total do
produto, é responsabilidade do líder do projeto. [caption id="attachment_736"
align="aligncenter" width="713" caption="ciclo de desenvolvimento "][![ciclo
de desenvolvimento onde as quantidade de linhas da aplicações crescem
sempre](http://ianntech.com.br/wp-content/uploads/2010/12/ciclo-
dev.png)](http://ianntech.com.br/wp-content/uploads/2010/12/ciclo-
dev.png)[/caption] Ciclos de Desenvolvimento como o acima, que fazem o
software crescer em linhas de código indefinidamente não são a verdade
absoluta, embora parece que essa perspectiva esta presente no futuro de
qualquer software. Existe como fugir desse quadro? Tenho certeza que sim, e
vou discutir algumas coisas simples a se fazer para conseguir isso. A primeira
coisa é, 1 - **PENSE**. Vamos pensar com um trecho de código hipotético,
pequeno mesmo. Lembre-se que todo código usado nesse artigo serve somente para
demonstração.

[![](http://ianntech.com.br/wp-
content/uploads/2010/12/pessoa_class_1.png)](http://ianntech.com.br/wp-
content/uploads/2010/12/pessoa_class_1.png)

Na primeira entrega do projeto toda ver que fosse impressa uma ficha de uma
pessoa, ela seria impressa de uma maneira padrão, sem diferenciar nada para
nenhuma pessoa. Acho que poucos discordariam que essa seria uma das maneiras
de implementar essa ideia.Existem outras tantas melhores, mas essa seria uma
maneria. Software entregue, tudo certo. Cliente satisfeito. Porém, 2 meses
depois ele pede para que homens e mulheres tenham fichar diferentes. O que
fazer? Aqui surgem dois tipos de programadores. Aqueles que vão investir tempo
numa solução definitiva para o problema que surge do raciocínio de que esse
tipo de pedido pode ocorrer novamente e aqueles que vão pensar em carregar um
template diferente dentro do metodo imprimir para cada valor possível no campo
sexo( num mundo normal, somente M=Masculino e F=feminino). Para qual dos dois
lado você se sente mais propenso? Eu vou de opção número 2. Crio um template
novo e em menos de 10 minutos tenho o pedido do cliente atendido.

[![](http://ianntech.com.br/wp-
content/uploads/2010/12/pessoa_class_2.png)](http://ianntech.com.br/wp-
content/uploads/2010/12/pessoa_class_2.png)

Software entregue, tudo certo. Cliente satisfeito. Tudo tranquilo até que 21
dias depois o cliente envia um email dizendo que agora quer adicionar o campo
idade no cadastro de pessoas e também quer imprimir as fichas com formatos
diferenciados para crianças Jovens e Adultos, do sexo masculino e Feminino.
Pronto, agora o desenvolvedor que fez a última modificação vai receber as
criticas todas daquele que pensou na solução mais robusta. Sim, ele vai. Você
mesmo pode ter  criticado (em pensamento ou não) quando eu preferi a opção
mais simples. A chave dessa evolução é baseada em um tipo de raciocínio
simples. ** 2 - Não brinque de adivinhar o futuro. ( overengineer )** Não
tente trabalhar para o “além da imaginação”. Se você não vislumbrar um real
ganho para a aplicação proveniente do código super mega blaster plus fucking
foda que você esta querendo implementar, guarde-o para o futuro, quando ele
será realmente necessário(ou não). Você pode estar certo de que o resultado é
positivo para o projeto, tanto pelo lado comercial, relacionado a prazos,
quanto pelo lado técnico, já que evita que na aplicação existam códigos mais
complexos(que tornam a evolução um desafio maior) antes que eles sejam
realmente necessários. Em outras palavras, não pratique overengineer. Voltando
ao código exemplo, agora temos um problema. O típico problema que a
dificultade de manutenção de uma aplicação aumentar consideravelmente. Quando
o desenvolvedor que pegou essa tarefa para realizar olhar para o código do
método imprimir vai pensar em primeiro lugar que será uma questão de adicionar
mais condições ao if, ou, se ele for limpinho, vai pensar em trocar o if por
um switch ;). Vejamos, como seria.

[![](http://ianntech.com.br/wp-
content/uploads/2010/12/pessoa_class_3.png)](http://ianntech.com.br/wp-
content/uploads/2010/12/pessoa_class_3.png)

E agora temos uma situação onde a complexidade da tarefa de manutenção e a
probabilidade de erro ao fazer uma alteração cresceram muito. Tudo por que a
tarefa era adicionar suporte a um pedido para o cliente. Nesse ponto o código
ainda é administravel, mas duvido que esse modelo de desenvolvimento não
pudesse chegar a cabo de mais de 100 opções de impressão de uma ficha. ** 3 -
Não duplique código** Ainda existe a questão de que esse modelo de decisão
internalizado num método tende a duplicar-se pela aplicação, digamos, quando
houver um método que grava um valor de taxa diferente para cada cliente
baseado nessas mesmas regras. Primeira reação do desenvolvedor poderá ser
qual? copiar e colar. Lógico, o editor esta lá para isso, localizar códigos
duplicados, mas não é muito bom aceitar que duplicar código seja a solução de
um problema. Com o código duplicado o que você tem e uma chance absurda de
alterar algo em um lugar e esquecer do outro e provocar um bug. Vamos tentar
uma abordagem menos insana para o problema que a primeira vista pode parecer
um exagero de código para um problema que uma coleção de if’s resolveria, mas
que traz segurança para a implementação. ** 4 - Estabeleça um plano de Ação
(divida em passos a tarefa)** Primeiro Passo será abstrair o problema da
idade.

[![](http://ianntech.com.br/wp-
content/uploads/2010/12/abstract_pessoa.png)](http://ianntech.com.br/wp-
content/uploads/2010/12/abstract_pessoa.png)

Ao transformar a classe pessoa em abstrata eu informei que essa classe não
mais pode ser instanciada. O metodo is é o método adicionado para lidar com a
idade de forma centralizada, sem repetição de código, sem risco de quebrar a
regra de intervao ],) ( voce lembra dessa notação?). Agora vamos ao proximo
passo, a criação das classes que serão utilizadas para resolver nosso problema
de idade realmente. ** 5 -Trabalhe com Classes que representem palavras do
domínio do problema** ** **

[![](http://ianntech.com.br/wp-
content/uploads/2010/12/pessoas.png)](http://ianntech.com.br/wp-
content/uploads/2010/12/pessoas.png)

Cada uma dessas classes é responsavel por suas caracteristicas. Uma
caracteristica de OO que vi negligenciada em muitos códigos OO com que já tive
contato. Se eu criar uma instancia de Crianca, ela sabe sua faixa etaria, o
mesmo é valido para Jovem e também para adulto. Nesse ponto do código ainda
teriamos que ficar testando as tres classes como abaixo

[![](http://ianntech.com.br/wp-
content/uploads/2010/12/exemplo.png)](http://ianntech.com.br/wp-
content/uploads/2010/12/exemplo.png)

Isso não é muito legal por que o numero de faixas pode aumentar e também pode
ser adicionada novas regras para classificação. Então a melhor estratégia é
usar um Design pattern chamado Strategy(não resisti).

[![](http://ianntech.com.br/wp-
content/uploads/2010/12/pessoa_strategy.png)](http://ianntech.com.br/wp-
content/uploads/2010/12/pessoa_strategy.png)

E voilá, temos agora uma maneira de inverter a tendencia de crescimento de
código que esta sendo apresentada pela forma como as requisições do cliente
estavam sendo atendidas. Fez diferença para o cliente? Não, claro que não! Fez
diferença para a empresa que te contratou? Sim, ela vai gastar menos horas
para implementar novas regras do cliente. O software custa menos no final. E
aqui esta o valor do software. Segundo Martin Fowler, o valor do software se
dá pelo que ele faz hoje e pelo que ele pode fazer no futuro. Na implementação
o valor do software estava diminuindo. Passaria a ser mais dificil lidar com
ele para adicionar novas funcionalidades. Mas dessa maneira, creio que o valor
do software cresceu e deixou espaço para maior crescimento. Mas o problema
esta somente parcialmente resolvido. Um exemplo de uso desse strategy segue
aqui.

[![](http://ianntech.com.br/wp-
content/uploads/2010/12/exemplo.png)](http://ianntech.com.br/wp-
content/uploads/2010/12/exemplo.png)

Se dermos continuidade, cobriremos o problema de decisão do template por conta
também do sexo. Mas acho que já consegui passar a ideia. Revendo as dicas,
fica assim então. **1 - PENSE.** ** **Entender completamente o problema no
qual você vai trabalhar é premissa básica para soluciona-lo completamente(e
não causar outro problema). Não tenha medo de perguntar novamente e novamente
até que tenha entendido algo. Se fizer isso, perguntar sempre, algumas pessoas
vão te chamar de fraco, e outras vão te chamar de detalhista. Preste atenção
no segundo tipo de pessoas, são elas que se tornarão melhores profissionais no
futuro. ** ** **2 - Não brinque de adivinhar o futuro. ( overengineer )** **
**Não importa o quanto você conheça do domínio da aplicação. Somente
implemente aquilo que consegue visualizar como problema de curto e médio
prazo. Se você fizer essa implementação da forma correta não será tarefa
difícil porta-la para um novo modelo quando necessário. ** ** **3 - Não
duplique código** ** **Quer chegar em casa no horário todos os dias? Então não
duplique código, essa é a maneira campeã de gerar bugs de dificil
rastreamento. Você aplica a alteração em uma cópia e esquece de outra ou outra
pessoa faz diferente. São inumeras as maneiras de uma duplicação de código que
parece, inicialmente te ajudar, acabar transformando seu trabalho num inferno.
**4 - Estabeleça um plano de Ação (divida em passos a tarefa)** ** **Já sabe o
que vai fazer? Tem um código funcionando e precisa implementar uma
funcionalidade nova? Divida seu trabalho em passos que mantenham o máximo
possível do tempo a aplicação passando em todos os testes que já existiam
antes (teste durante o desenvolvimento) e os execute pa-u-la-ti-na-men-te. **5
-Trabalhe com Classes que representem palavras do domínio do problema** **
**Parece repetitivo, mas vale dizer que apesar de ser uma dica repetida por
todos, poucas pessoas usam. Se voce tem que trabalhar com uma coleção de
livros e os diferenciar por tipo, talvez como romance, terror, ficção e outros
é muito melhor trabalhar com LivrodeRomance, LivrodeTerror, LivrodeFiccao que
já conhecem suas próprias caracteristicas do que ficar trabalhando com Livro
e uma coleção de setters para cada tipo de propriedade. Objetos Leves levam a
sistemas leves. Espero que gostem. Um Abraço e até o próximo artigo.

