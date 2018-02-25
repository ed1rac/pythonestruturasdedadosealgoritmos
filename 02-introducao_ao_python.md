# Introdução ao Python

Python é uma linguagem de programação originalmente desenvolvida por Guido van Rossum no início dos anos 90. A versão _major_ mais recente do Python é a 3, lançada em 2008. Estas notas tomam como base esta última versão.

O site oficial da linguagem Python é [http://www.python.org](http://www.python.org). Lá você encontra as versões de Python disponibilizadas de forma gratuíta e a documentação.

## O Interpretador

Python é uma linguagem interpretada - o que significa que os comando são executados através de um software - o _Interpretador Python_.

O intepretador é o software que recebe um comando, o avalia e reporta os resultados de um comando python por vez.

O interpretador pode ser usado pelo programador de forma interativa - que é quando o programador interage adicionando um comando ou bloco de comandos por vez ao interpretador - e recebe a respostas: como um jogo de perguntas e respostas na qual o comando é a "pergunta" e o resultado do comando é a "resposta" que o interpretador devolve. Isto é bastante útil, principalmente quando estamos procurando os erros de um programa.

Entretanto, na maioria das vezes, o programador coloca todo o código Python em arquivos e executa o interpretador apontando-o para o arquivo que tem o código Python. Chamamos estes arquivos de _scripts_ ou _código fonte_ e, como convenção, os salvamos com a extensão _.py_.

### Como executar comandos Python
Após instalar o Python no seu computador você pode invocar o interpretador de forma iterativa, executando o comando `python` no seu SO, sem argumentos.

Ou, pode executar um script com comandos Python pré-definidos ao executar o comando `python` colocando o caminho para seu arquivo de compandos como argumento, como por exemplo em `python nome-do-seu-script.py`. Neste caso o interpretador vai executar o seu script Python a partir do arquivo.

Ainda, você pode usar uma _flag_ adicional `-i` para informar ao interpretador que funcione de modo iterativo após executar o seu script Python. neste caso o comando é: `python nome-do-seu-script.py`

Há outras formas de executar comandos Python, e há muitas ambientes integrados de desenvolvimento (IDEs, em inglês) - como o IDLE, o PyCharm e o Jupyter - que facilitam o desenvolvimento em Python. Nestas notas vamos focar no uso do Jupyter.

## Como é um Programa Python?

O exemplo a seguir é um programa simples em Python que calcula a média ponderada das entradas que o usuário digita durante a execução do script.

```python
print('Bem vindo à calculadora de média!')
print('Digite os valores, um par por linha:')
print('Entre com uma linha em branco quando finalizar')

soma = 0.0
quantidade = 0

finalizou = False                      # flag que aponta se o usuário entrou com uma linha em branco

while not finalizou:
    entrada = input()
    if entrada == '':
        finalizou = True
    elif not entrada.isnumeric():      # testa se a entrada é um número
        print('Formato da entrada \'{0}\' não reconhecido. Entrada ignorada'.format(entrada))
    else:
        soma += float(entrada)
        quantidade += 1

print('A média é ', end='')
if quantidade == 0:
    print(0.0)
else:
    print(soma/quantidade)
```

Note que:

* a sintaxe do Python se apóia no uso de espaços em branco
* comandos individuais geralmente são terminados com um caractere de final de linha - embora é possível um comando ser extendido através de um caractere de barra invertida `\` ou da abertura de um delimitador que não foi fechado
* a identação (os espaços em branco ou tabulações) é elemento chave na hora de definir o corpo de execução de estruturas de controle - note a identação das  8 linhas que estão após a instrução `while`
* o caractere '#' inicia um comentário de linha - tudo o que tiver após o '#' é uma anotação para o programador e é ignorado interpretador.

## Objetos em Python

Python é uma linguagem orientada à objetos e as _classes_ formam a base para todos os tipos de dados. Vamos ver mais sobre Orientação a Objetos no [Próximo Capítulo](TODO: Por a referência do próximo capítulo aqui!)

### A Declaração de Atribuição

O comando mais importante de todos em Python é a _declaração de atribuição_:

```python
    temperatura = 36.5
```

Este comando estabelece a palavra "temperatura" como um *_identificador_* (ou *_nome_*) e então associa-o com um *_objeto_* de ponto flutuante com o valor 36,5.

Os identificadores em Python:

* são _case-sensitive_ [^case-sensitive-footnote]
* podem ser compostos uma combinação de letras, números e caracteres _underscore_ (o caractere 'sublinhado').
* não podem começar com um número
* há palavras reservadas ao Python que não podem ser usadas como identificadores: `False, None, True, as, assert, break, class, continue, def, del, elif, else, except, finally, for, from, flobal, if, import, in, is, lambda, nonlocal, not, or, pass, raise, return, try, while, whith` e `yeld`.

[^case-sensitive-footnote]: quando dizemos que identificaroes são _case-sensitive_ nos referimos a serem sensíveis ao uso de caracteres maiúsculos ou minúsculos, assim `temperatura` é diferente de `Temperatura`.

Python é uma linguagem *_dinamicamente tipada_*, isso quer dizer que não há declaração prévia associando um identificador com um tipo particular de dados.

Para aqueles familiarizados com linguagens como C++ ou Java, um identificador em Python é semelhante a uma variável apontador, ou uma variável de referência - no qual o identificador é na verdade associado à posição de memória em que está o objeto a que se refere. `None` é um objeto especial em Python que server para propósitos similares a referencia a `null` em Java e C++.

Um programador pode estabelecer um *_alias_* ao atribuir um segundo identificador para um objeto existente. Neste caso é importante notar que se o objeto referido suporta comportamentos que afetam o seu estado a mudança será percebida através dos dois identificadores. Contudo, se um dos _nomes_ é re-atribuído a um novo valor usando uma declaração de atribuição subsequente, isto não afeta o outro identificador_.

### Criando e Usando Objetos

#### Instanciação

O processo de criar uma nova instância de uma classe é conhecida como *_instanciação_*. em geral, a sintaxe para instanciar um objeto é invocar o construtor da classe.
Por exemplo: se a classe se chama `Quadrado`, você pode instanciá-la usando uma sintaxe `q = Quadrado()` se o construtor não necessita de parametros, ou `q=Quadrado(`$param_1$, $param_2$, ..., $param_n$`)` se necessita de $n$ parametros.

Muitas das classes _built-in[^built-in-footnote]_ do Python suportam serem instanciadas por um *_literal_*. Por exemplo, `temperatura = 36.5` resulta na criação de uma nova instância da classe *float* que tem o valor 36,5 e foi expressa no código a partir de um literal.

[^built-in-footnote]: Built-in são as classes que já vem com o Python. São definidas pela própria linguagem.

#### Chamando Métodos

As classes em Python podem definir um ou mais *_métodos_* (também conhecidas como *_funções de membro_*), que são invocadas de uma instância específica da classe usando um operador de ponto ("."). Por exemplo: `entrada.isnumeric()` - que vimos no código da sessão (TODO: colocar sessão aqui) que executa o método `isnumeric()` sobre a string `entrada`, retornando se é ou não é uma string com conteúdo numérico.

O Python também suporta funções tradicionais (veja a sessão [Funções](#funções) - TODO: colocar o link da seção "Funções" aqui)

*_Métodos_* chamados a partir de uma instância podem ser classificados como:

* _accessors_: quando retornam informações sobre o objeto mas não mudam o seu estado, ou
* _mutators_ ou _métodos de atualização_: queu mudam o estado do objeto.


#### Classes Built-in do Python

As classes built-in do Python podem ser classificadas como _imutáveis_ se cada objeto daquela classe tem um valor fixo a partir da instanciação - que não pode ser modificado, ou _mutáveis_ - caso contrário.

| Classe | Descrição | Imutável? |
|---|---|---|
| bool | Valor Booleano | :heavy_check_mark: |
| int | Inteiro (de magnitude arbitrária) | :heavy_check_mark: |
| float | Número de ponto flutuante | :heavy_check_mark: |
| list | Sequência mutável de objetos | |
| tuple | Sequência imutável de objetos | :heavy_check_mark: |
| str | String de caracteres | :heavy_check_mark: |
| set | Conjunto desordenado de objetos distintos | |
| frozenset | Conjunto imutável de objetos distintos | :heavy_check_mark: |
| dict | Mapeamento associativo (também conhecido como dicionário) | |


TODO: detalhar sobre cada uma das classes a seguir

* bool: números avaliam para `False` se zero e `True` se não zero. Sequências avaliam para `False` se vazias e `True` caso contrário. `None` resolve para `False`.
* int: se a partir de texto não numérico E número no texto não é inteiro avalia para `False`. representação octal, binaria e hexadecimal como 0o4527, 0b0011, 0x7fa2. Dá para usar a instanciação da classe int para resolver texto em outras bases. int('7f',16) resolve para 127.
* float: dá para excrever em notação cientifica. ex: 6.022e23 representa $6.022 x 10^{-23}$.
* sequencias: Python não tem uma classe separada para caracteres - Caractere é uma string de tamanho 1.
* lista: é uma estrutura referencial, armazena referências para os objetos que são seus elementos. São baseadas em arrays e são indexadas iniciando em zero. Tem a habilidade de expandir e contrair suas capacidades dinamicamente, conforme necessário.
* tupla: a tupla de 1 elemento deve ser declarada com uma vírtula depois do elemento, como em `(17, )`
* str: otimizda para representar uma sequência de caracteres Unicode. Strings literais podem ser declaradas udando ''' ou """ no início e final da literal string. 
* set: tem um método altamente otimizado para verificação de se um elemento específico está contido ou não no conjunto - baseado na estrutura de dados conhecida como _hash table_. Não mantém os dados em ordem. Só aceita adição de instancias de objetos imutáveis. pode ser instanciada como em  `set()` ou `{'um', 'dois', 'tres'}`
* frozenset: é uma forma imutável do _set_.
* dict: representa um _dicionário_ ou _mapeamento_ de um conjunto de _chaves_ distintas para seus _valores_ associados. Baseada em _hash tables_ assim como os _set_'s, podem ser instanciados como em `{ 'pt': 'Portugal', 'br': 'Brasil'}` ou `dict([('pt', 'Portugal'), ('br', 'Brasil')])`

#### Expressões, Operadores e Precedência

##### Operadores

* Lógicos: not, and, or. `and` e `or` tem short-circuit na avaliação.
* Igualdade: is, is not (para identidade), ==, != (para equivalência)
* Comparação: <, <=, >, >= - Operadores levantam uma exceção se os operandos são tipos incomparáveis.
* Aritméticos: +, -, *, /, //, %
* Bitwise (para inteiros): ~ (complemento, unário), & (and), | (or), ^ (xor), << (shift left, completa com zeros), >> (shift right, completa com o bit do sinal)
* de Sequência: s[j], s[start:stop], s[start:stop:step], s + t (concatenação), k*s (atalho para s + s + s ... k vezes), val in s (contém), val not in s. uso de índices negativos para indices a partir do fim. A sintaxe `del s[j]` remove o elemento da lista. Maior ou menor é avaliado lexicograficamente. s==t, s<t, <=, >, >=.
* para Conjuntos e Dicionários: key in s, key not in s, s1 == s2 (equivalente), !=, <= (subconjunto), < (subconjunto próprio), >=, >, | (uniao), & (interseção), - (subtração), s1 ^ s2 (elementos precisamente em 1 dos conjuntos)
* Atribuição extendida: +=, -=, *=, /= eles mudam o objeto original!. para não mudar precisa de uma reatribuição com x = x + 1.

Atribuição e comparação encadeadas: é valido `x = y = 0`, também `1 <= x + y <= 10`.

TODO: Colocar tabela 1.3/p17 de preceência.


## Control Flow

### If

```python
if first_condition:
    first_body
elif second_condition:
    second_body
elif third_condition:
    third_body
else:
    fourth_body
```

```python
if response:
```

é equivalente a:

```python
if response != '':
```

### Loops


```python
while condition:
    body
```

```python
for elemento in iterável:
    body
```

Por não ter como indexar um `set`o `while` não pode ser usado em `set`s, mas o for pode!


TODO: Falar do `range()`
TODO: Falar do `break`
TODO: Falar do `continue`


## Funções

Usamos o termo _funções_ quando nos referimos às funções tradicionais, _stateless_, que são invocadas sem o contexto de estado de alguma _classe_ ou _instãncia_ de alguma classe. Para invocá-las usamos a sintaxe `função(dados)`.

Usamos a palavra _método_ para nos referirmos às funções invocadas sobre um objeto específico, usando a sintaxe `dados.função()`.

A função a seguir conta quantas vezes um item equivalente ao `alvo` aparece nos `dados`.

```python
def contar(dados, alvo):
    n = 1
    for item in dados:
        if item == alvo:       # encontrou um item equivalente ao alvo
            n += 1
    return n
```

Chamamos de _assinatura_ da função a linha que começa com a palavra chave `def`. Ela estabelece um identificador como nome da função e identifica seus parâmetros.

Chamamos de _corpo_ da função as demais linhas. o corpo da função é tipicamente expresso como um bloco identado de código.

Cada vez que uma função Python é chamada, um _registro de ativação_ que armazena informações relevantes da chamada corrente é criado.

O _registro de ativação_ inclui o que chamamos de _namespace_ (o "espaço de nomes", numa tradução livre) a fim de separar identificadores que tem o escopo local na chamada corrente: todos os parâmetros da chamada da função e também todos os identificadores que forem definidos no corpo da função passam a fazer parte do _namespace_ da chamada da função.

Um identificador _local_ de uma função passa a não ter relação com identificadores com o mesmo nome que estão no escopo do _chamador_ da função. como no exemplo a seguir:

```python
def somar(a, b):
    return a + b
a = 10
resultado = somar(20,30)
```

Após a chamada `resultado` tem o valor `50`, independentemente de termos definido `a=10` no escopo de antes da chamada.

A palavra chave `return` indica que a função deve imediatamente cessar a execução. Se estiver seguida de alguma expressão, deve retornar o valor daquela expressão para o _chamador_. Se não há expressão explícita após o `return`, o valor `None` é automaticamente retornado para o chamador.

Não é necessário terminar uma função com a palavra `return`. Se o corpo da função termina e não há `return` então o valor `None` é enviado para o chamador.

Podem existir vários `return`s dentro da definição de uma função. O primeiro `return` encontrado, dado a lógica de controle de uma função para de executá-la e retorna ao escopo do chamador assim que for executado.

```python
def contem(dados, alvo):
    for item in alvo:
        if item == target:
            return True
    return False
resultado = somar([1, 2, 3], 2)
```

Neste exemplo `resultado` tem o valor `True`.

### Passagem de informações

No contexto de chamadas de funções, definimos como *parâmetros formais* os parâmetros da assinatura de uma função, e *parâmetros reais* os parâmetros identificados no momento da invocação da função.

Em Python, tanto a passagem de parâmetros quanto o retorno da função seguem a lógica do operador de _assignment_. Ou seja, _objetos_ não são copiados - o que garante que a invocação das funções Python seja eficiente.

#### Parâmetros Mutáveis

como o parâmetro formal é um alias para o parâmetro real, o corpo da função pode interagir com os objetos de forma que possam mudar o seu estado. Um exemplo é executar o ocomando `data.append('F')`. entretanto, se reatribuirmos o parâmetro formal (que é um alias) para outro valor, ele perde o vínculo com o objeto original e passa a não alterar mais o objeto original.

#### Parâmetros Default

Python proê meios para as funções suportarem mais de uma assinatura de chamada - ou seja, as funções podem ser polimórficas.

```python
def foo(a, b=15, c=27):
```

### Parâmetros por Palavras chaves

TODO: mostrar as diferenças entre parâmetros posicionais e parametros por palavra chave./

TODO: Exemplo da função `max(a, b, key=abs)`

```python
def myfunc2(*args, **kwargs):
   for a in args:
       print a
   for k,v in kwargs.iteritems():
       print "%s = %s" % (k, v)
```

### Funções Python built-in 

TODO: Colocar tabela 1.4/p29

### Input e Output com Python

TODO: print(), intput(), open(), tabela 1.5/p32 interação com arquivos de texto via um proxy do arquivo (fp)

### Gerenciamento de Excessões:

| Class | Description |
| --- | --- |
| Exception | classe baes para a maioria dos tipos de erros |
| AttributeError | criada pela sintaxe obj.foo se o objeto obj nao tem o membro chamado foo |
| EOFError | lançada se o EOF é alcançado para o console ou para um arquivo |
| IOError | falha numa operação de I/O (eg. Abertura de um arquivo) |
| IndexError | o índice de uma sequência está fora dos limites |
| KeyError | uma chave não existente no set ou dict foi usada |
| NameError | Um identificador não existente foi usado |
| StopIteration | lançado pela sintaxe next(iterador) quando não há mais elemento next |
| TypeError | O tipo errado de parâmetro foi enviado para a função |
| ValueError | parametro tem um valor inválido (eg. sqrt(-5)) |
| ZeroDivisionError | lançado quendo qualquer operador de divisão executa com denominador 0 |


#### lançando uma excessão

```python
def sqrt(x):
    if not isinstance(x, (int, float)):
        raise TypeError('x deve ser numérico')
    elif x < 0:
        raise ValueError('x não pode ser negativo')
    # Trabalho de verdade a partir desta linha
```


#### Agarrando uma excessão

```python
    try:
        razao = x / y
    except ZeroDivisionError:
        #faça algo aqui
```

```python
    try:
        fp = open('arquivo.txt')
    except IOError as e:
        print('Não foi possível abrir o arquivo:',e)
```

### Iteradores e Geradores


#### Iteradores

* um _iterador_ é um objeto que gerencia uma iteração através de uma série de valores.
* um _iterável_ é um objeto, obj, que produz um _iterador_ via a sintax _iter(obj)_

```python
data = [1, 3, 5, 7]
i = iter(data)
next(i)
```

Iteradores não fazem cópia dos dados do iterável e aplicam uma técnica chamada _lazy evaluation_ para só avaliar para um resultado se há a necessidade, economizando assim os recursos computacionais.

#### Geradores

Um gerador é implementado com uma xintaxe que é muito similar a das funções, mas ao invés de retornar valores, um comando *_yeld_* é executado para indicar cada elemento da serie

Exemplo com funções:

```python
def fatores(n):
    results = []
    for k in range(1, n+1):
        if n % k == 0:
            results.append(k)
    return results
```

Exemplo como generator:

```python
def fatores(n):
    for k in range(1, n+1):
        if n % k == 0:
            yield k
```

Exemplo otimizado como generator:

```python
def fatores(n):
    k = 1
    while k*k < n:         # enquanto k < sqrt(n)
        if n % k == 0:
            yield k
            yield n // k
        k += 1
    if k * k == n:         # caso especial quando n é um quadrado perfeito
        yield k
```


### Outras conveniências adicionais do Python

#### Expreções condicionais

```python
expr1 if condition else expr2
```

#### Sintaxe de _Comprehension_

```python
[ expression for value in iterable if condition ]
```

```python
[ k*k for k in range(1, n+1) ]        # list comprehension
{ k*k for k in range(1, n+1) }        # set comprehension
( k*k for k in range(1, n+1) )        # generator comprehension
{ k: k*k for k in range(1, n+1) }     # dict comprehension
```

Note que o generator comprehension é particularmente atrativo quando os resultados não precisam ser armazenados na memória!


#### Packing e Unpacking de sequencias

```python
data = 2, 3, 4, 5
return x, y
a, b, c, d = range(7, 11)
for k, v in mapping.items():
for a, b in zip(list_a, list_b):
```

#### Simultaneous assignments

```python
x, y, z = 6, 2, 5
j, k = k, j
```

```python
def fibonacci():
    a, b = 0, 1
    while True:
        yield a
        a, b = b, a + b
```

### Scopes and Namespaces

O processo de determinar o valor associado a um identifier é chamado de *_name resolution_*.

TODO: Diferença entre escopo global e local

Cada escopo no Python é representado através de uma abstração conhecida como *_namespace_*. O namespace gerencia todos os identificadores que estão correntemente definidos em um dado escopo.

TODO: Desenhar uma figura de um escopo

A função `dir()`reporta os nomes dos identificadores dado um namespace. A função `vars()` reporta os nomes e os valores.

Cada objeto tem seu próprio namespace para armazenar atributes e as classes também tem, cada uma, seu próprio namespace.


### Objetos '_First-Class_'

Na terminologia de linguagens de programação, objetos *_first-class_* são instancias de um tipo que pode ser atribuídos a um identificador, passado como um parâmetro ou retornado por uma função.

Em Python, também as fuções e as classes são tratados como objetos _first-class_.

### Modulos e Declaração de Importação

A declaração *_import_* carrega definições de um módulo para o namespace corrente.

Uma forma de importação usa a sintaxe:

```python
from math import pi, sqrt
```

O comando adiciona ambos `pi`e `sqrt` como definidos no módulo math ao namespace corrente.

Outra forma de importação usa a sintaxe:

```python
from math import *
```

que importa todas as funções do módulo math no namespace corrente e pode sobrescrever conteúdo do namespace atual - devemos tomar cuidado com este uso!


Outra ainda, usa a sintaxe

```python
import math
```

e, neste caso, o comando adiciona ambos o identificador `math` dentro do namespace corrente e todas as funções do módulo que agora devem ser acessadas como `math.pi`, por exemplo.

#### Criar um Módulo

É só salvar as definições em um arquivo com o sufixo .py e carregar usando as sintaxes apresentadas anteriormente.

Por exemplo, se colocamos todas as definições pertinentes no arquivo chamado utilidades.py, para carregá-las podemos usar a sintaxe from utilidades import funcao.


Existe uma construção especial para embarcar comandos dentro de módulos tal que eles so sejam executados se diretamente chamados como um script, mas que não executem quando o módulo é chamado de um outro script. Estes comandos devem ser colocados no corpo de uma declaração condicional como abaixo:

```python
    if __name__ == '__main__':
        #coloque o código aqui
``` 

#### Módulos importantes do Python

| Nome do Módulo | Descrição |
| --- | --- |
| array | provê armazenamento compacto de array para tipos primitivos |
| collections | Define estruturas de dados adicionais e classes base abstratas envolvendo coleções de objetos |
| copy | define funções gerais para fazer cópias de objetos |
| heapq | prove funções de priority-queue baseadas em heap |
| math | define constantes e funções matemáticas comuns |
| os | provê suporte a interação com o sistema operacional |
| random | prové geração de números aleatórios |
| re | provê suporte para processamento de expressões regulares |
| sys | provê um nível de interação adicional com o interpretador Python |
| time | provê suporte para medir tempo ou gerar atrasos em um programa |


#### Números Aleatórios no Python

O módulo `random`no Python provê a abilidade de geração de números pseudo-aleatórios - isto é, números que são estatisticamente aleatórios (mas não necessariamente aleatórios de verdade). O gerador de números aleatórios padrão do Python é o Mersenne twister. Ele não deve ser usado para aplicações como configurações de segurança do computador.

Funções presentes no módulo random:

|syntaxe | descrição|
| --- | --- |
|seed(hashable) | inicializa o gerador de números pseudo aleatórios baseado no valor do hash do parâmetro |
|random() | retorna um valor de ponto flutuante no intervalo [0.0, 1.0) | 
|randint(a,b) | retorna um inteiro pseudo-aleatório no intervalo fechado [a,b] |
|randrange(start, stop, step)|retorna um inteiro fseudo-aleatório no range indicado pelos parâmetros |
|choice(seq)|retorna um elemento da sequência escolido de forma pseudo-aleatória |
|shuffle(seq)|Reordena os elementos da sequencia de forma pseudo-aleatória |



