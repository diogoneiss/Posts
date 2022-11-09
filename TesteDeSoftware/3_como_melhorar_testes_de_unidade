
## Testes mais limpos

### Poucos asserts por teste = um único conceito
Acelerar compreensão e entendimento do teste testando apenas um conceito do comportamento

### Escrita declarativa

Teste deve verificar o comportamento do código de produção de maneira declarativa, ou seja, em termos do que ele faz, descritivamente

###  Nomes de teste devem descrever funcionalidades
Eles são a primeira dica para o desenvolvedor do que está sendo testado e devem permanecer assim
Como não vamos invocar as funções de teste, elas podem ter nomes grndes para serem bem descritivas quanto ao que é testado, sendo auto-documentáveis

### Asserts auto explicativos

Incluir mensagem para aparecer em caso de falha, descrevendo o que aconteceu

### Valores auto-descritivos

Colocar os detalhes nos valores dos asserts, como no exemplo de named dates

## Tests smells

### Lógica condicional

Não devemos utilizar estruturas de controle como if's e whiles, já que podem afetar o comportamento do teste e dificultar sua compreensão, já que não sabemos tão bem quando ele entraria nessas estruturas de controle

Podemos ter casos que o teste não execute o if, o que não é desejado, já que deve testar sempre um comportamento determinístico e condicionais tornam o teste imprevisível, dando a possibilidade de não chegar na asserção correta, não testando efetivamente
#### Quando é recomendado?
Eles podem existir no caso de restrição de ambiente, para verificar qual ambiente o teste está rodando, como no caso de Windows ou Mac.

### Gerenciamento de exceções

Quando usamos blocos try/catch criamos condicionais implícitas, de modo que o código não teste tenha uma lógica obscura e potencialmente com bugs. É melhor utilizar estruturas nativas do framework para asserção de lançamento de excessões, de modo que ele falhe o teste caso ela não seja lançada. 

Frequentemente é útil separar os testes em testes que gerem e testes que não geram exceções

### Teste desconhecido

Quando não temos asserts, sempre passando no caso. As vezes é utilizado para garantir que um comportamento específico funciona, como no caso de testes de interface, para ver se a tela é desenhada.

### Teste obscuro

Teste complexo que dificulta o entendimento do que está sendo testado, pouco auto documentável

### Testes copiados

Toleráveis para asserção de funcionamento adequado em edge cases, porém podem ser substituidos por testes parametrizados em vários casos

### Fixture genérica

Ocorre quando uma fixture é criada excessivamente genérica, com atributos não usados pelos métodos de teste e poluindo o ambiente.

Outro problema é a performance, já que o setUp seria chamado antes de todos os métodos de teste. Seria melhor refatorar para vários setUps estáticos diferentes, cada um no escopo de classe, de modo que fossem chamados uma única vez e os testes que precisam das respectivas variáveis estariam na classe que testa.

Um exemplo disso é uma feature complexa que tem múltiplos atributos gerados, com um setUp estático de classe criando a fixture e cada teste verificando se a variável para tal comportamento está como esperado.

### Mystery guest

Quando utilizamos recursos externos, desejavelmente feitos nos testes de integração, em testes de unidade. Seu problema é que torna o teste flaky e lento, sendo melhor usar dublês de teste

### Redundant Print

Não precisamos de prints, já que o tete deve ser auto-verificável.

## Cobertura
A razão Número de comandos rodados pelo teste / total de comandos indica a cobertura de testes

* Cobertura de linhas: Linhas executadas nos testes pelo menos uma vez
* Cobertura de branches: Linhas e branches cobertas, como o caso de condicionais raros. O condicional só entrará na métrica de cobertura se todos os casos acontecerem
* Cobertura de funções: Porcentagem de funções executadas por um teste
* Cobertura de chamadas de funções: quantas linhas de um programa que chamam funções que são exercitadas por testes

Cobertura de branches é sempre mais difícil, já que cobre condicionais.

Cobertura abaixo de 50% é preucupante, com o desejável acima de 78%. A cobertura depende bastante da linguagem, com Python, por exemplo, sendo mais fácil de atingir cobertura alta que linguagens como C++

Sabemos que baixa cobertura implica em ausência de testes, porém alta cobertura não significa testes bons, significa que testes existem, o que pode ser feito facilmente com testes complexos, asserções vazias ou mesmo testes ruins. Cobertura apenas significa que as linhas foram rodadas. Features que mudam frequentemente devem ter cobertura mais alta, garantindo que testes capturem potenciais introduções de bugs

Uma utilidade muito boa de cobertura de testes é saber onde são necessários testes

## Design for testability

Códigos que são fáceis de ser testados implicam em alta coesão e baixo acoplamento, melhorando o projeto de sistema

### Sistemas legado
Para refatorar sistemas legado, podemos usar de regra geral testar o mais externo e refatorar o mais interno, usando testes de aprovação, fazendo refatorações pontuais para deixá-lo mais testável.

O jeito mais compreensível é quebrar métodos complexos em pequenos métodos testáveis, extraindo esses métodos e testando-os

#### Construtor parametrizado

Externalizar o objeto, criá-lo fora da classe e passar o objeto para seus clientes como parâmetro

#### Subclass e method override
Usar herança para retirar comportamentos indesejados do teste

## Test driven development

Escrever teste, falhar, escrever mínima implementação viável, passar teste

Refatorar implementação até o projeto estar satisfatório

Começaremos com um teste falho, já que nenhum dos métodos existe, criaremos as implementações e o retorno trivial para o teste passar, refatorando até a implementação estar satisfatória

Se necessário podemos refatorar o código do teste também, adequando-o ao comportamento sob teste

#### Vantagens

* Recebemos o teste de graça, aumentando cobertura
* Pensando sobre o que é necessário para a implementação da feature e o que ela envolverá, os métodos e seus parâmetros, tipos de retorno, etcs, deixado ele altamente coeso. 
* *Facilita a depuração, já que temos um critério de aceitação do que é esperado e o que foi retornado pelo sistema sob teste. 
* Melhor entendimento do problema, já que você só consegue escrever bons testes se entender a especificação


