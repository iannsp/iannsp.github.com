Como eu precisei ver Testes
===========================
Published: 2012-07-17 07:02:36

Alguns fatos: Eu invisto(alguns dizem que eu perco) tempo compreendendo alguma
coisa pela qual surja interesse(FATO 1) Outro fato é que a algum tempo venho
refletindo sobre testes e também, aliás, especialmente, sobre Test Driven
Development(TDD)(FATO 2). O ultimo fato, e de menor importancia é que este
post é longo. Logo, se você reclama de textos longos, não acho que valha a
pena dedicar seu tempo a este. vamos ao que interessa: Conversando com o Diogo
Baeder, Ney Basilio e o Rafael Valeira eu acabei encontrando, juntando uma
peça aqui e acolá, uma maneira realistica, não ligada diretamente a software,
mas sim a vida, na qual apoiar uma escolha por TDD. Eu perguntava sobre as
dificuldades que tenho sobre utilizar testes, tais como racionalizar o por que
dos mocks, que criamos e mantemos em paralelo a implementação original para
podermos isolar completamente uma teste de suas dependencias ou também a
diferença entre usar fixtures em um teste e "mockar" quando uma das resposta
me levou a lembrar, não sei porque, da seguinte frase: "A gente devia ter duas
vidas, uma pra treinar e outra pra viver." E é dai que cheguei a sintese de
como resolvi encarar testes e que pretendo apresentar aqui:

> "Um software deve ser desenvolvido para sobreviver em um ambiente
previamente definido."

[![](http://ianntech.com.br/wp-
content/uploads/2012/07/4603259_1.jpg)](http://ianntech.com.br/wp-
content/uploads/2012/07/4603259_1.jpg) Se definirmos o dominio de um problema
como um mundo e o software como um ser que deve viver naquele mundo, ele, o
software, pode ser colocado pra treinar em um mundo simulado(testes) e ir
melhorando, antes de passar a realmente viver(live). O mundo real esta lá, com
efeitos imprevisíveis. Os usuários (com seu julgamento) estão lá. A latência
esta lá. A falha em um serviço esta lá. Num espaço onde os efeitos são reais.
E se pudermos, antes de estar lá, praticar como fazemos em um treinando ou
como o faz um jovem aprendiz ou um estudante, tanto melhor. Mas para isso
precisamos presupor que um software tem certas caracteristicas. **1a** - Um
software, como uma criança, pode, apesar de seus pais o acharem perfeitos,
sofrer com o ambiente em que vive e cresce e ser influenciado pelas
companhias. Crescer na companhia de bons softwares/hardwares é muito saudável
e o contrário pode fazer com que se pareça errar _por sua própria natureza_,
mas na realidade é só um "bubbles" de coisas que acontecem no ambiente.
Podemos definir uma lei baseada no cliche que é "**dize-me com quem andas e te
direi quem és**". **2a -** é que um software aprende sempre, mesmo que não
tenha sido escrito para isso. Uma regra escrita hoje se prova obsoleta amanhã
por que agora existe um dado que permite mais acurácia. O programador vai
alterar aquela regra e, por reflexo, podemos ver num sistema de versionamento
de arquivos, toda a evolução em termos <del>psicológicos </del>algoritmicos e
<del>físicos</del> quantidade de codigo(linhas apagadas, acrescidas e
alteradas) e todo o ganho de novas capacidades e aperfeiçoamento das
habilidades já existentes. Podemos definir essa como uma segunda lei, e
utilizar aqui a frase **"interação e tempo geram conhecimento"**. Precisamos
presupor essas duas caracteristicas para entender que o melhor lugar para um
software aprender a lidar com "as coisas da vida"_ é o mesmo melhor lugar de
quem esta em processo de aprendizado_. Esse lugar é um _ambiente controlado_,
_sem as penalidades reais_, onde as situações que precisam ser aprendidas
possam _ser reproduzidas e seus resultadados analisadas_, para que _se saiba o
que deve ser aperfeiçoado_.

> Esse lugar tem nome, ele é chamado de "ambiente de testes".O equivalente
para um software do que é a escola para os humanos.

Construir um lugar assim e utiliza-lo, tem um custo, assim como construir um
mundo qualquer([consultar os ratos sobre
isso](http://pt.wikipedia.org/wiki/A_Pergunta_Fundamental)), mas é um custo
infinitamente menor que o custo de "errar na realidade", alias, se pegarmos o
espírito dos seriados de sucesso atual, essa diferença pode ser explicada como
a diferença de emoção em passar walking dead inteiro atirando em alvos de feno
imóveis, ou atirar diretamente em zumbis. Criar um <del>mundo</del> ambiente
de testes para que os<del> seres vivos</del> softwares possam
<del>praticar</del> ser testados é a melhor maneira de garantir que tenham
<del>uma vida</del> um deploy no live seguro e tranquilo sem que seu criador
seja apedrejado por heresia. A conclusão disso foi que ao escrever testes, o
ato de_ escreve-los antes é primordial para o relacionamento programador/teste
ser positivo_(e não simplemente _boring_) e que ao escrever um teste você esta
poupando uma vida(uma peça de sofware deixa de morrer). Existe uma diferença
tênue entre escrever um teste para uma peça de software e escrever uma peça de
software atraves de um teste. Se softwarelogia existisse, e essa tivesse uma
missão como a da antropologia, mas voltada a software, teriamos: No primeiro
caso, você esta lidando com um ser pronto, cuja única parte visivel é a
externa(interface) e cujo conteudo, se voce quiser conhecer, terá de
dissecar(uma tarefa complexa, e o ser pode morrer no processo). No segundo,
não existe ser, mas você esta dizendo que, para que ele exista, deve atender a
certas regras(como um peixe, que obedece a regra de viver grande parte do
tempo em meio aquático) e você não precisara disseca-lo para saber que ele
cumpre essa regra, afinal, de inexistente, você, o criador, o  fará existente
e fato, ele só conseguira existir se atender os requisitos do mundo que você
projetou para valida-lo(fatalista não?!). Outra coisa muito importante é:
_Ninguem consegue escrever um teste para uma peça de software que escreveu sem
cair na armadilha de concluir que não vai conseguir escrever um teste para um
problema que não tenha pensando e tratado no código por que se não conseguiu
imaginar o problema na implementação, também não vai imagina-lo no teste._
Para quem curte quadrinhos, e leu "[A morte do super-
man](http://pt.wikipedia.org/wiki/A_Morte_do_Superman)" a diferença do que foi
definido acima é algo como se o Bertron tivesse criado o
[Apocalipse](http://pt.wikipedia.org/wiki/Apocalipse_%28DC_Comics%29) em
laboratório, de acordo com o que imagina ser o certo, e colocasse ele pra
matar o super-homem(provavelmente o Apocalipse iria morrer) e criar o mesmo
Apocalipse fazendo ele sobreviver ao mesmo ambiente que o Super-Homem.
Praticamente, nesse segundo caso, além do benefício de evolução incremental e
positiva, ele ainda ganhou um parametro com o profiling todo publicado contra
o qual comparar a sua criação(a saber, o próprio super-homem). O ambiente de
testes, fica assim caracterizado como a peça mais importante dentro do
processo de desenvolvimento de software, como é a escola dentro da formação de
um ser-humano. É nele que um software vai ser confrontado com situações reais,
com penalidades controladas, como um aluno que faz uma prova de aritmética e
erra o troco de uma compra de 10 reais onde deu uma nota de 100. Ele pode
dizer na escola que o troco é de nove reais e, mesmo assim, não perder
dinheiro, mas na vida real, ele teria um prejuízo de?!(responda ai) _Assim
como na escola, o mundo de teste apresenta um  novo desafio a medida que julga
que o software esta preparado para ele._ Você não cria todos os testes que
caracterizam o "mundo de provas" de uma vez. Faz isso de maneira incremental,
na medida em que vai assistindo a peça de software ir vencendo os desafios
anteriores. Esse processo incremental permite que se saiba o que errou, onde
errou e o que melhorar. Assim como uma prova baseada em um bimestre de aulas e
não em um ano inteiro. Corrigir os erros de um bimestre é um processo bem
menos doloroso do que corrigir os de um ano. Assim como corrigir um algoritmo
de 7 linhas é mais compreensivel do que corrigir um software de 100 linhas.
Foi assim que tive que pensar em testes para me sentir a vontade enquanto os
uso. Recapitulando: 1 - Dize-me com quem andas e te direi quem és. _Um
software deve ser testado isoladamente para que seu comportamento não seja
influenciado pelos erros dos outros._ 2 - interação e tempo geram
conhecimento. _O processo de teste deve ser incremental e seguir uma linha de
tempo pré-estabelecida. Isso adiciona conhecimento e permite sua recuperação,
não importa se seu software utilize algorítmos mutáveis ou não. O conhecimento
se acumula no servidor de controle de versão de código que você esta
utilizando._ 3 - Ambiente de teste deve ser levado tão a sério para o software
quanto o é a escola para a educação de seres humanos. _O processo de teste de
um software permite uma co-relação com o processo de aprendizado de uma
criança._ 4 - Crie o ambiente de teste antes do software a ser testado.
_Ninguem que projeta um software deixa de analisar questões que estejam ao seu
alcance(falo de pessoas justas). Isso torna impossível num momento não ver um
defeito e no outro vê-lo. Na realidade, quando você passa a ver um erro depois
do software criado é por que esta sendo penalizado por ele com o custo mais
caro possível, em produção. Assim como uma criança que deixa a escola e não é
mais criança é penalizada pela vida quando percebe que não aprendeu algo
quando devia te-lo feito._ &nbsp_place_holder; &nbsp_place_holder;
&nbsp_place_holder;

