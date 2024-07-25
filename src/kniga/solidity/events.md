
## События
Когда транзакция завершается (успешно или нет), она выдает квитанцию транзакции, как мы увидим в [evm_chapter]. Квитанция транзакции содержит записи журнала, которые предоставляют информацию о действиях, произошедших во время выполнения транзакции. События - это объекты высокого уровня Solidity, которые используются для создания этих журналов.

События особенно полезны для легких клиентов и сервисов DApp, которые могут "следить" за определенными событиями и сообщать о них в пользовательский интерфейс или изменять состояние приложения, чтобы отразить событие в базовом контракте.

Объекты событий принимают аргументы, которые сериализуются и записываются в журналы транзакций, в блокчейн. Перед аргументом можно поставить ключевое слово indexed, чтобы значение стало частью индексированной таблицы (хэш-таблицы), по которой приложение может осуществлять поиск или фильтрацию.
До сих пор мы не добавили никаких событий в нашем примере с Faucet, поэтому давайте сделаем это. Мы добавим два события, одно для регистрации любых снятий и одно для регистрации любых депозитов. Мы назовем эти события соответственно Withdrawal и Deposit. Сначала мы определим события в контракте Faucet:

```
contract Faucet is Mortal {
	event Withdrawal(address indexed to, uint amount);
	event Deposit(address indexed from, uint amount);

    [...]
}
```

Мы решили сделать адреса индексируемыми, чтобы обеспечить поиск и фильтрацию в любом пользовательском интерфейсе, созданном для доступа к нашему смесителю.

Далее мы используем ключевое слово emit для включения данных о событиях в журналы транзакций:

```
// Give out ether to anyone who asks
function withdraw(uint withdraw_amount) public {
    [...]
    msg.sender.transfer(withdraw_amount);
    emit Withdrawal(msg.sender, withdraw_amount);
}
// Accept any incoming amount
receive () external payable {
    emit Deposit(msg.sender, msg.value);
}
```

Полученный контракт Faucet.sol выглядит как Faucet8.sol: Переработанный контракт Faucet, с событиями.
Пример 3. Faucet8.sol: Пересмотренный контракт Faucet, с событиями
`link:code/Solidity/Faucet8.sol[]`

### Ловля событий
Итак, мы настроили наш контракт на испускание событий. Как нам увидеть результаты транзакции и "поймать" события? Библиотека web3.js предоставляет структуру данных, которая содержит журналы транзакции. В них мы можем увидеть события, сгенерированные транзакцией.

Давайте воспользуемся truffle для запуска тестовой транзакции на пересмотренном контракте Faucet. Следуйте инструкциям в [truffle] для создания каталога проекта и компиляции кода Faucet. Исходный код можно найти в репозитории GitHub книги под code/truffle/FaucetEvents.

```
$ truffle develop
truffle(develop)> compile
truffle(develop)> migrate
Using network 'develop'.

Running migration: 1_initial_migration.js
  Deploying Migrations...
  ... 0xb77ceae7c3f5afb7fbe3a6c5974d352aa844f53f955ee7d707ef6f3f8e6b4e61
  Migrations: 0x8cdaf0cd259887258bc13a92c0a6da92698644c0
Saving successful migration to network...
  ... 0xd7bc86d31bee32fa3988f1c1eabce403a1b5d570340a3a9cdba53a472ee8c956
Saving artifacts...
Running migration: 2_deploy_contracts.js
  Deploying Faucet...
  ... 0xfa850d754314c3fb83f43ca1fa6ee20bc9652d891c00a2f63fd43ab5bfb0d781
  Faucet: 0x345ca3e014aaf5dca488057592ee47305d9b3e10
Saving successful migration to network...
  ... 0xf36163615f41ef7ed8f4a8f192149a0bf633fe1a2398ce001bf44c43dc7bdda0
Saving artifacts...

truffle(develop)> Faucet.deployed().then(i => {FaucetDeployed = i})
truffle(develop)> FaucetDeployed.send(web3.utils.toWei(1, "ether")).then(res => \
                  { console.log(res.logs[0].event, res.logs[0].args) })
Deposit { from: '0x627306090abab3a6e1400e9345bc60c78a8bef57',
  amount: BigNumber { s: 1, e: 18, c: [ 10000 ] } }
truffle(develop)> FaucetDeployed.withdraw(web3.utils.toWei(0.1, "ether")).then(res => \
                  { console.log(res.logs[0].event, res.logs[0].args) })
Withdrawal { to: '0x627306090abab3a6e1400e9345bc60c78a8bef57',
  amount: BigNumber { s: 1, e: 17, c: [ 1000 ] } }
```

 
После развертывания контракта с помощью функции deployed мы выполняем две транзакции. Первая транзакция - это депозит (с помощью функции send), который создает событие Deposit в журнале транзакций:

```
Deposit { from: '0x627306090abab3a6e1400e9345bc60c78a8bef57',
  amount: BigNumber { s: 1, e: 18, c: [ 10000 ] } }
```

Далее мы используем функцию withdraw для снятия средств. При этом возникает событие Withdrawal:

```
Withdrawal { to: '0x627306090abab3a6e1400e9345bc60c78a8bef57',
  amount: BigNumber { s: 1, e: 17, c: [ 1000 ] } }
```

Чтобы получить эти события, мы просмотрели массив журналов, возвращенный в результате (res) транзакций. Первая запись журнала (logs[0]) содержит имя события в logs[0].event и аргументы события в logs[0].args. Отобразив их на консоли, мы можем увидеть имя события и аргументы события.
События являются очень полезным механизмом не только для внутриконтрактного взаимодействия, но и для отладки во время разработки.
