# Por que escrever bons testes de unidade

## O que testes de unidade devem fazer?

Um teste de unidade deve testar uma pequena unidade de código, seja esta unidade uma ou mais funções, garantindo seu comportamento esperado de acordo com as regras de negócio. Serão frequentemente rodados durante o desenvolvimento, muitas vezes com auxílio de uma IDE.

Existem também testes de integração - que testam fluxos maiores, muitas vezes com presença de API's externas - e testes de sistema, que testam o fluxo inteiro, como o usuário, comunmente simulando uma interface gráfica.

Os testes unitários auxiliam na detecção de bugs, garantindo que funciona devidamente para um conjunto de casos específicos e, caso novos bugs surjam, possibilitam saber o que funciona e o que não funciona, de modo que novos testes cobrindo o bug sejam escritos e a resolução do problema seja feita.

Vale lembrar que eles não garantem a ausência de bugs, apenas sua presença 

## Vantagens de bons testes

Embora bons testes consumam um tempo de desenvolvimento considerável, eles tornam o software mais robusto e melhoram a experiência de programação. Entre suas principais vantagens, temos:

### Melhor qualidade

A quantidade de bons testes é correlacionada com maior qualidade do sistema, uma vez que ele se tornará mais robusto, resistente ao tempo e autodocumentado, de forma que seja mais fácil de manter e adicionar features, já que há testes verificando os comportamentos esperados. Além disso, protegerá do tempo, de modo que desenvolvedores futuros consigam entender o que cada componente deve fazer em cada caso e ter garantia de funcionamento esperado em todos os cenários.

### Reduzir erros antes de ir para produção

Detectar erros antes de ir para produção faz os custos serem menores, já que alterar qualquer coisa uma vez que foi ao ar é mais caro que resolver enquanto está em desenvolvimento/homologação, uma vez que o sistema já estará em uso e o tempo fora do ar custará perdas ao cliente. Caso seja detectado um bug, ele pode ser reproduzido, simulado e testado, vendo como as entradas reagem a ele, possibilitando uma resolução mais rápida.

### Evoluir com velocidade e confiança

Os engenheiros de software envolvidos no projeto tem melhor experiência de trabalho, já que conseguem ter feedback quase instantâneo da corretude do que estão desenvolvendo e se algum erro ou efeito colateral foi introduzido, incrementado a velocidade e qualidade da evolução do código. Isso tudo faz com que a produtividade aumente e que erros sejam detectados prontamente, reduzindo a necessidade de depuração e empoderando o time a realizar mudanças sem medo de quebrar outras funcionalidades.

### Código seguirá padrões melhores

Com a frequente escrita de testes o sistema tenderá a ser mais desacoplado e coeso, pois pensaremos muito sobre como o teste pode ser escrito enquanto criamos o código, analisando entradas e saídas.

As funções serão suficientemente enxutas para serem testadas como uma unidade, algo difícil de se fazer com baixa coesão (responsabilidades demais por função) e terão menos dependências externas, já que isso precisaria ser simulado toda vez que um teste fosse criado, incentivando menor acoplamento. Tal princípio se chama *Design for Testability*
