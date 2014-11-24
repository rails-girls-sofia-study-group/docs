# RPS - съкращаване на кода с двумерен масив/таблица

1. [Въведение](01_rps_intro.md)
1. [If/else](02_rps_if_else.md)
1. [Произволен избор и валидация](03_rps_random_choice_and_validation.md)
1. [Съкращаване на кода с хеш таблица](04_rps_hash.md)
1. [Съкращаване на кода с двумерен масив](05_rps_table.md)

Също както променихме кода с if-клаузата да използва хеш таблица, можем и да го съкратим по друг начин. Вместо да запазим ключове и стойности, нека създадем таблица с две измерения:

- възможните ходове на потребителя
- възможните ходове на компютъра

Тя би изглеждала горе-долу по следния начин:

```
  | R P S
--+------
R | = W L
P | L = W
S | W L =
```

В тази таблица нека редовете да са избора на компютъра, а колоните - избора на потребителя. При това положение, стойностите имат следното значение:

- "=" означава, че двамата са наравно
- "W" означава, че потребителя печели (win)
- "L" означава, че потребителя губи (lose)

Първо, ще дефинираме таблицата:

``` ruby
result_table = [
  ["=", "W", "L"],
  ["L", "=", "W"],
  ["W", "L", "="]
]
```

*Базови познания: [списъци](lists.md)*
*Базови познания: [двумерни таблици](tables.md)*

Тази таблица е чисто и просто списък от списъци. Ако достъпим първия елемент от списъка с `result_table[0]`, ще получим като резултат `["=", "W", "L"]`, което само по себе си е списък. И така, за да достъпим (примерно) втория елемент от *този* вложен списък, ще използваме `result_table[0][1]`, което ще ни даде `W`.

След това, ще вземем вход от потребителя и ще изберем ход за компютъра, използвайки метода, който ползвахме досега:

``` ruby
puts "Please enter one of: rock, paper, scissors"
user_choice = gets.chomp

possible_choices = ["rock", "paper", "scissors"]

if not possible_choices.include?(user_choice)
  puts "Your choice, '#{user_choice}', is not one of: rock, paper, scissors. Please try again."
  exit
end

computer_choice = possible_choices.sample

puts "You played:      #{user_choice}"
puts "Computer played: #{computer_choice}"
```

Последната стъпка е да използваме таблицата, която дефинирахме, за да намерим резултата. Засега имаме ход за потребителя и такъв за компютъра. Ще разберем кой поред е този ход в списъка от ходове:

``` ruby
user_choice_index     = possible_choices.index(user_choice)
computer_choice_index = possible_choices.index(computer_choice)
```

Така получаваме две числа, `user_choice_index` и `computer_choice_index`, които са между 0 и 2. Ще индексираме двумерната таблица с тези две числа и ще получим отговор от "L", "W", или "=".

``` ruby
result = result_table[computer_choice_index][user_choice_index]

if result == "W"
  puts "You win!"
elsif result == "L"
  puts "You lose!"
elsif result == "="
  puts "It's a tie"
else
  raise "Unknown result: '#{result}' for computer choice: '#{computer_choice}', user choice: '#{user_choice}'"
end
```

Това решение също е компактно откъм код, понеже използва специална структура (двумерната таблица), която съдържа отговора на "кой побеждава при такъв ход на играча и такъв ход на компютъра". Единственото, което трябва да направим, е да преведем хода, идващ като низ "rock", "paper", "scissors", до число, с което да достъпим правилните елементи в таблицата.

Забележете, че този път правим проверка и за трите стойности, "W", "L", "=". В случай, че не е нито една от тези стойности, има някаква грешка в програмата! На теория, кода, който сме написали, би трябвало да работи правилно и никога да не се попадне в `else` клаузата. На практика обаче, ако ние, като програмисти, сме допуснали грешка в програмата, може да се получи грешен резултат и да не осъзнаем, че това е така. А дори да осъзнаем, да не намерим лесно проблема.

Кода в `else` клаузата хвърля грешка с `raise`. Грешката съдържа информация за това какви са били стойностите на ключовите променливи в момента. От тях можем да си направим някакви изводи за това какъв може да е проблема.

Такъв тип програмиране се нарича "defensive". Понякога е добра идея да вмъкваме подобни проверки, просто за да сме сигурни, че правим правилното нещо. В повечето случаи обаче, програмата ще ни даде грешка при грешни данни така или иначе, така че не си заслужава да правим специална проверка. Но в случай, че имате сравнително засукана логика, грешка в която не би била очевидна, може би е добра идея да проверите дали всичко е както очаквате да бъде.

Ето целия код на решението:

``` ruby
result_table = [
  ["=", "W", "L"],
  ["L", "=", "W"],
  ["W", "L", "="]
]

puts "Please enter one of: rock, paper, scissors"
user_choice = gets.chomp

possible_choices = ["rock", "paper", "scissors"]

if not possible_choices.include?(user_choice)
  puts "Your choice, '#{user_choice}', is not one of: rock, paper, scissors. Please try again."
  exit
end

computer_choice = possible_choices.sample

puts "You played:      #{user_choice}"
puts "Computer played: #{computer_choice}"

user_choice_index     = possible_choices.index(user_choice)
computer_choice_index = possible_choices.index(computer_choice)

result = result_table[computer_choice_index][user_choice_index]

if result == "W"
  puts "You win!"
elsif result == "L"
  puts "You lose!"
elsif result == "="
  puts "It's a tie"
else
  raise "Unknown result: '#{result}' for computer choice: '#{computer_choice}', user choice: '#{user_choice}'"
end
```
