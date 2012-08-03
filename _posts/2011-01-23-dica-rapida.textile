Dica Rápida PHP MacPort
=======================
Published: 2011-01-23 16:45:30

Se você usa Mac e costuma atualizar os seus software usando o Ports tem duas
coisas que você precisa ficar ligado: 1 - O php 5.3.5 já esta ao alcance de um
port update 2 - Se o seu driver de PDO para Mysql travar e o log tiver a
mensagem "error for object 0x1019c84c8: pointer being freed was not allocated"
basta voce remover o driver (port uninstall php-mysql) e instalar novamente
(por install php-mysql). Isso acontece por que o driver não esta sendo
atualizado automaticamente.

