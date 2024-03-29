
## Специальная транзакция: Создание контракта

Особый случай, о котором следует упомянуть, - это транзакция, создающая новый контракт на блокчейне, развертывая его для будущего использования. Транзакции создания контракта отправляются на специальный адрес назначения, называемый нулевым адресом; поле __to__ в транзакции регистрации контракта содержит адрес __0x0__. Этот адрес не представляет ни EOA (нет соответствующей пары закрытый-публичный ключ), ни контракт. Он не может тратить ether или инициировать транзакцию. Он используется только в качестве адресата, со специальным значением "создать этот контракт".

Хотя нулевой адрес предназначен только для создания контрактов, на него иногда поступают платежи с различных адресов. Этому есть два объяснения: либо это случайность, приводящая к потере ether, либо это намеренное сжигание ether (преднамеренное уничтожение ether путем отправки его на адрес, с которого он никогда не сможет быть потрачен). Однако если вы хотите произвести преднамеренное сжигание ether, вам следует сообщить о своем намерении сети и вместо этого использовать специально выделенный адрес для сжигания:

`0x000000000000000000000000000000000000dEaD`

__Предупреждение:__ Любой ether, отправленный на указанный адрес для сжигания, станет нерасходуемым и будет потерян навсегда.

Транзакция создания контракта должна содержать только __data__, содержащую скомпилированный байткод, который создаст контракт. Единственный эффект этой транзакции - создание контракта. Вы можете включить сумму ether в поле значения, если хотите установить новый контракт с начальным балансом, но это совершенно необязательно. Если вы отправляете значение (ether) на адрес создания контракта без __data__ (без контракта), то эффект будет таким же, как и при отправке на адрес сгорания - нет контракта для зачисления, поэтому ether теряется.

В качестве примера мы можем создать контракт Faucet.sol, использованный в [intro_chapter], вручную создав транзакцию на нулевой адрес с контрактом в полезной нагрузке данных. Контракт необходимо скомпилировать в представление байткода. 

Это можно сделать с помощью компилятора Solidity:

```
$ solc --bin Faucet.sol

Binary:
6060604052341561000f57600080fd5b60e58061001d6000396000f30060606040526004361060...
```
 
Эту же информацию можно получить из онлайн-компилятора Remix.

Теперь мы можем создать транзакцию:

```
> src = web3.eth.accounts[0];
> faucet_code = \
  "0x6060604052341561000f57600080fd5b60e58061001d6000396000f300606...f0029";
> web3.eth.sendTransaction({from: src, to: 0, data: faucet_code, \
  gas: 113558, gasPrice: 200000000000});

"0x7bcc327ae5d369f75b98c0d59037eec41d44dfae75447fd753d9f2db9439124b"
```
 
Хорошей практикой является всегда указывать параметр __to__, даже в случае создания контракта с нулевым адресом, поскольку цена случайной отправки ether на __0x0__ и его потери навсегда слишком велика. Также следует указать gasPrice и gasLimit.

Как только контракт будет создан, мы сможем увидеть его в блокчейн-проводнике Etherscan, как показано в Etherscan, где контракт успешно добыт.

![Эфирскан, показывающий успешно добытый контракт](./kartinki/contract_published.png)
Рисунок 5. Эфирскан, показывающий успешно добытый контракт

Мы можем посмотреть на квитанцию о сделке, чтобы получить информацию о контракте:

```
> web3.eth.getTransactionReceipt( \
  "0x7bcc327ae5d369f75b98c0d59037eec41d44dfae75447fd753d9f2db9439124b");

{
  blockHash: "0x6fa7d8bf982490de6246875deb2c21e5f3665b4422089c060138fc3907a95bb2",
  blockNumber: 3105256,
  contractAddress: "0xb226270965b43373e98ffc6e2c7693c17e2cf40b",
  cumulativeGasUsed: 113558,
  from: "0x2a966a87db5913c1b22a59b0d8a11cc51c167a89",
  gasUsed: 113558,
  logs: [],
  logsBloom: \
    "0x00000000000000000000000000000000000000000000000000...00000",
  status: "0x1",
  to: null,
  transactionHash: \
    "0x7bcc327ae5d369f75b98c0d59037eec41d44dfae75447fd753d9f2db9439124b",
  transactionIndex: 0
}
```
 
Сюда входит адрес контракта, который мы можем использовать для отправки средств на контракт и получения средств с него, как показано в предыдущем разделе:

```
> contract_address = "0xb226270965b43373e98ffc6e2c7693c17e2cf40b"
> web3.eth.sendTransaction({from: src, to: contract_address, \
  value: web3.utils.toWei(0.1, "ether"), data: ""});

"0x6ebf2e1fe95cc9c1fe2e1a0dc45678ccd127d374fdf145c5c8e6cd4ea2e6ca9f"

> web3.eth.sendTransaction({from: src, to: contract_address, value: 0, data: \
  "0x2e1a7d4d000000000000000000000000000000000000000000000000002386f26fc10000"});

"0x59836029e7ce43e92daf84313816ca31420a76a9a571b69e31ec4bf4b37cd16e"
```
 
Через некоторое время обе транзакции видны на Etherscan, как показано в Etherscan, где показаны транзакции по отправке и получению средств.

![Etherscan, показывающий транзакции по отправке и получению средств](./kartinki/published_contract_transactions.png)
Рисунок 6. Etherscan, показывающий транзакции по отправке и получению средств

СДЕЛАТЬ:
