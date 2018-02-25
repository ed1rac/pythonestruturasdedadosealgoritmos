# Programação Orientada à Objetos

## Objetivos, Princípios e Padrões
Os atores centrais da programação orientada a objetos, como o próprio nome já diz, são os _objetos_.

Cada objeto é uma *_instância_* de uma *_classe_*.

Uma Classe declara de forma precisa e consistente o que esperar de uma instância da classe.

A definição da classe tipicamente especifíca _variáveis de instância_ (ou _data members_) - que dados o objeto contém - e os _métodos_ (ou _member functions_) - que o objeto pode executar.

### Objetivos do Projeto Orientado à Objetos

Implementações de software devem alcançar _robustez_, _adaptabilidade_ e _reusabilidadde_.

* Robustez: capaz de gerenciar entradas não experadas que não estão explicitamente definidas na aplicação. capaz de se auto-recuperar de estados de erro.
* Adaptabilidade: capaz de evoluir com o tempo em respostas à mudança de condições do ambiente. capaz de rodar com mudanças mínimas em outro hardware e outras plataformas.
* Reusabilidade: O mesmo código deve ser usável como um componente de siferentes sistemas em várias aplicações.

### Principios do Projeto Orientado à Objetos

Para facilitar os objetovos, os princípios são:

* Modularidade: refere-se a um princípio de organização no qual diferentes componentes do sistema de software são divididos em unidades funcionais separadas.
* Abstração: refere-se a refinar um sistema complicado até as suas partes mais fundamentais. É por este princípio que chegamos até as ADTs (Tipos abstratos de dados)
* Encapsulamento:Componentes diferentes de um sistema de software não devem revelar seus detalhes internos ou suas respectivas implementações.

#### ADTs e Interfaces

ADT especifica *_o quê_* cada operação faz, mas não *_como_* é feita. O conjunto de comportamentos suportados por um ADT é referido como sua *_interface pública_*

Sobre a especificação da interface, o Python tem a tradição de tratar as abstrações implicitamente usando um mecanismo conhecido como *_duck typing_*, no qual os programadores assumem que um objeto suporta uma série de comportamentos conhecidos, e que o interpretador lançará erros de run-time se estas premissas falharem.

Mais formalmente, Python suporta tipos abstratos de dados usando um mecanismo conhecido como uma *_abstract base class_* (ABC). Uma abstract base class não pode ser instanciada diretamente, mas ela define um ou mais métodos comuns que todas as implementações daquela abstração devem ter (e que devem ser realizadas apartir de uma ou mais *_classes concretas_*).

#### Encapsulamento e o seu suporte na linguagem Python

Como Python suporta fracamente o encapsulamento, fica como convenção que os nomes dos membros de uma classe que iniciam com um caractere de sublinhado ("_") são assumidos serem não-públicos e por isso não devemos nos basear neles.

Estas convenções são reforçadas pela omissão intencional destes métodos e membros da documentação gerada automaticamente.

### Design Patterns

Design pattern descreve uma solução para um problema "típico" de design de software.
Um pattern provê um template geral para uma solução que pode ser aplicada em diferentes situações.

Podem ser design patterns:

* de Algoritmos: recursão, amortização, divide-and-conquer, prune-and-search, Brute force, Dynamic programming, Métodos Gulosos, ...
* de Engenharia de software: Iterator, Adapter, Position, Composition, Template method, Locator, Factory method, ...

Vamos usar alguns destes métodos no livro.

## Desenvolvimento de Software

Os passos mais importantes no desenvolvimento de software são:

* Desenho: onde decidimos como dividir o funcionamento de nossos programas em classes, como estas classes interagem, que dados vão armazenar e que ações vão executar.
* Implementação: onde de fato escrevemos o código da solução
* Testes e Debugging: é o processo de checar experimentalmente a corretude de um programa, debugando-0 a fim de descobrir os seus erros.

Seguem algumas boas práticas para estes passos.

### Desenho

Alguns princípios importantes no Desenho do Software

* Responsabilidades bem definidas para cada ator do nosso sistema. Os atores se tornarão as classes.
* Independência - tanto quanto possível - do trabalho de cada classe em relação às outras
* Comportamento - definir de forma precisa os comportamentos de cada classe, pois eles definem os métodos/a interface daquela classe.

### Implementação

* Padrões de codificação: `CamelCase` para classes, `nomes_de_variáveis` separadas com sublinhado, `CONSTANTES` em caixa alta, `_variáveis_não_publicas` iniciadas com sublinhado, identação por 4 espaços.
* Literais string criam a documentação (\_docstring\_) das classes e métodos

### Testes e Debugging:

* Construir um plano de teste minuncioso
* Identificar e testar os casos de contorno das entradas (como entradas vazias, com um elemento, etc..)
* Identificar as condições especiais das estruturas usadas pelo programa (como inserção no início da lista, após o último elemento, etc...)
* Criar exemplos gerados aleatoriamente
* Verificar as dependências entre classes e funções do programa de forma top-down (com stubs) ou botton-up (a partir de testes unitários)
* Automatizar testes, usando o módulo unitttest do Python. Este framework permite agupar os casos de teste individuais em test suites maiores e prove suporte para execução, repeorting e análise dos resultados destes testes.



## Definições de Classe

Em python cada dado é representado como instância de alguma classe.

A classe serve como _blueprint_ para suas instancias, determinando o modo que o estado da informação é representado na forma de _atributos_.

TODO: Adicionar detalhes da documentação de classes no site [https://docs.python.org/3/tutorial/classes.html](https://docs.python.org/3/tutorial/classes.html)

A definição de classe começa com a palavra chave _class_ seguida pelo nome da classe, dois pontos, e pelo bloco identado de código que serve como o corpo da classe. 


### Exemplo

TODO: Extraído diretamente do Livro texto do Goodrich e colegas. Criar um exemplo bacana e colocar no lugar.

Segue o conteúdo que estaria no arquivo `credit_card.py`

```python
class CreditCard:
    """A consumer credit card"""
    
    def __init__(self, customer, banck, acnt, limit):
        """ Create a new credit card instance.

        The initial balance is zero

        customer    the name of the customer (e.g., 'John Snow')
        bank        the name of the bank (e.g., 'Mu-Bank')
        acnt        the account identifier (e.g., '4123 5437 4514 6735')
        limit       credit limit (medido em reais)
        """

        self._customer = customer
        self._bank = bank
        self._account = acnt
        self._limit = limit
        self._balance = 0

    def get_customer(self):
        """Return name of the customer."""
        return self._customer

    def get_bank(self):
        """Return the bank's name."""
        return self._bank

    def get_account(self):
        """Return the card identifying number (typically stored as a string)."""
        return self._account

    def get_limit(self):
        """Return current credit limit."""
        return self._limit

    def get_balance(self):
        """Return current balance."""
        return self._balance

    def charge(self, price):
        """Charge given price to the card, assuming sufficient credit limit.

        Return True if charge was processed; False if charge was denied.
        """
        if price + self._balance > self._limit:  # se a cobrança irá exceder o limite
            return False                         # não pode aceitar a cobrança
        else:
            self._balance += price
            return True

    if __name__ == '__main__':
        wallet = []
        wallet.append(cc = CreditCard('Joao Américo', 'Meu Banco', '5341 2356 3466 4253', 2500))
        wallet.append(cc = CreditCard('Joao Américo', 'Outro Banco', '1234 4352 4523 1234', 3500))
        wallet.append(cc = CreditCard('Joao Américo', 'Banco Três', '3464 5637 7864 3253', 5000))
``
        for val in range(1, 17):
            wallet[0].charge(val)
            wallet[1].charge(2*val)
            wallet[2].charge(3*val)`

        for c in range(3):
            print('Customer = ', wallet[c].get_customer())
            print('Bank = ', wallet[c].get_bank())
            print('Account = ', wallet[c].get_account())
            print('Limit = ', wallet[c].get_limit())
            print('Balance = ', wallet[c].get_balance())
            while wallet[c].get_balance() > 100:
                wallet.make_payment(100)
                print('New balance = ', wallet[c].get_balance)
            print()
```

### O construtor

```python
cc = CreditCard('Joao Américo', 'Meu Banco', '5341 2356 3466 4253', 1000)
```

Internamente isto resulta na chamada do método `__init__` que serve como o construtor da classe.

É responsável por setar o estado inicial da instância, com os valores apropriados em cada variável de instância.

Note que no código a seguir dizemos que a variável `_customer` é *_qualificada_* pelo *_self_* e por isso pertence à intância que temos em mãos, e a variável `customer` é não qualificada, por isso pertence ao namespace local da função `__init__()`

```python
self._customer = customer
```

### O Identificador *`self`*

Sintaticamente, _self_ identifica a instância sobre a qual o método é invocado. Usamos no código de duas formas:

1. Para declarar métodos de instância, como a seguir

``` python
def charge(self, price);
```

1. Para recuperar variáveis de instância ou para chamar um método da insância, como a seguir

```python
if price + self._balance > self._limit

cc = CreditCard('Joao Américo', 'Meu Banco', '5341 2356 3466 4253', 1000)
cc.ccharge(123.43)
```

### Encapsulamento

Por convenção os métodos que iniciam com sublinhado ("_") são métodos não públicos.

### Overload de operadores e métodos especiais do Python

Por padrão o operado `+` não é definido para uma classe nova. Entretanto, é possível o autor de uma classe nova prover a definição usando uma técnica que se chama *_overload de operadores_*. Isto é feito implementando um método com um nome especial.

Em Python, a sintaxe a + b é convertida a uma chamada de método na forma `a.__add__(b)`.

Quando um operador binário é aplicado a duas instâncias de tipos diferentes, como em `3 * 'texto'` o Python dá prioridade a classe do operando da _esquerda_ - nesse caso usando o a implementação `__mul__` da classe `int`.

Se a classe da esquerda não implementa tal comportamento, Python busca na definição de classe da direita - na classe `string` - pela definição de um _operador pela direita_ (chamado de _right hand operator_ em inglês). Neste caso a classe string deve implementar a função `__*r*mul__`.

Note que a distinção entre `__mul__` e `__rmul__` também permite que a semântica implementada seja diferente em alguns casos.

### Overload de funções que não são operadores

Há também outras funções especiais que permitem overload e são bastante úteis para nós que vamos implementar estruturas de dados em Python:

| Sintaxe comum | Forma do método especial |
| --- | --- |
| a + b | a.__add__(b); alternativamente b.__radd(a) |
| a - b | a.__sub__(b); alternativamente b.__rsub(a) |
| a * b | a.__mul__(b); alternativamente b.__rmul(a) |
| a / b | a.__truediv__(b); alternativamente b.__rtruediv(a) |
| a // b | a.__floordiv__(b); alternativamente b.__rfloordiv(a) |
| a % b | a.__mod__(b); alternativamente b.__rmod(a) |
| a ** b | a.__pow__(b); alternativamente b.__rpow(a) |
| a << b | a.__lshift__(b); alternativamente b.__rlshift(a) |
| a >> b | a.__rshift__(b); alternativamente b.__rrshift(a) |
| a & b | a.__and__(b); alternativamente b.__rand(a) |
| a | b | a.__or__(b); alternativamente b.__ror(a) |
| a ^ b | a.__xor__(b); alternativamente b.__rxor(a) |
| a += b | a.__iadd__(b); alternativamente b.__riadd(a) |
| a -= b | a.__isub__(b); alternativamente b.__risub(a) |
| a *= b | a.__imul__(b); alternativamente b.__rimul(a) |
| a ...= b | a.__i...__(b); alternativamente b.__ri...(a) |
| +a | a.__pos__() |
| -a | a.__neg__() |
| ~a | a.__invert__() |
| abs(a) |a.__abs__()|
| a < b |a.__lt__(b)|
| a <= b |a.__le__(b)|
| a > b |a.__gt__(b)|
| a >= b |a.__ge__(b)|
| a == b |a.__eq__(b)|
| a != b |a.__neq__(b)|
| v in a |a.__contains__(v)|
| a[k] = v |a.__setitem__(k, v)|
| del a[k]  |a.__delitem__(k)|
| a(arg1, arg2, ...)  |a.__call__(arg1, arg2, ...)|
| len(a) |a.__len__()|
| hash(a) |a.__hash__()|
| iter(a) |a.__iter__()|
| next(a) |a.__next__()|
| bool(a) |a.__bool__()|
| float(a) |a.__float__()|
| int(a) |a.__int__()|
| repr(a) |a.__repr__()|
| reversed(a) |a.__reversed__()|
| str(a) |a.__str__()|

### Implied Methods

Há métodos que tem implementação padrão do Python dado que outros métodos estejam implementados. É o caso do método especial `__iter__`: se a classe provê métodos tanto para `__len__` e `__getitem__`, um iterador padrão é automaticamente provido pelo Python. Ainda mais, uma vez que um iterador existe, você também ganha de graça o método `__contains__`.

Outro ponto importante é que a implementação de alguns métodos como `__eq__` não implicam que o Python vai prover implicitamente o método complementar, `__neq__`. Você deve implementar os dois.


### Exemplo: Classe de vetor multidimensional

```python
v = Vector(5)           # constrói o vetor 5-dimensional <0, 0, 0, 0, 0>
v[1] = 23               # <0, 23, 0, 0, 0> (via __setitem__)
v[-1] = 45              # <0, 23, 0, 0, 45> (também via __setitem__)
print([4])              # print 45 (via __getitem__)
u = v + v               # <0, 46, 0, 0, 90> (via __add__)
print(u)                # print <0, 46, 0, 0, 90>
total = 0
for entrada in v:       # iteração implicita via __len__ e __getitem__
    total += entrada
```

Exemplo da Classe Vetor multi dimensional

```python
class Vector:
    """Representa um vetor multidimensional no espaço"""
    
    def __init__(self, d):
        """Cria um vertor d dimensional de zeros"""
        self._coords = [0] * d

    def __len__(self)
        """Retorna a dimensão do vetor"""
        return (len(self._coords))

    def __getitem__(self, k):
        """Retorna a k-ésima coordenada do vetor"""
        return self._coords[k]

    def __setitem__(self, k, v):
        """Seta a k-esima coordenada do vetor para um dado valor"""
        self._coords[k] = v

    def __add_(self, outro):
        """Retorna a soma de dois vetores"""
        if len(self) != len(other):                         # se apóia no método __len__
            raise valueError('as dimensões devem ser as mesmas')
        result = Vector(len(self))                          # inicia um vetor de zeros
        for k in range(len(self)):
            result[k] = self[k] + other[j]
        return result

    def __eq__(self, outro):
        """Retorna True se o vetor é igual ao outro"""
        return self._coords == other._coords

    def __neq__(self, outro):
        """Retorna True se o vetor é diferente do outro"""
        return not self.__eq__(outro)                # se baseia na definição de __eq__ já existente

    def __str__(self):
        """Produz uma representação do vetor em texto"""
        return '<' + str(self._coords)[1:-1] + '>' #adapta a representação da lista
```

### Iteradores

Para resumir, *_iterator_* para uma sequência provê um método chave especial, chamado `__next__` que retorna o próximo elemento da coleção. Se não há mais elementos então ele levanta uma exceção _StopIteration_.

Segue abaixo uma implementação simples.

Note que o Python já provê automaticamente uma implementação de iterador para qualquer classe que define ambos `__len__` e `__getitem__`.

```python
class SequenceIterator:
    """Um iterador para qualquer tipo sequência do Python"""

    def __init__(self, sequence):
        """Cria um iterador para a sequência dada"""
        self._seq = sequence            # mantem a referencia para o dado original
        self._k = -1                    # iremos incrementar para 0 na primeira chamada do next

    def __next__(self):
        """Retorna o próximo elemento ou lança o erro StopIteration"""
        self._k +=1
        if self._k < len(self._seq):
            return(self._seq[self._k])  # retorna o elemento
        else:
            raise StopIteration()       # não há mais elementos

    def __iter__(self):
        """Por convenção o iterador deve retornar ele mesmo como uma instância de iterador"""
        return self
```

### Range: Uma outra implementação de Exemplo

```python
for x in range(1, 10, 2):

```

```python
class Range:
    """Uma classe que copia a classe built-in range"""

    def __init__(self, start, stop=None, step=1):
        """Inicializa uma instância Range
        
        Semântica é similar ao da classe built-in range
        """
        if step == 0:
            raise ValueError('step não pode ser 0')
        
        if stop is None:                # caso especial de range(n)
            start, stop = 0, start      # deve ser tratado como range(0, n)

        #calcula o tamanho efetivo apenas uma vez
        self._length = max(0, (stop - start + step - 1) // step)

        # precisamos gravar o start e o step (mas não o stop) para suportar o método __getitem__
        self._start = start
        self._step = step

    def __len__(self):
        """Retorna o número de entradas no range"""
        return self._length
        
    def __getitem__(self, k):
        """Retorna a entrada no índice k (usando a interpretação standard se negativo)"""
        if k < 0:
            k += len(self)              # tenta converter o índice negativo

        if not 0 <= k < self._length:
            raise IndexError('index fora do range')

        return self._start + k * self._step
```


## Herança

Um projeto hierárquico é útil para o desenvolvimento de software:

* funções comuns podem ser agrupadas no nível mais geral - promovendo reuso de código
* comportamentos diferentes podem ser implementados nos níveis mais específicos - via especialização de um comportamento padrão através de um _override_ ou via extensão da superclasse ao prover métodos completamente novos à classe mais geral.


Na terminologia de orientação a objetos, uma classe mais geral é denomidada *_base class_*, *_parent class_* ou *_superclass_*, enquanto a classe mais específica ue deriva da mais geral é conhecida como *_subclass_* ou *_child class_*.

## Namespaces e Orientação de Objetos

## Cópia _Shallow_ e _Deep_