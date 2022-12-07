# Uso de mocks/doubles em testes de software

## Motivação para uso

Muitas vezes temos códigos de unidade que dependem de serviços externos ou instanciação de objetos complexos, como o caso de uma API de busca.

Para deixar o teste determinístico, criaremos uma implementação que engana a classe, como o caso que entradas mapeiem saídas para simular a busca.

Ao usar o mock, aproveitarmeos polimorfismo para instanciar o objeto complexo e usar uma entrada conhecida para verificamos se os comportamentos esperados acontecem, sem necessitar efetivamente chamar a api externa

Se quisermos testar a lógica de formatar o retorno da busca, o mock é valioso para o teste, já que possibilita desacoplar a formatação da busca em api, tornando o teste determinístico.

## O que são doubles

Mocks são utilizados como sinônimos, embora sejam apenas um tipo de double, que funciona sendo um dublê do objeto real, permitindo verificações de comportamento e estado.

## Quando não usar doubles

Devemos tomar cuidado, já que quanto mais doubles existirem no teste menos "realista" ele será, já que depende de cada vez menos coisas, significando menos a aprovação no teste

Outro contexto é que doubles exigem conhecimento da implementação interna, acoplando o método sob teste as implementações internas do SUT, ou seja, se um dia refatorarmos o código para não fazer uma chamada com parâmetros específicos, o teste quebrará, algo indesejável, já que queremos minimizar o acoplamento SUT/teste, exigindo cautela ao decidir que doubles criar.

## Tipos de Doubles

### Dummy

Apenas preenche parâmetros, não sendo usado no método. Geralmente serve para injeções de dependências complexas.

Um exemplo de implementação seria criar uma classe que herda todos os atributos do objeto e implementa métodos e atributos do objeto dummy, porém com lançamento de excessões caso sejam executados, permitindo a instanciação correta

### Stub / Esboço de método

Complementa o dummy permitindo a execução, dando respostas programáveis ao double, como chamadas de função e seus parâmetros: podemos colocar para toda vez que um parâmetro for passado, retornar True, e quando um parâmetro específico for passado, como o número 2, retornar False.

### Spy

Capturam informações acerca do seu contexto de uso, como registro de chamadas e suas contagens, podendo substituir alguns métodos específicos do objeto real (stub) ou usar os métodos reais, apenas espionando-os

### Mock

São mais complexos que o spy, sendo pré programados e tendo expectativas do que devem receber, espionando os casos de uso em um objeto fictício, verificando comportamento
(consultar slides pra ter mais ctz)

### Fake

Objetos com implementações reais, porém inadequados para produção, como o caso de utilizar um sqlite local invés do banco de dados real, permitindo consultas e inserções, permitindo simular o uso de um banco de dados real