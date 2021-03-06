![Curso - JavaScript Super Saiyajin](http://i.imgur.com/jGXoRO6.png)

# Aula 01 - Conhecendo funções

## O que é uma função?

<br>

> **f( x ) = y**

<br>

> Uma função ou aplicação é uma relação de um conjunto `A` com um conjunto `B`.

*fonte: [Função (matemática) - Wikipedia](https://pt.wikipedia.org/wiki/Fun%C3%A7%C3%A3o_(matem%C3%A1tica))*

<br>

![](https://upload.wikimedia.org/wikipedia/commons/thumb/0/07/Venn_diagram_of_a_function.svg/450px-Venn_diagram_of_a_function.svg.png)

<br>

Podemos imaginar que o conjunto `A` é o conjunto dos valores dos nossos <br>
parâmetros e o conjunto `B` é o conjunto dos valores dos resultados.

Logo essa relação entre esses dois conjuntos pode também ser<br> 
uma transformação, filtragem, etc. Por exemplo:


![](http://clubes.obmep.org.br/blog/wp-content/uploads/2015/11/separado.png)

Nesse caso temos duas funções:

- uma filtra os números pares;
- a outra filtra os números ímpares;

Essas duas funções utilizam o mesmo conjunto de entrada, o conjunto dos números Naturais e suas respostas são **sub-conjuntos** dos números Naturais.

> Você sabe que temos outros conjuntos numéricos também né?!


- Conjunto dos Naturais;
- Conjunto dos Inteiros;
- Conjunto dos Racionais;
- Conjunto dos Irracionais;
- Conjunto dos Reais ;



## Entendendo as operações matemáticas básicas

> Na lógica matemática e na ciência da computação, lambda cálculo , também escrito como cálculo-λ é um sistema formal que estuda funções recursivas computáveis, no que se refere a teoria da computabilidade, e fenômenos relacionados, como variáveis ligadas e substituição. Sua principal característica são as entidades que podem ser utilizadas como argumentos e retornadas como valores de outras funções.
> 
> A parte relevante de lambda cálculo para computação ficou conhecida como lambda cálculo não-tipado. O lambda cálculo tipado e o não-tipado tem suas ideias aplicadas nos campos da lógica, teoria da recursão (computabilidade) e linguística, e tem tido um grande papel no desenvolvimento da teoria de linguagens de programação (com a versão não-tipada sendo a inspiração original para programação funcional, em particular Lisp...
> 
> ...
> 
> Como os nomes de funções são uma mera conveniência, o lambda cálculo não tem interesse em nomear uma função. Já que todas as funções esperando mais de um argumento podem ser transformadas em funções equivalentes recebendo uma única entrada (via Currying), o lambda cálculo não tem interesse em criar funções que aceitam mais de um argumento. 

*fonte: [Cálculo lambda - Wikipedia](https://pt.wikipedia.org/wiki/C%C3%A1lculo_lambda)*

<br>

### Reduzindo à apenas uma operação

<br>
<br>

> **Você já pensou que qualquer operação matemática pode ser**<br>
> **reduzida apenas em soma e subtração???**


<br>
<br>

![](http://geradormemes.com/media/created/vuaeem.jpg)

<br>
<br>


> Vou dar uma dica: pode usar apenas soma e números **negativos**!

> Dica matadora essa né?


<br>
<br>

Você pode usar número negativo pois seu sinal é<br> 
[representado por 64 bits, sendo apenas 1 para seu sinal](http://www.2ality.com/2012/04/number-encoding.html).

<br>
<br>

![](http://i.imgur.com/lXqXj6A.png)

<br>
<br>

Então vamos pensar:

```js
5-4=1
5+4=9
5+(-4)=1 
```

É nessa hora que você lembra do Ensino Médio e a regra de sinais:

> número negativo com número negativo (1° caso)

> número positivo com número positivo (2° caso)

> número negativo com número positivo ou vice-versa (3° caso)


Primeiro caso:

> Quando temos dois números negativos repetimos o sinal de subtração e somamos esses dois números. 


```
-12 + -8 = - (12 + 8) = - 20
-10 + -16 = - (10 + 16) = - 26
-15 + -2 = - (15 + 2) = - 17
-11 + -46 = - (11 + 46) = - 57
```


Segundo caso:

> Quando temos dois números positivos repetimos o sinal de adição e somamos esses dois números. 

```
+12 + 8 = + (12 + 8) = + 20
+10 + 16 = + (10 + 16) = + 26
+15 + 2 = + (15 + 2) = + 17
+11 + 46 = + (11 + 46) = + 57
```


Terceiro caso:

> Quando temos um número negativo e outro positivo ou vice-versa devemos repetir o sinal do maior número em módulo e depois devemos subtrair o maior número (em módulo) pelo menor número (também em módulo). 

> O módulo de um número nada mais é do que pegar o valor positivo desse número. O módulo é representado por duas barras dispostas uma no início e outra no fim do número. |-2| === 2


```
+12 + -8 = + (|12| - |-8|) = 4 
+10 + -16 = - (|-16| - |10|) = - 6
+15 + -2 = + (|15| - |-2|) = + 13
+11 + -46 = - (|-46| - |11|) = - 35
```

<br>
<br>

> **A partir desse terceiro caso já matamos a charada!**

<br>
<br>

- soma: 
  - ( x, y ) => x + y 
  - ( y ) => ( x ) => x + y 
- subtração:
  - ( x, y ) => soma( x, -y ) 
  - ( y ) => ( x ) => soma( x )( -y ) 
  + invertendo essa operação
- multiplicação: ( utilizando apenas a soma )
  - ( x, y ) => x * y 
  - ( y ) => ( x ) => ...
  + invertendo essa operação
- divisão: ( utilizando apenas a soma )
  - ( x, y ) => x / y 
  - ( y ) => ( x ) => ...
  + invertendo essa operação


Demonstrando com código:

```js

const sum = ( x, y ) => x + y 
const sumParcial = ( y ) => ( x ) => x + y 

const minus = ( x, y ) => sum( x, -y ) 
const minusParcial = ( y ) => ( x ) => sumParcial( -y )( x ) 

```

> **Entendeu o porquê estou mostrando como criar essas operações**<br>
**básicas onde recebo apenas um parâmetro por vez?**

> Lembrando que nós só poderemos usar funções que re-usem outras!

<br>

Caso você ainda não tenha entendido ainda irei demonstrar praticamente.

Imagine que você quer ter uma função que sempre multiple por `2` qualquer valor.

```js

const double = ( x ) => x * 2

```

Podemos facilmente criar uma função para reaproveitar isso, dessa forma:


```js

const times = ( y ) => ( x ) => x * y
const double = times( 2 )
const triple = times( 3 )
const tenTimes = times( 10 )

```

<br>


> Agora vamos fazer uma que multiplique por 3 e outra por 10.

```js

const times = ( y ) => ( x ) => x * y
const double = times( 2 )
const triple = times( 3 )
const tenTimes = times( 10 )

```


<br>

> **Muito simples né?**

Perceba que quebramos uma função que possuía dois parâmetros<br>
em outras duas funções que recebem apenas um parâmetro cada.


<br>
<br>

> **Então agora vamos escrever essa mesma função usando apenas a soma!**

<br>
<br>

Para isso precisamos entender o **algoritmo** da multiplicação:

```

Receba x e y
Pegue o valor de x e some nele mesmo y vezes.


```

Traduzindo para JavaScript:


```js

const times = ( y ) => ( x ) => {

  let result = 0

  while ( y > 0 ) { // ( y )
    result += x
    y--
  }

  return result
}

console.log('3 times 4', times( 4 )( 3 ) )

```

#### Reduzindo a multiplicação para a soma

```js

const sum = ( y ) => ( x ) => x + y

const times = ( y ) => ( x ) => {

  let result = 0

  const sumX = sum( result )

  while ( y > 0 ) { // ( y )
    result += sumX( x )
    y--
  }

  return result
}

console.log('3 times 4', times( 4 )( 3 ) )

```

<br>
<br>

> **Conseguiu entender o [`while`](http://mdn.io/while)?**

<br>
<br>

Ele é uma função de *looping* assim como o [`for`]() e o [`do while`], porém<br>
é diferente de funções iteradoras como:

- [map](http://mdn.io/map);
- [filter](http://mdn.io/filter);
- [reduce](http://mdn.io/reduce);
- [forEach](http://mdn.io/forof);
- [for in](http://mdn.io/forin);
- [for of](http://mdn.io/forof);
- etc

A diferença entre esses dois tipos de funções é que as funções de<br>
*looping* não precisam de uma estrutura de dados como base para iterar.
Já as de iteração necessitam de uma estrutura iterável.

Mostrai o mesmo exemplo com algumas dessas funções.

Imagine que temos um *Array* de Objetos e precisamos antes de somar<br>
os salários retirar 10% do valor de cada um e depois fazer uma média.

```js

const workers = [ 1000, 2500 , 10000 ]

const withdraw = ( list, percent ) => {

  let counter = 0
  let newList = []

  while ( counter < list.length) {
    const percentValue = list[ counter ] * ( percent / 100 )
    const newSalary = list[ counter ] - percentValue

    newList[ counter ] = newSalary 
    counter++
  }

  return newList
}

console.log( 'New Salaries: ', withdraw( workers, 10 ) )

```

No código acima nós apenas criamos um *Array* novo com os valores<br>
dos valores calculados pela nossa função

```js

const workers = [ 1000, 2500 , 10000 ]

const sumAll = ( list, percent ) => {

  let counter = 0
  let total = 0

  while ( counter < list.length) {
    const percentValue = list[ counter ] * ( percent / 100 )
    const newSalary = list[ counter ] - percentValue

    total += newSalary 
    counter++
  }

  return total
}

console.log( 'Sum of Salaries: ', sumAll( workers, 10 ) )

```

### Lembrete 1

> Percebeu que não criamos **funções** porém não criamos nenhuma constante <br>
> para os valores que passaremos como parâmetro?

Isso se deve graças a dois conceitos que são obrigatórios para uma linguagem <br> estar contida no Paradigma Funcional:

- [First-class Function]()
- [High-Order Function]()

**Falarei melhor sobre esses conceitos na próxima aula!**

## Desafio

Criar a função de divisão utilizando apenas a função de soma, <br>
onde ela receba 2 valores inteiros e consiga retornar um <br>
valor decimal. Por exemplo: `5 / 2 = 2.5`

Além disso explique como dois valores do conjunto dos Números Naturais<br>
transformou-se em um valor que não está contido nesse grupo e qual o grupo que ele pertence.

> **Lembrando que a ÚNICA função aceita dentro da divisão será a da soma!**




###### Oozaru

![](http://i.imgur.com/kPZOvNa.png)

Como demonstrei anterioremente, utilizamos funções<br>
anônimas, que definimos em constantes, pois isso nos remetei ao [Cálculo lambda](https://pt.wikipedia.org/wiki/C%C3%A1lculo_lambda) que é a base da <br>
Programação Funcional.

Logo preciso também lhe mostrar do outro jeito, usando `function`.

> Por isso a `function` está na seção ***Oozaru***! Pois você pode<br>
> usar mas **EU** não lhe aconselho.
> 


<br>
<hr>
<br>
