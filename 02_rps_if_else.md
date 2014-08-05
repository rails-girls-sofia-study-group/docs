# RPS - условия

Дотук имаме избора на потребителя в променливата `user_choice`. Имаме и избора на компютъра в променливата `computer_choice`. Знаем, че във всяка една от тези две променливи има едно от: "rock", "paper", "scissors". Искаме да сравним тези два избора спрямо правилата на играта.

Най-очевидния начин да стане това, е просто да напишем проверка за всеки един от деветте възможни случая. Да започнем с това:

``` ruby
user_choice = "rock"
computer_choice = "scissors"

if user_choice == "rock" and computer_choice == "scissors"
  puts "You win!"
else
  puts "You lose!"
end
```

В този вариант, просто описваме какво ще се случи ако `user_choice` и `computer_choice` са две познати стойности. Условието `user_choice == "rock" and computer_choice == "scissors"` е условие, чийто резултат знаем: потребителя печели ("You win!"). Остава да минем през всички възможни варианти и да опишем какъв е резултата:

``` ruby
user_choice = "?"
computer_choice = "?"

if user_choice == "rock" and computer_choice == "scissors"
  puts "You win!"
elsif user_choice == "rock" and computer_choice == "paper"
  puts "You lose!"
elsif user_choice == "rock" and computer_choice == "rock"
  puts "It's a tie"
else
  puts "I don't know what the result is yet."
end
```

Дотук изброяваме три варианта -- ако потребителя е избрал "rock", при какви условия печели, при какви условия губи и при какви е равна игра. Нека изброим и останалите варианти:

``` ruby
user_choice = "?"
computer_choice = "?"

if user_choice == "rock" and computer_choice == "scissors"
  puts "You win!"
elsif user_choice == "rock" and computer_choice == "paper"
  puts "You lose!"
elsif user_choice == "rock" and computer_choice == "rock"
  puts "It's a tie"
elsif user_choice == "paper" and computer_choice == "rock"
  puts "You win!"
elsif user_choice == "paper" and computer_choice == "scissors"
  puts "You lose!"
elsif user_choice == "paper" and computer_choice == "paper"
  puts "It's a tie"
elsif user_choice == "scissors" and computer_choice == "paper"
  puts "You win!"
elsif user_choice == "scissors" and computer_choice == "rock"
  puts "You lose!"
elsif user_choice == "scissors" and computer_choice == "scissors"
  puts "It's a tie"
end
```

Това е дългичко, но минава през всички възможни варианти за потребителя и за компютъра. Забележете, че реда, в който сме ги подредили, може да е различен. Тук сме минали през всички варианти в следния ред:

- потребителя е избрал "rock", какви варианти имаме за компютъра?
- потребителя е избрал "paper", какви варианти имаме за компютъра?
- потребителя е избрал "scissors", какви варианти имаме за компютъра?

Но бихме могли да го подредим и по друг начин, например по резултата, който се получава:

``` ruby
user_choice = "?"
computer_choice = "?"

if user_choice == "rock" and computer_choice == "rock"
  puts "It's a tie"
elsif user_choice == "paper" and computer_choice == "paper"
  puts "It's a tie"
elsif user_choice == "scissors" and computer_choice == "scissors"
  puts "It's a tie"
elsif user_choice == "rock" and computer_choice == "scissors"
  puts "You win!"
elsif user_choice == "paper" and computer_choice == "rock"
  puts "You win!"
elsif user_choice == "scissors" and computer_choice == "paper"
  puts "You win!"
elsif user_choice == "rock" and computer_choice == "paper"
  puts "You lose!"
elsif user_choice == "paper" and computer_choice == "scissors"
  puts "You lose!"
elsif user_choice == "scissors" and computer_choice == "rock"
  puts "You lose!"
end
```

Подредбата тук е:

- при какви комбинации потребител/компютър имаме равенство?
- при какви комбинации потребител/компютър имаме победа за потребителя?
- при какви комбинации потребител/компютър имаме загуба за потребителя?

Тук може да забележим един начин да посъкратим кода. В случая `user_choice == "rock" and computer_choice == "rock"`, ние сравняваме двете променливи с един и същ низ. Същото правим и в случая, когато са "paper" и "scissors". Можем просто да ги сравним един с друг:

``` ruby
user_choice = "?"
computer_choice = "?"

if user_choice == computer_choice
  puts "It's a tie"
elsif user_choice == "rock" and computer_choice == "scissors"
  puts "You win!"
elsif user_choice == "paper" and computer_choice == "rock"
  puts "You win!"
elsif user_choice == "scissors" and computer_choice == "paper"
  puts "You win!"
elsif user_choice == "rock" and computer_choice == "paper"
  puts "You lose!"
elsif user_choice == "paper" and computer_choice == "scissors"
  puts "You lose!"
elsif user_choice == "scissors" and computer_choice == "rock"
  puts "You lose!"
end
```

Така успяхме да съкратим две проверки, а кода работи по същия начин. Друго, което можем да забележим, е че няма нужда да проверяваме за загуба:

``` ruby
user_choice = "?"
computer_choice = "?"

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

Единствените три състояния на играта са "равенство", "победа", "загуба". Ако проверим дали е "равенство" и видим, че не е, след това проверим дали е "победа", и видим, че не е, единственото оставащо като вариант е "загуба", затова можем просто да сложим `else` и да не проверяваме променливите.

Ето целия код, който написахме до момента:

``` ruby
puts "Please enter one of: rock, paper, scissors"
user_choice = gets.chomp

computer_choice = "scissors"

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

Забележете, че компютъра все още играе "scissors", всеки път. Това е следващото, което трябва да се поправи.
