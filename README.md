RPOcoin Core clone
=====================================

Clone do repositório do RPOcoin, que por sua vez é um clone do Bitcoin

O que é RPOcoin?
----------------

É um clone do Bitcoin personalizado a partir do repositório do RPOcoin com o propósito de servir como objeto de estudos e material didático em curso específico.

Licença
-------

RPOcoin Core is released under the terms of the MIT license. See [COPYING](COPYING) for more
information or see https://opensource.org/licenses/MIT.

Processo de desenvolvimento
-------------------

O repositório do RPOcoin é clonado e modificado. Parte-se do princípio de que as alterações feitas no código do bitcoin quanto a personalização, fica mais vizível no código do RPOcoin, portanto, as alterações de personalização do RPOcoin são feitas observando os termos "RPOcoin", "litecoin" e "LTC". Substituidos por "RPOcoin", "rpocoin" e "RPO" respectivamente em todo o código clonado.

Relevância
-------

Do ponto de vista técnico, não há necessidade alguma de usar qualquer clone do bitcoin para estudar seu código, haja vista que o mesmo possui 3 mecanismos de instalação de full node:

**mainnet:** A rede "de produção" do Bitcoin. Onde o full node se conecta com a rede para transações reais a partir do status atual da blockchain.

**testnet3:** A rede de teste do Bitcoin. Onde o full node se conecta na rede de testes já em andamento, mas sem valor real.

**regtest:** A rede de "teste de regressão" do Bitcoin. Onde a dificuldade de mineração é praticamente 0 e, pode iniciar do 0 com nenhum bloco minerado e nenhum
peer conectado.

Assim, usar o **regtest:** do próprio Bitcoin é suficiente para manipular o sistema, minerar o bloco gênesis e trabalhar com carteiras e demais possibilidades. No entanto, há relevância em personalizar o código para conhecer mais a fundo o sistema e criar uma **mainnet:** do zero para conhecer os fundamentos e mecanismos do Bitcoin mais a fundo.

### Código usado para a personalização

a ser inserido
