## Políticas de escalonamento

1. FIFO: First in first out, primeiro leva vantagem
			Não é usualmente  preemptiva, beneficia processos científicos
2. Shortest job first: algoritmo ótimo, coloca os menores primeiro. Tem o problema de calcular o tamanho do *burst*, estimativa de duração do próximo processo. Bom para processos em batch que você sabe os tempos de execução aproximados
3. Round robin: considera um quantum de tempo e, ao estourar o quantum, troca de processo. Beneficia aplicações interativas mas científicas não, já que resultados parciais não ajuda,
4. Prioridades: Tem alocação estática, ou seja, mais importantes inerentemente rodam primeiro e dinâmica, que os mais perto do prazo rodam primeiro. Pode levar a inanição
5. Múltiplas filas: várias filas, cada um com uma regra e possibilidade de promoção/rebaixamento
6. Completly Fair Scheduler: Cada processo tem uma fatia ideal, execução reduz fatia (demora excessiva perde prioridade), espera não (processos interativos não são afetados) 

### Compartilhamento de variáveis
 É possível implementar operações atômicas por software. O problema de sincronização é a falta de comunicação, o que gera condições de corrida.
 
* Condição de corrida: quando dois processos tentam executar a mesma ação e somente um deles consegue porque "ganhou"
* Exclusão mútua: apenas um processo faz algo em um instante
* Seção crítica: apenas um processo pode executar essa seção de código, tornando-a atômica.

Troca de contexto é um problema, necessário garantir que ela não seja um problema (exemplo: trocar de contexto antes de afixar o aviso que não tem leite)

Requisitos:

1. Apenas um processo dentro da seção crítica
2. Em caso de múltiplas solicitações deve permitir que apenas uma prossiga
3. Processos não podem morrer na seção crítica

Como implementar os requisitos:

1. Trancar sempre antes de utilizar
2. Destrancar sempre que termianr
3. Não trancar de novo se já tiver trancado
4. Não ficar muito tempo na seção crítica

### Problema produtor consumidor

Colocam e tiram itens de um buffer, é necessário sincronização de acesso, para que o produtor não coloque itens demais e o consumidor não consuma uma fila vazia.

## Primitivas de sincronização

 1. Better mutex - sleep/wakeup
		 Tem uma "cama" dentro que evita espera ocupada, colocando o processo em uma fila de processos "dormindo" . Ao colocar para dormir você marca como bloqueado, insere na fila de dormindo, dá um unlock (mutex baixo nivel), chama o escalonador para escolher outro processo e  mais um lock (mutex baixo nivel). Faz uso de uma seção "super crítica" dentro do lock, minimizando a espera ocupada.
		 A verificação se o if (!m->free) garante que, se o processo atual não puder continuar por um lock, outro é escolhido
		 Temos que garantir que no algoritmo de better_lock ninguém escreva em uma mesma variável
2. Semáforos: podem ser binários ou de contagem, só permitem n pessoas
3. Monitores: Utilizam uma classe específica em que todos os métodos são mutualmente exclusivos 
4. Mensagens: envio e recebimento. O produtor consumidor poderia ser feito com um exemplo em que ele fica aguardando mensagens, travado, de produção/consumo um do outro.

### lock/unlock

-   Exclusão mútua;
-   Primitiva básica a partir da qual a maioria das outras é implementada;
-   Espera ocupada: seção crítica deve ser mínima;

### sleep/wakeup

-   Evitam espera ocupada;
-   Junto com lock/unlock formam um conjunto completo de primitivas de sincronização;

-   O conjunto lock/unlock e sleep/wakeup são ``perfeitos'' para sincronização:
    -   Usados para acesso a variáveis compartilhadas:
    -   Como as variáveis são explicitamente declaradas, não existem ``efeitos colaterais''.
    -   Simples de usar e entender;
    -   Separam sincronização e espera;

    struct bed {
      wait_queue queue;
    }
    
    sleep(b, k) {
      currentproc->state = BLOCKED;
      insert_queue(b->queue, currentproc);
      unlock(k);
      schedule();
      lock(k);
    }
    
    wakeup(b) {
      p = remove_queue(b->queue);
      if (p != NULL)
        p->state = READY;
    }

### Agora implementando exclusão mútua sem busy waiting

struct better_mutex {
  mutex k;
  bed b;
  int free;
}

better_lock(k) {
  lock(k->mutex);
  if (!k->free)
    sleep(k->bed, k->mutex);
  k->free = 0;
  unlock(k->mutex);
}

better_unlock(k);
  lock(k->mutex);
  k->free = 1;
  wakeup(k->bed);
  unlock(k->mutex);
}

## Problemas clássicos de sincronização

### Filósofos comensais

Uma solução é tornar um deles canhoto, pegando o garfo em ordem diferente, e os demais com os locks esquerda direita, resolvendo o problema da **espera circular**, já que o canhoto vai por último ( ou primeiro)

Outra solução é usar uma antessala com semáforo de contagem n-1, fazendo com que nem todos possam entrar, com alguns esperando

Bebedeira dos filósofos: variação que você usa o jantar dos filósofos para saber se espera ou pega outra

### Leitores e escritores
Semelhante a uma loja de ecommerce

Escritores tem que ter um lock, de modo a garantir a exclusão mútua.

Semáforos de escritor e leitor podem sufocar os escritores, de modo que se chegarem leitores demais o escritor nunca roda

Uma solução legal é usar uma antessala com semáforo, de modo que só entrem leitores quando ela se tornar zero 

### Barbeiro dorminhoco
Interessante usar lock unlocks cruzados para garantir que um vai ser executado logo depois do outro, como um sleep wakeup.

Precisamos entrar no cliente, ver se tem cadeira e, se tiver, acordar o barbeiro. Senão desbloquear mutex e continuar o cliente


## Transações

2 phase locking não garante ausência de deadlocks mas sim a serialização, já que cresce e encolhe

## Deadlock

Deadlock depende das três coisas para poder acontecer. Se não existirem, não pode ter deadlock
1. Exclusão mutual
2. Sem preempção (não é interrompido)
3. Espera circular
Deadlock é um ciclo no grafo de dependências

Podemos
4. Não deixar deadlock acontecer
5. Recuperar de deadlock
6. Fingir que não existe  

A melhor maneira de lidar com deadlocks é evitar espera circular. Um jeito é ordenar os recursos e adquiri-los em ordem, de modo que um ciclo não aconteça ou garantir que ele nunca vai esperar recursos (algoritmo do banqueiro)

### Algoritmo do banqueiro

Só permite processos que adquirem recursos disponíveis, embora recuse processos que podem não causar deadlock (conservador demais)


## Detecção de deadlocks
Caro e deve ser chamado infrequentemente

### REcuperação de deadlocks

Podemos abortar processos (todos ou só alguns, cuidado com inanição) ou tomar de volta o processo, como um rollback
 

 

