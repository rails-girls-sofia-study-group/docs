# RPS - произволен избор и валидация на вход

1. [Въведение](01_rps_intro.md)
1. [If/else](02_rps_if_else.md)
1. [Произволен избор и валидация](03_rps_random_choice_and_validation.md)
1. [Съкращаване на кода с хеш таблица](04_rps_hash.md)
1. [Съкращаване на кода с двумерен масив](05_rps_table.md)

За да има смисъл играта, трябва да играем срещу някого. Компютъра може да избере произволен ход и да го изиграе. Това ще стане така:

``` ruby
possible_choices = ["rock", "paper", "scissors"]
computer_choice = possible_choices.sample
```

*Базови познания: [списъци](lists.md)*

Първо създаваме променлива `possible_choices`, която съдържа списък от трите възможни стойности за избора. След това, извикваме метода `sample` върху списъка, който ни дава един произволен елемент от него.

И така, като комбинираме кода, който имаме досега с тази добавка, получаваме следния резултат:

``` ruby
puts "Please enter one of: rock, paper, scissors"
user_choice = gets.chomp

possible_choices = ["rock", "paper", "scissors"]
computer_choice = possible_choices.sample

puts "You played:      #{user_choice}"
puts "Computer played: #{computer_choice}"

if user_choice == computer_choice
  puts "It's a tie"
elsif user_choice == "rock" and computer_choice == "scissors"
  puts "You win!"
elsif user_choice == "paper" and computer_choice == "rock"
  puts "You win!"
elsif user_choice == "scissors" and computer_choice == "paper"
  puts "You win!"
else
  puts "You lose!"
end
```

Сега имаме доста добре работеща програма. Ако я пуснем и въведем "rock" за нашия избор, ще получим нещо такова:

```
Please enter one of: rock, paper, scissors
rock
You played:      rock
Computer played: paper
You lose!
```

Или, ако имаме късмет:

```
Please enter one of: rock, paper, scissors
rock
You played:      rock
Computer played: scissors
You win!
```

Но какво става, ако въведем нещо различно от "rock", "paper" или "scissors", примерно "baba"?

```
Please enter one of: rock, paper, scissors
baba
You played:      baba
Computer played: scissors
You lose!
```

Хмм, това работи някакси, но не е каквото очакваме. Ако в реална игра изиграем нещо странно, това не значи, че автоматично губим -- просто значи, че хода е невалиден и трябва да играем пак.

Добра идея е винаги да мислим за това какво ще въведе потребителя и как ще реагираме ако въведе нещо странно. В случая, искаме да проверим дали избора на потребителя пасва на някой от познатите ни избори. Ще използваме променливата `possible_choices` за тази цел:

``` ruby
possible_choices = ["rock", "paper", "scissors"]

if not possible_choices.include?(user_choice)
  puts "Your choice, '#{user_choice}', is not one of: rock, paper, scissors. Please try again."
  exit
end
```

С този код, играта вече прави проверка дали сме въвели нещо смислено:

```
Please enter one of: rock, paper, scissors
baba
Your choice, 'baba', is not one of: rock, paper, scissors. Please try again.
```

Целия код, който сме написали до момента, е:

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

if user_choice == computer_choice
  puts "It's a tie"
elsif user_choice == "rock" and computer_choice == "scissors"
  puts "You win!"
elsif user_choice == "paper" and computer_choice == "rock"
  puts "You win!"
elsif user_choice == "scissors" and computer_choice == "paper"
  puts "You win!"
else
  puts "You lose!"
end
```

Следваща статия: [Съкращаване на кода с хеш таблица](04_rps_hash.md)
