---
layout: page
title:  "Ruby"
date:   2016-11-30 20:20:00 -0300
categories: aula
---

Ruby é uma linguagem de programação dinâmica, interpretada e orientada a objetos, desenvolvida na década de 1990 por Yukihiro "Matz" Matsumoto no Japão.

## Como usar esta página

Esta página contém vários editores de código, que você pode editar e rodar.

A saída do código é exibida no console de desenvolvimento do seu navegador. Para abrir o console, tecle `Ctrl+Shift+I` (Chrome ou Firefox) e clique na aba `Console`.

Para rodar o código de um editor, você pode clicar no botão "Rodar" ou então clicar sobre o código e teclar `Ctrl+Enter`.

O código Ruby é rodado remotamente, então pode demorar um pouco para o resultado aparecer.

Você pode acessar um editor aprimorado em <https://repl.it/languages/ruby>.

## Começando

### Alô, mundo!

{:.editor}

```ruby
puts 'Alo, mundo!'
```

O método `puts` recebe como argumento uma string e imprime essa string.

Os **parênteses são opcionais** na chamada de métodos (contanto que a expressão não se torne ambígua). Portanto, a expressão acima pode ser escrita como `puts('Alo, mundo!')`.

As strings podem ser escritas com aspas simples -- `'` -- ou aspas duplas -- `"`.

### Tudo é um objeto

Todos os valores (strings, números, `true`, dentre outros) são objetos; portanto, pode-se chamar métodos.

{:.editor}

```ruby
# Isto é um comentário

puts -42.abs
puts 123.class
puts "copo\nd'agua".upcase
```

### Conversão de tipos

{:.editor}

```ruby
# .to_s converte para string
puts "20" + 17.to_s
# .to_i converte para inteiro
puts "20".to_i + 17
# .to_f converte pra float
puts "10".to_f / 3
# Somar string com número resulta em erro
puts "20" + 17
```

### Toda operação é uma chamada de método

Toda operação é uma chamada de método e retorna um valor. Por exemplo, `1 + 3` é apenas uma forma conveniente de escrever `1.+(3)`, ou seja, chamar o método `+` do objeto `1` passando `3` como parâmetro.

{:.editor}

```ruby
puts 1.+(3)
puts 1 + 3
puts 2 == 2
puts 2.==(2)
```

Em Ruby, todos os métodos possuem um valor de retorno, mesmo que seja `nil` (equivalente ao `null` do Java). Compare com Java, em que há métodos que não possuem retorno (`void`).

### Variáveis e constantes

Variáveis começam com letra minúscula. Constantes começam com letra maiúscula:

{:.editor}

```ruby
# Variável
contador = 0
contador += 1

# Constante
PI = 3.14159
PI = 2       # resulta em warning
```

Variáveis globais começam com `$`.

## Alguns tipos de dados

### Strings

Há várias formas de definir strings em Ruby:

{:.editor}

```ruby
a = "\nThis is a double-quoted string\n"
a = %Q{\nThis is a double-quoted string\n}
a = %{\nThis is a double-quoted string\n}
a = %/\nThis is a double-quoted string\n/
a = <<-BLOCK

This is a double-quoted string
BLOCK
```

Strings suportam interpolação de variáveis:

{:.editor}

```ruby
valor = 3.14159
puts "pi é igual a #{valor}"
```

A expressão `#{xyz}`, em uma string, é substituida pelo valor da expressão `xyz`. Também pode-se usar expressões mais complexaS:

{:.editor}

```ruby
nome = "mundo"
puts "ALO, #{nome.upcase}"
```

### Símbolos

Símbolos são como strings, porém imutáveis, isto é, não podem ser modificados uma vez criados. Eles são geralmente usados como identificadores ou valores de enumerações em um programa e, nesses casos, símbolos são mais eficientes que strings. Símbolos são iniciados por `:`. Exemplo:

{:.editor}

```ruby
nome_pessoa1 = "Joao"
sexo_pessoa1 = :masculino

nome_pessoa2 = "Maria"
sexo_pessoa2 = :feminino
```

### Arrays

Arrays podem misturar elementos de diferentes tipos, inclusive outros arrays:

{:.editor}

```ruby
a = [1, 'hi', 3.14, 1, 2, [4, 5]]

puts a[2]             # => 3.14
puts a.[](2)          # => 3.14
p a.reverse        # => [[4, 5], 2, 1, 3.14, 'hi', 1]
p a.flatten.uniq   # => [1, 'hi', 3.14, 2, 4, 5]
```

Use o método `p` no lugar de `puts` para imprimir um valor em um formato mais adequado para *debugging*. `p x` é equivalente a `puts x.inspect`.

### Hashes

Hashes são estruturas chave-valor, também chamadas em outras linguagens de mapas ou arrays associativos.

{:.editor}

```ruby
# Hashes são delimitados por { e }
# {} representa um hash vazio
pessoa = {}

pessoa = { :nome => 'Joao', :idade => 18, :sexo => :masculino }
puts pessoa[:nome]

# Alterando o valor associado a uma chave
pessoa[:nome] = 'Jose'
puts pessoa[:nome]

# É muito comum usar símbolos como chaves 
# A partir do Ruby 1.9, há uma sintaxe alternativa
# para hashes que usam símbolos como chaves:

pessoa = { nome: 'Joao', idade: 18, sexo: :masculino }
```

## Algumas estruturas

### if-then-else

{:.editor}

```ruby
idade = 17

if idade < 16
  puts 'não pode votar'
elsif idade < 18
  puts 'não pode dirigir'
else
  puts 'já é adulto'
end
```

### if e unless em uma linha

{:.editor}

`unless` é o contrário de `if`, e significa "a não ser que".

Tanto `if` quanto unless podem ser usados no final de uma instrução:

```ruby
nome = 'Maria'
idade = 17

puts "Bem-vinda, #{maria}."
puts 'Acesso negado.' if idade < 18

puts "Bem-vinda, #{maria}."
puts 'Acesso negado.' unless idade >= 18
```

### Blocos

Blocos são trechos de código que você pode passar para algum método. Há duas formas de escrever blocos:

```ruby
# Uma linha
{ |x| puts x }
```

```ruby
# Várias linhas
do |x|
  puts x
end
```

O `|x|` é opcional. Entre `|` e `|`, fica a lista de parâmetros do bloco, separados por vírgulas.

Exemplos de uso:

{:.editor}

```ruby
3.times do
  puts "Alo mundo"
end

[3, 1, 4].each do |num|
  puts num
end

hash = {a: 1, b: 2, c: 3}
hash.each_pair { |k, v| puts "#{k} = #{v}" }
```

## Organizando o código

### Métodos

Use `def` para definir métodos. Enquanto não vemos classes ou módulos, todos os métodos que definirmos serão métodos do módulo `Kernel`. Exemplo:

{:.editor}

```ruby
# Vamos definir o método alo
def alo
  puts "Alo, mundo!"
end

# Agora, vamos chamar o método duas vezes
alo
alo
```

Note que para chamar um método, basta escrever o nome dele. Você até poderia escrever `alo()`, como em Java, mas os parênteses em Ruby são opcionais nesse caso, e na prática ninguém usa parênteses para chamar métodos sem parâmetros.

### Métodos com argumentos

{:.editor}

```ruby
# Note que o parâmetro pontuacao é opcional;
# se não for passado, assume-se o valor padrão, "!"
def alo(nome, pontuacao = "!")
  puts "Alo, #{nome}#{pontuacao}"
end

# Chamada
alo("mundo", "!")
alo("Terra", ".")
```

Os parênteses na chamada à função `alo` são opcionais.

## Valor de retorno

O valor da última expressão executada no método é retornado.

{:.editor}

```ruby
def soma(a, b)
  a + b
end

puts soma(2, 3)
```

### Métodos cujo parâmetro é um hash

Quando o último parâmetro de um método é um hash, há uma forma conveniente de chamar o método:

{:.editor}

```ruby
def mostra_pessoa(nome, dados)
  puts "Dados de #{nome}:"
  dados.each_pair do |chave, valor|
    puts "- #{chave}: #{valor}"
  end
end

# Chamada comum
mostra_pessoa 'Joao', { idade: 18, sexo: :masc }
# Quando o último parâmetro é um hash,
# podemos omitir as chaves:
mostra_pessoa 'Joao', idade: 18, sexo: :masc
```

## Programação orientada a objetos

### Classes

{:.editor}

```ruby
class Anfitriao
  def initialize(nome = "Mundo")
    @nome = nome
  end
  def diz_ola
    puts "Olá #{@nome}!"
  end
  def diz_adeus
    puts "Adeus #{@nome}, volte sempre."
  end
end

a = Anfitriao.new("Joao")
a.diz_ola
a.diz_adeus
```

Várias coisas acontecendo nesse código:

- Use `class` para definir uma classe
- O nome da classe obrigatoriamente começa com letra maiúscula
- O construtor é o método `initialize`
- As variáveis começadas por `@` são variáveis de instância (ou atributos) da classe
- Não é preciso declarar os atributos; eles passam a existir quando um valor é atribuído a eles
- Para instanciar um objeto, chama-se o método `new` da classe.

### Classes são abertas para modificação

{:.editor}

```ruby
class String
  def gritado
    self.upcase + "!!!"
  end
end

puts "alo, mundo".gritado
```

Note que `self` faz referência ao objeto atual. É o equivalente do `this` do Java.

## Getters e setters

Os atributos de uma classe não são visíveis fora dela.

{:.editor}

```ruby
class Anfitriao
  def initialize(nome = "Mundo")
    @nome = nome
  end
end

a = Anfitriao.new("Joao")
puts a.@nome   # Erro!!
```

É preciso criar métodos para acessar (ler ou modificar) os atributos.

{:.editor}

```ruby
class Anfitriao
  def initialize(nome = "Mundo")
    @nome = nome
  end

  def nome
    @nome
  end

  def nome=(novo_nome)
    @nome = novo_nome
  end
end

a = Anfitriao.new("Joao")
puts a.nome
a.nome = "Jose"
puts a.nome
```

Note que `a.nome = "Jose"` é equivalente a `a.nome=("Jose")`.

Como *getters* e *setters* são tão comuns, existem métodos que criam eles para você:

- `attr_reader`: cria getter
- `attr_writer`: cria setter
- `attr_accessor`: cria getter e setter

{:.editor}

```ruby
class Anfitriao
  attr_reader :nome
  attr_writer :idade
  attr_accessor :sexo

  def initialize(nome = "Mundo")
    @nome = nome
  end
end

a = Anfitriao.new
a.idade = 2
a.sexo = :masculino
puts a.sexo
puts a.nome
# Dá erro: método idade (getter) não existe
puts a.idade
```

### Atributos e métodos de classe

Também chamados de atributos e métodos estáticos, eles são únicos para todos os objetos da mesma classe.

- Atributos estáticos começam com `@@`.
- Métodos estáticos são definidos usando-se `def self.nome_do_metodo`.

Exemplo:

{:.editor}

```ruby
class Anfitriao
  def initialize(nome)
    @@saudacao = "Alo"
    @nome = nome
  end

  def diz_alo
    puts "#{@@saudacao}, #{@nome}"
  end

  def self.saudacao=(str)
    @@saudacao = str
  end
  def self.saudacao
    @@saudacao
  end
end

joao = Anfitriao.new("Joao")
maria = Anfitriao.new("Maria")

joao.diz_alo
maria.diz_alo

Anfitriao.saudacao = "Ei"
joao.diz_alo
maria.diz_alo
```

### Herança

Use `class A < B` para definir uma classe `A` que é subclasse de `B`.

{:.editor}

```ruby
class Animal
  def anda
    puts "andando"
  end
end

class Gato < Animal
  def anda
    super
    puts "e pulando"
  end
  def mia
    puts "miau"
  end
end

g = Gato.new
g.anda
g.mia

a = Animal.new
a.anda
a.mia   # Erro!
```

Use `super` dentro de um método para chamar o método de mesmo nome na superclasse.

As classes que não declaram superclasse herdam da classe `Object`.

### Visibilidade

Ruby também possui os modificadores de visibilidade `public`, `protected` e `private`. Por padrão a visibilidade é `public`. Todos os métodos definidos após um modificador estão sujeitos à regra do modificado. Exemplo:

{:.editor}

```ruby
class Teste
  def a
    puts 'a'
  end

  private

    def b
      puts 'b'
    end

    def c
      puts 'c'
    end
end

# Os métodos b e c são privados
t = Teste.new
t.a
t.c    # erro!
```



