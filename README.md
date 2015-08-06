PHPTestFest
===========

##Começando

Clone o repositório e inicie os submódulos

```bash
$ git clone https://github.com/PHPTestFestBrasil/PHPTestFest.git
$ git submodule init
$ git submodule update
```

##Requisitos
 - [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
 - [VirtualBox 5.0 Oracle VM VirtualBox Extension Pack](http://download.virtualbox.org/virtualbox/5.0.0/Oracle_VM_VirtualBox_Extension_Pack-5.0.0-101573.vbox-extpack)
 - [Vagrant](http://www.vagrantup.com/downloads.html)

Inicie a máquina virtual com o Vagrant

```bash
$ vagrant up
$ vagrant ssh
```

Compile o PHP com os testes

```bash
$ cd php-src
$ ./buildconf
$ ./configure --with-curl --with-gd --with-mhash --with-pdo-mysql --enable-soap --with-openssl --with-xsl --enable-bcmath --with-zlib --enable-sysvsem --with-readline --enable-gcov --enable-phar --enable-mbstring --enable-intl
$ make
$ make test
```

No fim, responder com Y para mandar os relatórios

##Gerando LCOV code coverage report

Siga os próximos passos para gerar um relatório de cobertura de código como o 
abaixo:

![](lcov_report.png)

Rode os seguintes comandos:

```bash
$ ./configure --enable-gcov # configura o php habilitando essa biblioteca 
$ make
```

Para gerar um relatório de cobertura de um teste, é necessário executar o comando

```bash
$ make lcov TESTS=teste/a/ser/executado  ; xdg-open lcov_html/index.html
```

O relatório em HTML fica disponível em lcov_html/index.html. Assim, é só comparar
o seu relatório de cobertura com o [relatório do PHP QA](http://gcov.php.net/PHP_HEAD/lcov_html/index.php)
para ver se o seu teste testou algo que não era testado antes.

##Slides

 - [PHPT - Ivan Rosolen (PHPSP)](http://pt.slideshare.net/ivanrosolen/phpt-13829359)
 - [Escrevendo testes com PHPT e contribuindo com o PHP - Rafael Dohms](http://blog.doh.ms/2009/08/19/escrevendo-testes-com-phpt/?lang=pt-br)
 - [PHPSP TestFest 2010 - Rafael Dohms](http://pt.slideshare.net/rdohms/phpsp-testfest-2010)
 
Fontes para geração desse repositório:

 - [https://gist.github.com/rogeriopradoj/68f4372483814cba62d5](https://gist.github.com/rogeriopradoj/68f4372483814cba62d5)
 - [https://github.com/mauriciovieira/PHPTestFest](https://github.com/mauriciovieira/PHPTestFest)

