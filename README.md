RPOcoin Core clone
=====================================

Clone do repositório do Litecoin, que por sua vez é um clone do Bitcoin

O que é RPOcoin?
----------------

É um clone do Bitcoin personalizado a partir do repositório do litecoin com o propósito de servir como objeto de estudos e material didático em curso específico.

Licença
-------

RPOcoin Core is released under the terms of the MIT license. See [COPYING](COPYING) for more
information or see https://opensource.org/licenses/MIT.

Processo de desenvolvimento
-------------------

O repositório do Litecoin é clonado e modificado. Parte-se do princípio de que as alterações feitas no código do bitcoin quanto a personalização, fica mais vizível no código do litecoin, portanto, as alterações de personalização do RPOcoin são feitas observando os termos "Litecoin", "litecoin" e "LTC". Substituidos por "RPOcoin", "rpocoin" e "RPO" respectivamente em todo o código clonado.

Relevância
-------

Do ponto de vista técnico, não há necessidade alguma de usar qualquer clone do bitcoin para estudar seu código, haja vista que o mesmo possui 3 mecanismos de instalação de full node:

**mainnet:** A rede "de produção" do Bitcoin. Onde o full node se conecta com a rede para transações reais a partir do status atual da blockchain.

**testnet3:** A rede de teste do Bitcoin. Onde o full node se conecta na rede de testes já em andamento, mas sem valor real.

**regtest:** A rede de "teste de regressão" do Bitcoin. Onde a dificuldade de mineração é praticamente 0 e, pode iniciar do 0 com nenhum bloco minerado e nenhum
peer conectado.

Assim, usar o **regtest:** do próprio Bitcoin é suficiente para manipular o sistema, minerar o bloco gênesis e trabalhar com carteiras e demais possibilidades. No entanto, há relevância em personalizar o código para conhecer mais a fundo o sistema e criar uma **mainnet:** do zero para conhecer os fundamentos e mecanismos do Bitcoin mais a fundo.

### Código usado para a personalização

Com o fork feito neste repositório, foi feito o clone no computador. A personalização se deu com revisão e commits feitos pasta a pasta nos seguintes diretórios:
* /src 
* /test
* /share
* /doc
* /depends
* /contrib
* /build_msv 
* /build-aux

Com o seguinte código é possível procurar e modificar automaticamente. Foram trocados os nomes relacionados a Litecoin para RPOcoin conform segue:

```
$ grep -rl 'Litecoin' ./ | xargs sed -i 's/Litecoin/RPOcoin/g'
$ grep -rl 'litecoin' ./ | xargs sed -i 's/litecoin/rpocoin/g'
$ grep -rl 'LTC' ./ | xargs sed -i 's/LTC/RPO/g'

```

Foram feitas alterações mais cuidadosas manualmente, também nos seguinte arquivos:

* Makefile.am
* configure.ac

* .travis/test_04_install.sh
* .travis/test_05_before_script.sh
* .travis/test_06_script_a.sh
* .travis/test_06_script_b.sh

# instalação

Uma vez feitas tais alterações, no diretório do RPOcoin foi configurado o db da seguinte forma:

```
$ wget http://download.oracle.com/berkeley-db/db-4.8.30.NC.tar.gz
$ sha256sum db-4.8.30.NC.tar.gz
# o último comando deve ter gerado o *hash* 12edc0df75bf9abd7f82f821795bcee50f42cb2e5f76a6a281b85732798364ef
$ tar -xvf db-4.8.30.NC.tar.gz
$ cd db-4.8.30.NC/build_unix
$ mkdir -p build
$ BDB_PREFIX=$(pwd)/build
$ ../dist/configure --disable-shared --enable-cxx --with-pic --prefix=$BDB_PREFIX
$ make install
```
Com o erro detectado após $ make install, foi feito a seguinte correção:
no diretório  /db-4.8.30.NC/dbinc/
```
$ nano atomic.h.
```

Line 147, substituir __atomic_compare_exchange((p), (o), (n)) para __atomic_compare_exchange_db((p), (o), (n))

Line 179, substituir __atomic_compare_exchange( para __atomic_compare_exchange_db(

# Compilar

dentro do diretório raíz do RPOcoin:

```
$ ./autogen.sh
$ ./configure LDFLAGS="-L${BDB_PREFIX}/lib/" CPPFLAGS="-I${BDB_PREFIX}/include/" --with-gui
$ make
```
# Testar

No diretório /src:
```
$ ./rpocoin-cli --version
$ ./rpocoind --version
```
