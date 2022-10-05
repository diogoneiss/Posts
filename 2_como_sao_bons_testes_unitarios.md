# Como são bons testes unitários

O primeiro passo é entender quando escrever testes. Devemos escrever testes _antes_ de finalizar todo o código, aproveitando dos benefícios que projetar testes garentem ao projeto.

Caso utilize Test-Driven-Development, ou TDD, os testes serão escritos antes de desenvolver a funcionalidade, vendo a falha no teste e programando para que essa falha se torne um teste de sucesso. Senão, escreva o teste após desenvolver alguma unidade de código independente.

Uma dica útil é criar testes quando bugs forem reportados, garantindo que uma vez resolvido o problema não volte.

## Estrutura de um teste

Comumente os testes são escritos em três etapas:

1. Organização / Arrange: configurações e atribuições necessárias para contextualizar o código, como inicializar objetos e criar variáveis.
2. Ação / Act: execução do que quer ser testado com o devido contexto, geralmente a função específica
3. Validação / Assert: Verificar se o resultado obtido confere com o esperado, aprovando ou falhando o teste de acordo.

É também conhecido como Given-When-then/Dado-Quando-Então, uma abordagem mais orientada a comportamentos, e Setup-Exercise-Verify-Teardown / Configuração-Execução/Verificação/Desmanche, modelo de 4 fases para testes mais focados no uso de funções de contextualização (fixtures) e seu ciclo de vida.

## setUp e tearDown

A metodologia Setup-Exercise-Verify-Teardown exemplifica bem esses conceitos, com todo teste iniciando com uma configuração inicial e, após todas as asserções, a destruição do teste. Esses métodos especiais implementam isso e 