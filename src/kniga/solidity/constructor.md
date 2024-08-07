
### Конструктор контрактов и самоуничтожение
Существует специальная функция, которая используется только один раз. При создании контракта также запускается функция конструктора, если таковая существует, для инициализации состояния контракта. Конструктор запускается в той же транзакции, что и создание контракта. Функция конструктора является необязательной; вы заметили, что в нашем примере с краном она отсутствует.

Конструкторы могут быть заданы двумя способами. До версии Solidity v0.4.21 включительно, конструктор - это функция, имя которой совпадает с именем контракта, как показано здесь:

```
contract MEContract {
    function MEContract() {
        // This is the constructor
    }
}
```

Сложность этого формата заключается в том, что если имя контракта изменено, а имя функции-конструктора не изменено, то это уже не конструктор. Аналогично, если в названии контракта и/или конструктора случайно допущена опечатка, функция снова перестает быть конструктором. Это может привести к довольно неприятным, неожиданным и труднообнаруживаемым ошибкам. Представьте, например, что конструктор устанавливает владельца контракта для целей контроля. Если функция на самом деле не является конструктором из-за ошибки в именовании, то владелец не только останется неустановленным во время создания контракта, но и функция может быть развернута как постоянная и "вызываемая" часть контракта, как обычная функция, что позволит любой третьей стороне взломать контракт и стать "владельцем" после создания контракта.

Для решения потенциальных проблем, связанных с тем, что функции-конструкторы могут быть основаны на идентичном имени контракта, в Solidity v0.4.22 введено ключевое слово constructor, которое работает как функция-конструктор, но не имеет имени. Переименование контракта никак не влияет на конструктор. Кроме того, теперь легче определить, какая функция является конструктором. Это выглядит следующим образом:

```
pragma ^0.4.22
contract MEContract {
    constructor () {
        // This is the constructor
    }
}
```

Подводя итог, можно сказать, что жизненный цикл контракта начинается с транзакции создания из EOA или аккаунта контракта. Если есть конструктор, он выполняется как часть создания контракта, чтобы инициализировать состояние контракта в процессе его создания, а затем отбрасывается.

Другой конец жизненного цикла контракта - уничтожение контракта. Контракты уничтожаются специальным опкодом EVM под названием SELFDESTRUCT. Раньше он назывался SUICIDE, но это название было упразднено из-за негативных ассоциаций, связанных с этим словом. В Solidity этот опкод представлен в виде высокоуровневой встроенной функции selfdestruct, которая принимает один аргумент: адрес для получения любого остатка эфира, оставшегося на аккаунте контракта. Это выглядит следующим образом:
`selfdestruct(address recipient);`

Обратите внимание, что вы должны явно добавить эту команду в ваш контракт, если хотите, чтобы он был удаляемым - это единственный способ удаления контракта, и по умолчанию она отсутствует. Таким образом, пользователи контракта, которые могут рассчитывать на то, что контракт будет существовать вечно, могут быть уверены, что контракт не может быть удален, если он не содержит опкода SELFDESTRUCT.

### Добавление конструктора и самоуничтожения в наш пример со смесителем
Контракт на примере смесителя, который мы представили в [intro_chapter], не имеет ни конструктора, ни функций самоуничтожения. Это вечный контракт, который не может быть удален. Давайте изменим это, добавив конструктор и функцию самоуничтожения. Вероятно, мы хотим, чтобы функция самоуничтожения могла быть вызвана только тем EOA, который изначально создал контракт. По соглашению, это обычно хранится в адресной переменной, называемой owner. Наш конструктор устанавливает переменную owner, а функция самоуничтожения сначала проверит, что владелец вызвал ее напрямую.
Во-первых, наш конструктор:

```
// Version of Solidity compiler this program was written for
pragma solidity ^0.6.0;

// Our first contract is a faucet!
contract Faucet {

    address owner;

    // Initialize Faucet contract: set owner
    constructor() {
        owner = msg.sender;
    }

    [...]
}
```

В нашем контракте теперь есть переменная типа адреса с именем "владелец". Имя "владелец" не является каким-либо особенным. Мы могли бы назвать эту адресную переменную "potato" и использовать ее точно так же. Имя owner просто делает понятным ее назначение.
Далее наш конструктор, который выполняется как часть транзакции создания контракта, присваивает адрес из msg.sender переменной owner. Мы использовали msg.sender в функции withdraw для идентификации инициатора запроса на вывод средств. В конструкторе, однако, msg.sender - это адрес EOA или контракта, который инициировал создание контракта. Мы знаем, что это так, потому что это функция конструктора: она выполняется только один раз, во время создания контракта.

Теперь мы можем добавить функцию для уничтожения контракта. Нам нужно убедиться, что только владелец может запустить эту функцию, поэтому мы используем оператор require для контроля доступа. Вот как это будет выглядеть:

```
// Contract destructor
function destroy() public {
    require(msg.sender == owner);
    selfdestruct(owner);
}
```

Если кто-либо вызовет эту функцию уничтожения с адреса, отличного от адреса владельца, она завершится неудачей. Но если ее вызовет тот же адрес, который был сохранен в owner конструктором, контракт самоуничтожится и отправит весь оставшийся баланс на адрес владельца. Обратите внимание, что мы не использовали опасную функцию tx.origin для определения того, желает ли владелец уничтожить контракт - использование tx.origin позволило бы злонамеренным контрактам уничтожить ваш контракт без вашего разрешения.
