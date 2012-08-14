G2 - Organizando o desenvolvimento com github e google calendar
===============================================================
Published: 2011-11-04 17:19:05

No momento coordeno o trabalho de um time de desenvolvimento pequeno de 3
pessoas(incluindo a mim) e dentro dessa característica do meu trabalho busquei
ferramentas que atendessem a necessidade de gerenciamento do time, que, apesar
de pequeno, precisa organizar e sincronizar uma série de atividades e que me
fizesse ganhar o máximo de tempo, me poupando de algumas tarefas de
gerenciamento. Com isso em mente, comecei a olhar para as ferramentas que já
tinha em mãos e cheguei as duas que destaquei no título. O google calendar e o
github, que me proporcionaram tudo que preciso para organizar o trabalho,
tanto para nós, membros da equipe de desenvolvimento, quanto para a gerencia e
diretoria e me ajudaram a não adicionar mais nenhum OrganizaWare na vida do
pessoal da equipe. **O custo** ****O primeiro detalhe dessa decisão foi que
ela não impactou em nenhum custo adicional para a empresa. Nós já tinhamos a
cultura do uso de
[DRCS](http://en.wikipedia.org/wiki/Distributed_revision_control) e também,
como a maioria dos mortais, também temos no time pessoas que tem uma conta do
google e com ela, acesso ao google calendar. Em empresas que não tem uma conta
corporativa do github, é adicionado no centro de custo do setor um valor
pequeno(varia de 25 a 200 dolares mensais) e sua aquisição traz consigo uma
série de reflexos positivos para os times de desenvolvimento, que acabam
adquirindo uma série de saudáveis habitos, que fogem ao escopo desse artigo. A
outra parte do sistema de organização é o google Calendar, que não tem custo
algum para contas no domínio google, mas podem ter custo se forem em domínios
corporativos, mas novamente, seus custos são pequenos(de 4 a 5 dólares
mensais). Abaixo segue a maneira como utilizo essas duas fantásticas
ferramentas. **[![Logo do github](http://ianntech.com.br/wp-
content/uploads/2011/11/github_logo-copy-300x93.png)](http://ianntech.com.br
/wp-content/uploads/2011/11/github_logo-copy.png) ** &nbsp_place_holder;
&nbsp_place_holder; &nbsp_place_holder; 1- Trabalhei com o time a questão de
que os **commits devem ser pequenos**, com porcões de código com
caracteristicas que levassem a não usar o "and" no message, com efeito:
"Adicão da funcionalidade X e bug fix Y" virou dois commits: "Adição da
funcionalidade X" "Bug fix Y" Parecem claros os benefícios, **mas é sempre bom
conversar sobre algo que se espera do time**, ao invés de somente presupor que
eles já sabem o que se espera. 2 - **Dividimos o software em suas partes
componentes **e criamos um repositório para cada parte, ao invés de manter
todo o código em somente um repositório e assim pudemos administrar melhor não
só o código como a demanda por novas funcionalidades por efeito da não
duplicação do código em outros projetos O reflexo negativo disso é que durante
o desenvolvimento e deploy é necessário estar atento a todos os repositórios.
Essa questão foi facilmente contornada com o uso do wiki, onde foi descrito o
processo, que **apesar de simples, fica muito mais fácil de reproduzir se é
documento**. 3 - Outra questão é que o git – e o github afinal – permite a
organização, então fizemos uso dessa capacidade utilizando os milestones, os
labels e a função de assign. Assim, cada milestone marca uma "version", uma
"major" e "minor" e são adicionadas as issues que o compõem. Novamente, essa é
outra coisa que, apesar de estar disponível, vejo sendo pouco usada. As issues
são as tarefas a serem realizadas e cada uma delas é marcada com as labels que
identificam o tipo de tarefa como
"frontend","backend","api","bugfix","pesquisa","migration". A lista de issue
permite visualizar as tarefas pelo seu tipo(label), dentro de um
milestone(entrega) Uma vez calculada a carga de cada milestone, é fechada uma
data de entrega e anotada no github. Para algumas das tarefas, devido a suas
caracteristicas e em consenso com o time, nós já fazemos assign para algum
membro do time, senão, no momento em que o programador assume a tarefa, ou
seja, começa a desenvolve-la, ele a marca para ele com o mesmo botão de
assign. Utilizando essas anotações fica bem facil saber se estamos dentro do
prazo, por exemplo, basta visualizar os milestones e ver a quantas anda o
progresso através do gráfico de barra que mostra a evolução das issues. 4 -
**Não existe evolução sem mensuração seguida de análise e um processo de
melhoria** e esses passos envolvem estatísticas que o github
apresenta(languages, impact, punchcard, traffic e clones) e dentre elas as
três primeiras são as que mais utilizo. **Languages **Com a métrica de
_languages_, é possível analisar que uma linguagem, por exemplo, javascript,
tem crescido dentro do projeto, o que pode indicar que esta sendo utilizada
cada vez mais pois estão sendo cobertas necessidades de user interface ou que
alguns problemas de lógica do domínio estão sendo entregues para esta
linguagem ao invés de serem resolvidos no server-side. Ou ainda, indicam um
momentum do projeto, talvez pelo fato de que, estando maduro o backend, o
client-side se tornou o foco dos esforços ligados ao avanço do software.
**Impact **O gráfico de _impact_ permite visualizar como se distribuem os
commits entre os membros do time e também indica quanto código foi adicionado
e apagado. Eu particularmente, desconfio quando o panorama geral mostra que
muito mais código esta sendo adicionado do que apagado. No geral, aplicações
saudáveis evoluem e evoluir não significa essencialmente ganharem mais e mais
linhas de código, significa refactoring e refactoring apaga e adiciona linhas.
Experiencias antigas me indicam que quando o perfil dos commits apresenta
poucas linhas apagadas com relação a linhas adicionas o time pode estar sob
muita pressão e isso tem levado a atender a demanda com pouco foco, talvez, na
qualidade da entrega. **Punchimpact **E o último gráfico que quero apresentar,
o _punchimpact_, que apresenta a atividade de commit dentro do período de uma
semana. Com ele fica fácil perceber que na sexta-feira acontece pouca coisa
por exemplo, talvez reflexo da tensão da responsabilidade (quem é louco de
fazer commits na sexta-feira?) ou até que a parte do dia em que ocorrem mais
commits é a parte da manhã... um provável indicador de que a cafeteira esta
quebrada. O punchimpact é um ótimo argumento em uma reunião para lançar uma
discussão saudável sobre dispersão e foco, ou youtube X textmate.
**[![](http://ianntech.com.br/wp-content/uploads/2011/11/Logo_Google-
Calendar.png)](http://ianntech.com.br/wp-content/uploads/2011/11/Logo_Google-
Calendar.png) ** O time se reune ao menos uma vez ao dia, as 11:40 e temos
vinte minutos para discutir o que ocorreu no dia e os planos do dia. O
importante é que colocando a reunião nesse horário ocorre mais foco, por que
quanto mais dispersão, mas longe o almoço fica ;) Brincadeiras a parte, este é
um horario escolhido. Nele não marcamos nenhum compromisso e normalmente
estamos todos na empresa. Isso esta lá, agendado no google calendar e com
convite e lembrete para todos. Outra coisa é as issues são lançadas também no
Calendar no formato _([id da issue]) Titulo_ e com a cor amarela e assim que é
finaliza, trocamos a cor para verde. Isso permite que outros times e a
gerencia e diretoria saibam o que esta sendo feito naquele momento e
desenvolvam a ideia de tempo de cada tipo de tarefa através da observação das
anotações disso no google Calendar. No geral, todos os eventos são lançados e
compartilhados — até mesmo as demonstrações do software, os testes e todo o
mais que faz parte do desenvolvimento. &nbsp_place_holder; **Conclusão** Essas
duas ferramentas têm ajudado o time a trazer resultados positivos para a
empresa, sempre mantendo foco na qualidade e nos prazos. &nbsp_place_holder;

