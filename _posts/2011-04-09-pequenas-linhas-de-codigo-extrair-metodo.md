pequenas linhas de código - extrair método
==========================================
Published: 2011-04-09 18:30:41

Para um programador preocupado com a qualidade do código existe um hábito que
é o de olhar novamente para o código assim que ele esta pronto. Queria pensar
aqui um pouco sobre o que é estar pronto, mas resolvi reduzir o "pronto" para
dois tipos.

  1. Pronto, já fiz funcionar.
  2. Pronto, esta funcionando da melhor maneira que posso imaginar no momento (sempre há um "re-olhar" para o código, eternamente).
O exemplo abaixo é bem curto. Uma classe chamada mensagem que contem somente
seu construtor e um método que realiza duas tarefas, a de receber o texto da
mensagem e gravar a mensagem no sistema SGDB. Esse é o exemplo de pronto do
tipo 1.  Bem, o código funciona, provavelmente atende a necessidade do
documento de requisição, mas temos algumas coisas que podem ser melhoradas,
então vamos levar este código para o tipo de pronto 2.  Agora temos um código
que considero melhor que o anterior, por pequenas coisas, mas acho. A
principal coisa é que cada método da classe agora tem uma única
responsabilidade. Isso vai facilitar o tratamento de erro, a montagem de
algoritmos complexos em que um objeto dessa classe esteja envolvido e reduz o
uso de documentação inútil redundante. Por inútil entenda que agora você não
vai precisar dizer o que um método faz. O nome do método já esta dizendo isso
e você pode confiar nisso. Se voce reparar no método setMensagemAndSave, vai
ver que ele ficou mais claro, mais fácil de ler (se achar que o exemplo não
demonstra isso, faça um esforço e imagine o mesmo exercício sendo praticado
num método com um algoritmo complexo com umas 20 responsabilidades envolvidas
e programadas diretamente ali, na função. O nome desse pequeno **refactoring
**é _extrair método_ e é um dos apresentados no livro[Refatoração![[bb]](http
://boo-box.com/bbli)](http://sledge.boo-box.com/list/page/UmVmYXRvcmElRTclRTNv
XyMjX2Jhcl8jI190YWdnaW5nLXRvb2wtd3BfIyNfMzYwNDYy-68), do [Martin
Fowler![[bb]](http://boo-box.com/bbli)](http://sledge.boo-box.com/list/page/TW
FydGluK0Zvd2xlcl8jI19iYXJfIyNfdGFnZ2luZy10b29sLXdwXyMjXzM2MDQ2Mg==-68) e eu
acho importante esse tipo de operação. Como uma visão global, vale lembra que
agora você pode atribuir uma nova mensagem e esperar para gravar em outro
momento, que pode chegar ou não e que o método publico e publicado não teve
seu algoritmo alterado, nem sumiu, nem nada desse tipo. É isso ai, eu avisei
que seriam....

> Pequenas linhas de código.

