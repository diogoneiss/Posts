# Como são bons testes unitários

O primeiro passo é entender quando escrever testes. Devemos escrever testes _antes_ de finalizar todo o código, aproveitando dos benefícios que projetar testes garentem ao projeto.

Caso utilize Test-Driven-Development, ou TDD, os testes serão escritos antes de desenvolver a funcionalidade, vendo a falha no teste e programando para que essa falha se torne um teste de sucesso. Senão, escreva o teste após desenvolver alguma unidade de código independente.

Uma dica útil é criar testes quando bugs forem reportados, garantindo que uma vez resolvido o problema não volte.

## Estrutura de um teste

Comumente os testes são escritos em três etapas:

1. Organização / Arrange: configurações e atribuições necessárias para contextualizar o código, como inicializar objetos e criar variáveis.
2. Ação / Act: execução do que quer ser testado com o devido contexto, geralmente a função específica
3. Validação / Assert: Verificar se o resultado obtido confere com o esperado, aprovando ou falhando o teste de acordo.

Fixtures são amplamente utilizadas e representam o ambiente usado para o teste, podendo ser implementadas como funções, rodadas antes e depois do teste a critério do programador, com ciclo de vida específico.

É também conhecido como Given-When-then/Dado-Quando-Então, uma abordagem mais orientada a comportamentos, e Setup-Exercise-Verify-Teardown / Configuração-Execução/Verificação/Desmanche, modelo de 4 fases para testes mais focados no uso de funções de contextualização (fixtures) e seu ciclo de vida.

## setUp e tearDown

A metodologia Setup-Exercise-Verify-Teardown exemplifica bem esses conceitos, com todo teste iniciando com uma configuração inicial e, após todas as asserções, a destruição do teste. Esses métodos especiais implementam isso de acordo com a necessidade de ciclo de vida da fixture, ou seja, é possível criar um setUp único para toda a suite de testes, um setUp para a classe com todos os testes, um setUp a ser rodado antes de toda função (o padrão).

## 1ª prática: teste através de APIs públicas

Testes devem simular o uso pelo usuário, de maneira análoga ao seu uso em sistemas. O usuário final não utilizará métodos internos e detalhes de implementação, apenas APIs de alto nivel.

Por exemplo, ao utilizar a função shape do numpy em python, pouco importa como ela foi feita, apenas que é esperado receber o shape do objeto passado para a função.

API's publicas tem como característica a ocultação da implementação, que fica a cargo da biblioteca/framework, e a consistêmcia, já que esses métodos raramente são alterados e, quando são, existem vários avisos de descontinuação antes dela ser de fato removida. Se testássemos apis privadas teríamos testes frágeis, já que mudanças internas poderiam quebrar os testes e não queremos ter que modificá-los.

É desejado que o teste seja o mais próximo possível do caso de uso real, atendando-se para o contrato esperado de entrada e saída

## 2ª prática: testes estáveis

Queremos que o teste seja escrito e alterado somente ao modificar o requisito específico sob teste, ou seja: se fizermos um teste de carrinho de compras, só devemos ter que alterar esse teste ao fazer uma mudança drástica nos requisitos funcionais do carrinho, de modo que isso modifique o comportamento esperado do teste.

Quando testes atuais não deveriam ser afetados

* Se refatorarmos código, ele deve ser testado frente aos testes atuais, garantindo que nada foi quebrado. No caso de quebrarem com refatoração, vale verificar se ele foi bem escrito e segue as melhoras práticas ou se algum erro foi feito.

* Se novas features forem adicionadas, novos testes para a feature devem ser escrito e os testes atuais devem ser matidos: caso os testes atuais sejam afetados é um forte indício de alto acoplamento no projeto de sistema ou de testes ruins.

* Se bugs forem corrigidos, testes devem ser feitos para garantir a correção, já que a existência do bug implica na ausência de um teste para tal caso. Não deve impactar os testes atuais: caso bugs afetem o código atual é um indício que o bug não foi corrigido, apenas propagado

Quando testes atuais devem ser alterados

* Se comportamento for mudado, podemos sim alterar testes, já que a premissa de asserção agora é diferente. 

## 3ª prática: Testar comportamentos

Devemos focar no teste de comportamento esperado, não na cardinalidade 1:1 entre testes e métodos. Tal prática promove acoplamento, uma vez que toda modificação nos métodos obriga uma modificação nos respectivos testes.

O teste deve focar no comportamento esperado. Invés de testar se para um caso específico uma mensagem é escrita na tela, criamos um teste que, para dado contexto, uma mensagem deve aparecer na tela, evitando que o teste "emule" o método sob teste. O comportamento dá o entendimento do que é esperado para o conjunto de entradas.

O mapeamento então, invés de 1:1, é many-to-many, de modo que os testes validem a interação de múltiplos métodos e seus vários comportamentos, criando testes específicos e estáveis.
