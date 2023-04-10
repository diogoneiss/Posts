## Requisitos do SGBD
* Abstração de acesso aos dados
* Suporte a múltiplas visões
## Arquitetura 3 esquemas
Geram abstrações e independência.

Independência lógica permite alterar o esquema conceitual sem alterar o esquema externo ou aplicações, como no caso de adicionar novas colunas. Pode ser violada com a remoção de alguma coluna

Independência física permite alterar o esquema interno sem mudar o conceitual ou externo, como no caso de alterar a compressão ou estrutura de dados.

Nível externo: o que será exibido, nas visões. 
_______ ind lógica
Nível conceitual: o que será armazenado: entindades, relacionamentos, operações
_______ ind física
Nível interno: como será armezenado, nível físico


Data Independence: The three-level architecture allows for data independence, which means that changes made at one level do not affect the other levels. For example, changes made to the physical storage of data do not affect the logical view of data seen by application programs.

Security: The three-level architecture allows for security measures to be implemented at each level. For example, data access and modification can be restricted at the external level, and data encryption can be implemented at the internal level.

Scalability: The three-level architecture allows for scalability, as each level can be scaled independently. For example, the physical storage can be expanded without affecting the logical view or application programs.

Flexibility: The three-level architecture allows for flexibility, as changes can be made at any level without affecting the others. For example, changes to the logical view can be made without affecting the physical storage.

Simplification: The three-level architecture simplifies the development of complex database systems, as it provides a clear separation of concerns between the different levels. This makes it easier to design, implement, and maintain large and complex databases.

## Modelo conceitual

Descreve de forma mais conceitual e e próxima da perceoção dos usuários, independe de aspectos de implementação

## Modelo entidade relacionamento - alto nível

* Chave composta: depende de mais de um atributo, ver como implementar
* Restrições estruturais: cardinalidade (numero de instancias que pode participar) e participação (se a existência depende do relacionamento com outra entidade, ou seja, se é total ou parcial. é a linha dupla)
### Hierarquia
Especialização pode ser definida por atributo, ou seja, um campo na entidade indica seu tipo

Disjunção: Podem ser disjuntas (exclusão mútua, representa com um d) ou sobrepostas (representada com um o, quando as duas especializações podem coexistir)
Completude: a cobertura da super classe em relação às sub classes pode ser total ou parcial 

Lattice: quando criamos uma subclasse derivada de superclasses separadas
### Relacionamentos
Indica associações entre duas ou mais entidades distintas
(feito com um losango )

Grau indica o número de tipos de entidades participantes de um relacionamento, acima de 3 é mt raro
## Modelo Relacional - modelo lógico, baixo nível

* Super chave: por padrão é a tupla inteira
* Chave: é uma super chave minimal, o mínimo necessário para id unicamente uma tupla
Chaves candidatas: contém chave primária e alternativas
No caso de um relacionamento n x m, teremos dois atributos sendo a chave primária, já que sua junção que identifica o registro em si
### Restrições de integridade
* Domínio: dados são do tipo específico para o atributo
* Entidade: chave primária não pode ser nula
* Integridade relacional: Emerge dos relacionamentos e garante a referência a tuplas existentes. Serve para chaves estrangeiras.

Dois casos: t1[FK] = t2[PK] ou t1[FK] = null. Não é permitido referências inválidas.

Exemplo: EMPLOYEE[DNO] -> DEPARTMENT[DNUMBER]
### Opções de remoção
* bloqueio (impedir a remoção, caso de vc tentar remover um dpto com funcionários dentro ainda)
* propagação
* replace por null

Notação = R1[FK] op -> R2[PK], com op em {b, p, n} e acima da seta

Um exemplo legal é dependentes. Temos a restrição DEPENDENT[ESSN] p -> EMPLOYEE[ESS], logo, se você apagar o funcionário, todos os seus dependentes são removidos também.

Ao desenhar, colocamos a restrição na seta de relação estrangeira.