Primeiro você precisa baixar [The Haskell PLataform](https://www.haskell.org/platform/) para seu sistema operacional e depois de instalado vamos para o terminal rodar o [cabal](https://www.haskell.org/cabal/), que é um tipo de NPM para o Haskell:

```
cabal

**********************************************************************

=== Configuration for cabal has been written to
    /Users/jeancarlonascimento/.cabal/config

=== Executables will be installed in:
    /Users/jeancarlonascimento/Library/Haskell/bin

    You may wish to place this on your PATH by adding the following
    line to your ~/.bash_profile:

    export PATH="$HOME/Library/Haskell/bin:$PATH"

=== When documentation is built, a master index to all documentation
    will be placed in:

    /Users/jeancarlonascimento/Library/Haskell/doc/index.html

    You may wish to bookmark that file once it gets built (after the
    first cabal install).

**********************************************************************

Downloading the latest package list from hackage.haskell.org
Note: there is a new version of cabal-install available.
To upgrade, run: cabal install cabal-install
cabal: no command given (try --help)

```

{<2>}![](http://www.game-art-hq.com/wp-content/uploads/2013/01/Kabal-MK9-Render.png)

Depois instalamos o `cabal-install`:

```
cabal install cabal-install
Resolving dependencies...
Downloading Cabal-1.22.0.0...
Configuring Cabal-1.22.0.0...
Installed Cabal-1.22.0.0
Downloading cabal-install-1.22.0.0...
Configuring cabal-install-1.22.0.0...
Building cabal-install-1.22.0.0...
Installed cabal-install-1.22.0.0
Updating documentation index
/Users/jeancarlonascimento/Library/Haskell/share/doc/index.html

```

Vou começa a seguir esse conteúdo [http://learnyouahaskell.com/](http://learnyouahaskell.com/). Então para rodarmos seu interpretador vamos rodar o [ghci](https://downloads.haskell.org/~ghc/latest/docs/html/users_guide/ghci.html) no terminal.

```
ghci
GHCi, version 7.8.3: http://www.haskell.org/ghc/  :? for help
Loading package ghc-prim ... linking ... done.
Loading package integer-gmp ... linking ... done.
Loading package base ... linking ... done.
Prelude> 400 + 20
420
Prelude> 210 *2
420
Prelude> 840 / 2
420.0
Prelude> (50 * 100) - 4999
1
Prelude> 50 * 100 - 4999
1
Prelude> 50 * (100 - 4999)
-244950
```

Por enquanto nada de novo correto? Agora vamos ver como são escritos os booleanos: `true` e `false`:

```
Prelude> True 
True
Prelude> False
False
Prelude> True && False
False
Prelude> True || False
True
Prelude> not False
True
Prelude> not (True && True)
False
Prelude> 
```

Notou que estão em **maiúscula** e também o uso do `not`? Diferentemente do Javascript onde usamos minúsucla e o operador `!` para negação. Olha o que acontece se você tentar usar `true` ou `false`:

```
Prelude> true

<interactive>:15:1: Not in scope: ‘true’
Prelude> false

<interactive>:16:1: Not in scope: ‘false’
Prelude> 

```

Agora vamos fazer teste de igualdade entre valores:

```
Prelude> 5 == 5
True
Prelude> 1 == 0
False
Prelude> 5 /= 5
False
Prelude> 5 /= 4
True
Prelude> "nomadev" == "nomadev"
True
```

Bom o operado `==` todos conhecemos como comparador de igualdade, porém temos o operador `/=` que compara se os valores são diferentes, assim como fazemos com `!==` no Javascript.

E se eu tentar somar 2 tipos de valores diferentes terei um erro como o abaixo:

```
Prelude> 5 + "nomadev"

<interactive>:26:3:
    No instance for (Num [Char]) arising from a use of ‘+’
    In the expression: 5 + "nomadev"
    In an equation for ‘it’: it = 5 + "nomadev"
```

Nesse caso o erro acontece pois os operadores aritméticos aceitam valores numéricos, diferentemente do Javascript onde podemos fazer:

```
> "5" + 5
'55'
```

E o Javascript irá concatenar o 5 como uma String, vamos ver outra parte interessante é a comparação, já que em Javascript podemos comparar qualquer tipo de valor, vamos ver em Haskell antes:

```
Prelude> 1 == "suissa"

<interactive>:27:1:
    No instance for (Num [Char]) arising from the literal ‘1’
    In the first argument of ‘(==)’, namely ‘1’
    In the expression: 1 == "suissa"
    In an equation for ‘it’: it = 1 == "suissa"

Prelude> 1 == True

<interactive>:28:1:
    No instance for (Num Bool) arising from the literal ‘1’
    In the first argument of ‘(==)’, namely ‘1’
    In the expression: 1 == True
    In an equation for ‘it’: it = 1 == True

Prelude> 1 == "1"

<interactive>:29:1:
    No instance for (Num [Char]) arising from the literal ‘1’
    In the first argument of ‘(==)’, namely ‘1’
    In the expression: 1 == "1"
    In an equation for ‘it’: it = 1 == "1"

```

Agora vamos ver no Javascript:

```
> 1 == "suissa"
false
> 1 == true
true
> 1 == "1"
true
```

Isso se deve ao operador `==` comparar apenas os valores, sem comparar os tipos, para corrigir isso precisamos usar o operador `===` em Javascript:

```
> 1 === "suissa"
false
> 1 === true
false
> 1 === "1"
false

```


Vamos voltar às operações aritméticas, se você lembrar anteriormente fizemos usamos o seguinte cálculo: `400 + 20`, onde o `+` é um função que aceita 2 número e os soma, como visto usamos ela no meio dos 2 valores, essa forma é chamada de função *infix*. A maioria das funções não aritméticas usam funções *prefix*, ou seja, vem antes do valor passado para ela, como visto abaixo:

```
Prelude> succ 8
9
```

A função `succ` recebe um valor e retorna seu sucessor. Como visto passamos um parâmetro para a função apenas separando ele da função com espaço. 

**- E caso eu tenha vários parâmetros?** 

Bom ai basta fazer a mesma coisa, vamos ver os seguintes exemplos:

```
Prelude> min 9 10
9
Prelude> min 3.4 3.2 
3.2
Prelude> max 100 101
101
```

As funções de aplicação como vistas acima possuem maior precedência, logo as 2 formas abaixo estão corretas:

```
Prelude> succ 9 + max 5 4 + 1
16
Prelude> (succ 9) + (max 5 4) + 1
16
```


Entretanto, se nós quisermos o sucessor do produto dos números 9 e 10, nós não podemos escrever `succ 9 * 10` porque ele irá pegar o sucessor de 9, o qual será multiplicado por 10. Para pegar o sucessor do produto entre 9 e 10 precisamos escrever assim: `succ (9 * 10)`.

```
Prelude> succ 9 * 10
100
Prelude> succ (9 * 10)
91
```

No Javascript nós não precisamos nos preocupar já que os parâmetros precisam ser passados via (), podemos fazer uma analogia com o seguinte código:

```
> function succ(x) { return x+1; }
undefined
> succ(9)
10
> succ(9) * 10
100
> succ(9*10)
91
```

Se uma função recebe 2 parâmetros nós também podemos chamar a função da forma *infix* chamando dentro de \` \`, backticks. Vamos usar a função `div` como exemplo:

```
Prelude> 840 `div` 2
420
Prelude> div 840 2
420
```

Na próxima parte iremos ver como criar nossas próprias funções.
