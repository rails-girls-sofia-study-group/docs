# Списъци

TODO: Enumerable, map, `*args`

Най-просто казано, "списък" е поредица от елементи. Друго име за същото е "масив". На английски двете думи са "list" и "array".

## Дефиниране

Списък може да се дефинира с квадратни скоби и елементи, отделени със запетаи. Примерно:

``` ruby
numbers = [1, 2, 3]
```

Може да се направи списък с елементи низове:

``` ruby
numbers_in_words = ["one", "two", "three"]
```

А може и да се направят списъци със смесена информация, например:

``` ruby
# Data is in the form: [ name, age, [list of favorite colors] ]

first_person  = [ "John", 23, ["blue", "green"] ]
second_person = [ "Jane", 37, ["red", "orange"] ]
third_person  = [ "Timmy", 12, ["pink", "blue", "yellow"] ]
```

Както вероятно е станало ясно от горния пример, списъци могат и да се влагат един в друг.

## Достъп до елементите

За да достъпим данните в списъка, използваме поредния номер на елемента, който търсим, като първия елемент има номер 0:

``` ruby
first_person = [ "John", 23, ["blue", "green"] ]

puts first_person[0]    # => "John"
puts first_person[1]    # => "23"
puts first_person[2][0] # => "blue"
puts first_person[2][0] # => "green"
```

Бихме могли да достъпим последния елемент с -1, предпоследния с -2, и т.н.

## Промяна на списъци

Можем да добавим още елементи в съществуващ списък с метода `push` или оператора `<<`. Ефекта им е един и същ:

``` ruby
numbers = []

numbers.push(1)
puts numbers.inspect # => [1]

numbers << 2
puts numbers.inspect # => [1, 2]
```

Бихме могли да слеем списъци с оператора `+`:

``` ruby
numbers = [1, 2, 3] + [4, 5]
puts numbers.inspect # => [1, 2, 3, 4, 5]
```

Горния пример можем да напишем и така:

``` ruby
numbers = [1, 2, 3]
numbers = numbers + [4, 5]
puts numbers.inspect # => [1, 2, 3, 4, 5]
```

Операцията `numbers = numbers + ...`, можем да съкратим с оператора `+=`:

``` ruby
numbers = [1, 2, 3]
numbers += [4, 5]
puts numbers.inspect # => [1, 2, 3, 4, 5]
```

## Итериране на списъци

Можем да "итерираме" списъка (да извършим нещо с всичките му елементи) с метода `each`:

``` ruby
names = ["Jack", "Jill", "Mary"]

names.each do |name|
  puts "Hello, #{name}, nice to meet you!"
end

# =>
#   Hello, Jack, nice to meet you!
#   Hello, Jill, nice to meet you!
#   Hello, Mary, nice to meet you!
```

Външния вид на този код вероятно ви е странен ако все още не знаете какво е "блок" в руби, но може да се опитате да го запомните просто така засега.
