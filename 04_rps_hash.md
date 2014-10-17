# RPS - съкращаване на кода с хеш таблица

1. [Въведение](01_rps_intro.md)
1. [If/else](02_rps_if_else.md)
1. [Произволен избор и валидация](03_rps_random_choice_and_validation.md)
1. [Съкращаване на кода с хеш таблица](04_rps_hash.md)

Мястото, където вземаме решение за това кой побеждава, е една голяма if-клауза. Изглежда така:

``` ruby
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

Успяхме да го съкратим доста, но все пак има как да се съкрати повече, като променим изцяло начина си на мислене. Вместо да правим няколко отделни проверки, просто ще използаме хеш (речник), за да запазим всички ходове, и кой ход ги бие.

*Базови познания: [хешове](hashes.md)*

Това ще изглежда така:

``` ruby
winning_moves = {
  "rock"     => "paper",
  "paper"    => "scissors",
  "scissors" => "rock",
}
```

Сега, в хеша `winning_moves` се съдържат печелившите ходове за всеки един ход. Ако достъпим `winning_moves["rock"]`, ще получим хода, който побеждава "rock", в случая -- "paper".

При това положение, можем да проверим дали хода на потребителя съвпада с печелившия ход, който съответства на този на компютъра:

``` ruby
if user_choice == winning_moves[computer_choice]
  puts "You win!"
end
```

Стойността `winning_moves[computer_choice]` ще ни даде хода, който би победил хода на компютъра. Съответно, ако хода на потребителя е същия, потребителя печели.

Аналогично, можем да проверим и обратното:

``` ruby
if computer_choice == winning_moves[user_choice]
  puts "You lose!"
end
```

Ако `winning_moves[user_choice]`, хода, който би победил `user_choice`, е същия като хода на компютъра (`computer_choice`), то компютъра печели, потребителя губи.

Ако нито едно от двете не е изпълнено, значи двамата са равни. Цялата логика изглежда така:

``` ruby
if user_choice == winning_moves[computer_choice]
  puts "You win!"
elsif computer_choice == winning_moves[user_choice]
  puts "You lose!"
else
  puts "It's a tie"
end
```

Както виждате, така съкратихме доста проверки -- останаха само две. Неприятното е, че кода сега е една идея по-труден за разбиране. Когато един проблем има много решения, заслужава си да помислим дали да избираме по-краткото, по-бързото, или по-разбираемото. Често разликата между параметрите на решението не е чак толкова драматична. Не е изобщо странно разбираемото решение да е доста бързо и доста кратко. Добра идея е да се наблегне на разбираемост, и в случай на нужда, да се преработи кода така, че да е по-бърз или по-кратък.

Целия код до този момент е:

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

if user_choice == winning_moves[computer_choice]
  puts "You win!"
elsif computer_choice == winning_moves[user_choice]
  puts "You lose!"
else
  puts "It's a tie"
end
```
