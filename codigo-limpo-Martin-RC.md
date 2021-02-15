## Capítulo 12 - Emergência

Quatro regras do Projeto Simples

1. *Efetuar todos os testes*: se não há uma maneira fácil de verificar que o código funciona, ele é
dubitável.
2. *Sem duplicação de código*
3. *Expressar o propósito do programador*
4. *Minimizar o número de classes e métodos*

### Expressividade

Grande parte dos custos de um projeto de software está na manutenção em longo prazo. Qnto mais claro
o autor tornar seu código, enos tempo outras pessoas terão de gastar para compreendê-lo. Isso reduz
os defeitos e o custo de manutenção.

- Escolha de bons nomes;
- Mantendo pequenas as classes e funções;
- Usar uma nomenclatura padrão (padrões de projeto);
- Testes de unidade bem escritos;

  É necessário praticar!!!

### Poucas classes e métodos

Apesar de termos que tentar escrever funções e classes pequenas, devemos tentar, ao mesmo tempo,
reduzir sua quantidade, portanto minimizando tanto o tamanho quanto a quantidade de classes e
funções.

## Capítulo 13 - Concorrência

**Objetos são abstrações de procedimento. Threads são abstrações de agendamento** - James O. Coplien

### Por que concorrência?

Concorrência é uma estratégia de desacoplamento.
Desacoplar melhora consideravelmente tanto as estruturas quanto a taxa de transferência. Devemos
pensar que o aplicativo deveria como muitos minicomputadores trabalhando juntos. 
Este desacoplamento:

- Facilita a compreenção do sistema;
- Oferece recursos para separar preocupações.

### Mitos e conceitos equivocados

- *Mito -> frases mais corretas*
- A concorrência sempre melhora o desempenho -> A concorrência gera um certo aumento, tanto no
desempenho quanto na criação de código adicional.
- O projeto não muda ao criar programas concorrentes -> Uma concorrência correta é complexa, mesmo
  para problemas simples. A concorrência geralmente requer uma mudança essencial na estratégia do
  projeto.
- -> Os bugs de concorrência geralmente não se repetem, portanto são frequentemente ignorados como
  casos únicos em vez dos defeitos que realmente são.

### Princípios para proteção da concorrência

1. *Princípio da Responsabilidade Única:* O código voltado para concorrência possui seus próprios
desafios, portanto, **mantenha seu código voltado para a concorrência separado do resto do código.**
2. *Limite o escopo dos dados:* Leve a sério o encapsulamento de dados; limite severamente o acesso
a quaisquer dados que possam ser compartilhados.
3. *Use cópia de dados:* Se houver uma maneira fácil de evitar o compartilhamento de objetos, será
muito pouco provável que o código resultante cause problemas.
4. *As threads devem ser as mais independentes possíveis:* Escreva seu código de modo que cada
thread exista em seu próprio mundo, sem compatilhamento de dados.

### Métodos de Execução

1. *Producer-Consumer:* Uma ou mais threads **producer** criam alguma tarefa e colocam em um buffer
ou fila de espera. Uma ou mais threads consumer pegam a tarefa da fila de espera e a finalizam.
2. *Leitores e escritores:* Quanto existe um recurso compartilhado que serve principalmente como uma
fonte de informações para leitores, mas que de vez em quanto é atualizada por escritores. O problema
consistem em coordenar os leitores de modo que não leiam algo que um escritor esteja atualizando, e
vice-versa.
3. *Dining Philosophers (Problema dos Filósofos):* Uma mesa redonda com vários filósofos, cada um
com um garfo no seu lado esquerdo, e um prato de macarrão no meio. Os filósofos só comem o macarrão
quando estão com fome, e para isso, precisam de dois garfos. Substitua os filósofos por threads e os
garfos por recursos.


**Recomendação:** Aprenda esses algoritmos básicos e entenda suas soluções.


### Cuidado com dependências entre métodos sincronizados

Dependências entre métodos sincronizados causam pequenos bugs no código concorrente. Evite usar mais 
de um método em um objeto compartilhado.
Três formas de deixar um código com um objeto compartilhado correto:
1. Bloqueio voltado para cliente
2. Bloqueio voltado para servidor
3. Servidor extra

### Mantenha pequenas as seções sincronizadas

Seções sincronizadas adicionam bloqueios que garantem que apenas uma thread rode por vez. Isto causa 
atrasos e trabalho extra, portanto deve-se proteger apenas seções críticas.

### É difícil criar códigos de desligamento corretos

Uma má implementação pode fazer com que threads fiquem travadas e o programa acabe não finalizando com sucesso.

Pense o quanto antes no desligamento do programa e faça com que ele funcione com êxito. Vai levar mais tempo do que
você espera. Revise os algoritmos existentes, pois isso é mais difícil do que você imagina.


### Teste de código com threads

Recomendações:

- Trate falhas falsas como questões relacionadas às threads.
- Primeiro, faça com que seu código sem thread funcione.
- Torne seu código com threads plugáveis;
- Torne seu código com threads ajustável;
- Execute com mais threads do que processadores;
- Execute em diferentes plataformas;
- Altere seu código para testar e forçar falhas.

Outras recomendações:

- Não ignore falhas de sistema como se fossem casos isolados;
- Não procure bugs não relacionados a threads com os relacionados a elas ao mesmo tempo. Certifique-se
de que seu código funciona sem threads.
- Faça de seu código com threads especialmente portátil de modo que possa executá-lo em várias configurações.
- Encontre maneiras de cronometrar o desempenho de seu sistema sob variadas configurações.
- Coisas acontecem quando o sistema alterna entre as tarefas. Execute mais threads do que os processadores ou núcleos presentes.
- Execute o quanto antes e frequentemente seu código com threads em todas as plataformas finais.

### Altere seu código para testar falhas

É comum que falhas se escondam em códigos concorrentes. Testes simples nem sempre conseguem expor esses erros.
Uma opção é forçar falhas de duas maneiras:

*Manualmente*

Inserir chamadas wait(), sleep(), yield() e priority() em lugares específicos para forçar falhas.

*Automátizada*

Você poderia utilizar uma classe com um único método:

'''vim
public class ThreadJigglePoint {
    public static void jiggle() {
    }
}
'''

É possível adicionar esta chamada em vários lugares no código:

'''vim
public synchronized String nextUrlOrNull() {
    if (hasNext()) {
        ThreadJigglePoint.jigle();
        String url = urlGenerator.next();
        ThreadJigglePoint.jigle();
        updateHasNext();
        ThreadJigglePoint.jigle();
        return url;
    }
    return null;
}
'''

A chamada agora pode selecionar aleatoriamente uma das ações: fazer nada, dormir ou ficar passivo.


## Capítulo 14 - Refinamento Sucessivo

Um caso de estudo de um analisador sintático de parâmetro em uma linha de comando.


## Capítulo 15 - Características Internas do JUnit

Será analizado um exemplo retirado do framework JUnit. O autor dá um exemplo de como poderia ser feito 
um refratoramento do código.


## Capítulo 16 - Refratorando o SerialDate

Um exemplo mais extensivo de como fazer um refratoramento de código. A classe SerialDate é refratorada neste
capítulo.


## Capítulo 17 - Odores e Heurísticas

Este capítulo é uma lista de com dicas de pontos de atenção no código, para que o mesmo se torne mais limpo. 

### Comentários

- *C1: Informações inapropriadas:* 
Metadados, como autores, data da última atualização, número SRP e assim por diante, não deve ficar nos comentários.
Este deve conter apeans dados técnicos sobre o código e projeto.
- *C2: Comentário obsoleto:*
Comentário que ficou velho, irrelevante e incorreto é obsoleto. Atualizá-lo ou se livrar dele.
- *C3: Comentários redundantes:*
Remover
- *C4: Comentário mal escrito:*
Um comentário que valha deve ser bem escrito. Não erre. Não diga o obvio. Seja breve.
- *C5: Ceodigo como comentário:*
Exclua-o.


### Ambiente

- *A1: Construir requer mais de uma etapa:*
Construir um projeto deve ser uma operação simples e única.
- *A2: Testes requerem mais de uma etapa:*
Você deve ser capaz de rodar todos os testes de unidade com apenas um comando.

### Funções

- *F1: Parâmetros em excesso:*
Funções devem ter um número pequeno de parâmetros.
- *F2: Parâmetros de saída*
Leitores esperam que parâmetros sejam de entrada, e não de saída.
- *F3: Parâmetros lógicos*
Parâmetros booleanos dizem que a função faz mais de uma coisa. Eles são confusos e devem ser eliminados.
- *F4: Função morta*
Descartar métodos que nunca são chamados.

### Geral

- *G1: Múltiplas linguagens em um arquivo fonte*
Minimizar tanto a quantidade como o uso de linguagens extras em nossos arquivos-fonte.
- *G2: Comportamento óbvio n˜åo é implementado*
Quando um comportamento nnão é implementado, os leitores e usuários do código não podem mais depender
de suas intuições sobre o que indica o nome das funções.
- *G3: Comportamento incorreto nos limites*
Não dependa de sua intuição. Cuide de cada condição de limite e crie testes para cada.
- *G4: Seguranças anuladas*
Desabilitar os testes de falhas e dizer a si mesmo que os aplicará depois é tão ruim quanto fingir
que seus cartões de crédito sejam dinheiro gratuito.
Minimizar tanto a quantidade como o uso de linguagens extras em nossos arquivos-fonte.
- *G2: Comportamento óbvio n˜åo é implementado*
Quando um comportamento nnão é implementado, os leitores e usuários do código não podem mais depender
de suas intuições sobre o que indica o nome das funções.
- *G3: Comportamento incorreto nos limites*
Não dependa de sua intuição. Cuide de cada condição de limite e crie testes para cada.
- *G4: Seguranças anuladas*
Desabilitar os testes de falhas e dizer a si mesmo que os aplicará depois é tão ruim quanto fingir
que seus cartões de crédito sejam dinheiro gratuito.
- *G5: Duplicação*
DRY (Don't repeat yourself). Sempre que você vir duplicação de código, significa que perdeu uma chance de 
abstração. Estruturas aninhadas de switch/case e if/else: analizar uma substituição por polimorfismo.
Algoritmos parecidos, mas não possuem as mesmas linhas de código: usar TEMPLATE METHOD ou STRATEGY.
- *G6: Códigos no nível errado de abstração*
Queremos que todos os conceitos de níveis mais altos fiquem na classe base e que todos os níveis mais 
baixos fiquem em suas derivadas.
- *G7: As classes base dependem de suas derivadas*
De modo geral, as classes base não deveriam enxergar nada em suas derivadas.
- *G8: Informações excessivas*
Módulos bem definidos possuem interfaces pequenas que lhe permite fazer muito com pouco. Tentar limitar o que 
é exposto nas interfaces de suas classes e módulos.
- *G9: Código morto*
Aquele que não é executado. Após um tempo começa a "cheirar". Exclua-o do sistema.
- *G10: Separação vertical*
Devem-se declarar as variáveis e funções próximas de onde são usadas.
- *G11: Inconsistência*
Se fizer algo de uma determinada maneira, faça da mesma forma todas as oturas coisas similares.
- *G12: Entulho*
Construtores sem implementação, variáveis não usadas, funções não chamadas são entulhos. Limpe-os.
- *G13: Acoplamento artificial*
Ocorre quando se colocar uma variável, uma constante ou uma função em um local temporariamente conveniente, porém inapropriado. 
Tome seu tempo para descobrir onde devem ser declaradas as funções, as constantes e as variáveis. 
- *G14: Feature Envy*
Os métodos de uma classe devem ficar interessados nas variáveis e funções da classe a qual eles pertencem, e não 
nas de outras classes.
- *G15: Parâmetros seletores*
De modo geral, é melhor ter muitas funções do que passar um código por parâmetro para selecionar o comportamento.
- *G16: Propósito obscuro*
Não usar expressões contínuas, notação húngara e números mágicos, pois obscurecem a intenção do autor.
- *G17: Responsabilidade mal posicionada*
Onde colocar o código? Utilizar o princípio da surpresa mínima: colocar o código onde um leitor geralmente espera.
- *G18: Modo estático inadequado*
Em geral, deve-se dar preferência a métodos não estáticos. Na dúvida, torne a função não estática.
- *G19: Use variáveis descritivas*
Uma das formas mais poderosas de tornar um programa legível é separar os cálculos em valores intermediários armazenados 
em variáveis com nomes descritivos.
- *G20: Nomes de funções devem dizer o que elas fazem*
Se tiver de olhar a implementação da função para saber o que ela faz, então é melhor selecionar um noome melhor.
- *G21: Entenda o algoritmo*
Escreva um algoritmo sabendo o que ele faz e não remendando vários pedaços buscando alcançar um objetivo.
- *G22: torne dependências lógicas em físicas*
O módulo dependente não deve fazer suposições sobre o módulo no qual ele depende.
- *G23: prefira polimorfismo a if/else ou switch/case*
Regra do "UM SWITCH"
- *G24: Siga as convenções padrões*
- *G25: Substitua os números mágicos por constantes com nomes*
- *G26: Seja preciso*
Quando tomar uma decisão em seu código, a faça precisamente. Saiba por que tomou a decisão e como lidará com 
quaisquer excessões.
- *G27: Estrutura acima de convenção*
Decisões no projeto devem-se basear em estruturas e não em convenções.
- *G28: Encapsule as condicionais*
Extraia funções que expliquem o propósito da estrutura condicional.
'''vim
if (shouldBeDeleted(timer))
'''
é melhor que
'''vim
if (timer.hasExpired() && !timer.isRecurrent())
'''
- *G29: Evite condicionais negativas*
- *G30: As funções devem fazer uma coisa só*
- *G31: Acoplamentos temporais ocultos*
'''vim
public void dive(String reason) {
    saturateGradient();
    reticulateSplines();
    diveForMoog(reason);
}
'''

tornar os acoplamentos temporais explícitos:
'''vim
public void dive(String reason) {
    Gradient gradient = saturateGradient();
    List<Spline> splines = reticulateSplines(gradient);
    diveForMoog(splines, reason);
}
'''
- *G32: Não seja arbitrário*
Tenha um motivo pelo qual você estruture seu código e certifique-se de que tal motivo seja informado na estrutura.
- *G33: encapsule as condições de limites*
'''vim
nextLevel = level +1;
'''
- *G34 Funções devem descer apenas um nível de abstração*
- *G35: Mantenha os dados configuráveis em níveis altos*
- *G36: Evite a navegação transitiva*
Lei de Demeter (criar um "Código Tímido": garantir que os módulos saibam sobre seus colaboradores 
imediatos apenas e não sobre o mapa de navegação de todo o sistema.

### Nomes

- *N1: Escolha nomes descritivos*
Nomes em software são 90% responsáveis pela legibilidade do código.
- *N2: Escolha nomes no nível apropriado de abstração*
- *N3: Use uma nomenclatura padrão onde for possível*
- *N4: Nomes não ambíguos*
- *N5: Use nomes longos para escopos grandes*
- *N6: Evite codificações*
- *N7: Nomes devem descrever os efeitos colaterais*

### Testes

- *T1: Testes insuficientes*
Uma coleção de testes deve testar tudo o que pode vir falhar. Testes são insuficientes enquanto houver condições 
que não tenham sido exploradas.
- *T2: Use uma ferramenta de cobertura!*
- *T3: Não pule testes triviais*
- *T4: Um teste ignorado é uma questão sobre uma ambiguidade*
- *T5: Teste as condições de limites*
- *T6: Teste abundantemente bugs próximos*
- *T7: Padrões de falhas são reveladores*
- *T8: Padrões de cobertura de testes podem ser reveladores*
- *T9: Testes devem ser rápidos*

## Abreviações

*SRP:* Princípio de Responsabilidade Única (método/classe/componente deve ter apenas um motivo para
ser alterado).
*DIP:*
*DRY:* Princípio do Não Se Repita



