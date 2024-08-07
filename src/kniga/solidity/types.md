
## Программирование с помощью Solidity
В этом разделе мы рассмотрим некоторые возможности языка Solidity. Как мы упоминали в [intro_chapter], наш первый пример контракта был очень простым и к тому же несовершенным в различных отношениях. Здесь мы будем постепенно улучшать его, одновременно изучая возможности использования Solidity. Однако это не будет полным учебником по Solidity, поскольку Solidity довольно сложна и быстро развивается. Мы рассмотрим основы и дадим вам достаточную базу, чтобы вы могли самостоятельно изучить остальное. Документацию по Solidity можно найти на сайте проекта.
### Типы данных
Сначала рассмотрим некоторые из основных типов данных, предлагаемых в Solidity:
#### Булево (bool)
Булево значение, истина или ложь, с логическими операторами ! (не), && (и), || (или), == (равно) и != (не равно).
#### Integer (int, uint)
Знаковые (int) и беззнаковые (uint) целые числа, объявленные с шагом в 8 бит от int8 до uint256. Без суффикса size используются 256-битные величины, чтобы соответствовать размеру слова EVM.
#### Фиксированная точка (fixed, ufixed)
Числа с фиксированной точкой, объявленные с помощью (u)fixedMxN, где M - размер в битах (с шагом 8 до 256), а N - количество десятичных знаков после точки (до 18); например, ufixed32x2.
#### Адрес
20-байтовый адрес Ethereum. Объект адреса имеет множество полезных функций-членов, основными из которых являются balance (возвращает баланс аккаунта) и transfer (переводит эфир на аккаунт).
#### Массив байтов (фиксированный)
Массивы байтов фиксированного размера, объявленные с байт1 до байт32.
#### Массив байтов (динамический)
Массивы байтов переменного размера, объявленные с помощью bytes или string.
#### Enum
Определяемый пользователем тип для перечисления дискретных значений: enum NAME {LABEL1, LABEL 2, ...}.
#### Массивы
Массив любого типа, фиксированный или динамический: uint32[][5] - массив фиксированного размера из пяти динамических массивов целых беззнаковых чисел.
#### Структура
Определяемые пользователем контейнеры данных для группировки переменных: struct NAME {TYPE1 VARIABLE1; TYPE2 VARIABLE2; ...}.
#### Составление карты
Таблицы хэш-поиска для пар ключ => значение: mapping(KEY_TYPE => VALUE_TYPE) NAME.
В дополнение к этим типам данных Solidity также предлагает различные литералы значений, которые могут быть использованы для вычисления различных единиц измерения:
#### Единицы времени
Единицы секунд, минут, часов и дней можно использовать в качестве суффиксов, преобразуя их в кратные единицы секунд.
#### Эфирные единицы
Единицы wei, finney, szabo и ether могут использоваться в качестве суффиксов, преобразуясь в кратные значения базовой единицы wei.

В нашем примере контракта Faucet мы использовали uint (что является псевдонимом uint256) для переменной withdraw_amount. Мы также косвенно использовали переменную address, которую мы задали с помощью msg.sender. Мы будем использовать больше этих типов данных в наших примерах в оставшейся части этой главы.

Давайте воспользуемся одним из множителей единиц, чтобы улучшить читаемость нашего примера контракта. В функции withdraw мы ограничиваем максимальную сумму снятия, выражая ее в вэях, базовой единице эфира:
`require(withdraw_amount <= 100000000000000000);`
Это не очень удобно для чтения. Мы можем улучшить наш код, используя множитель единицы измерения ether, чтобы выразить значение в ether вместо wei:
`require(withdraw_amount <= 0.1 ether);`

