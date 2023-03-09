# Доп 5. Руководство по web3js

Этот учебник основан на сайте web3@1.0.0-beta.29 web3.js. Он предназначен в качестве введения в web3.js.

Библиотека web3.js JavaScript представляет собой набор модулей, содержащих специфическую функциональность для экосистемы Ethereum, а также совместимый с Ethereum JavaScript API, реализующий спецификацию Generic JSON RPC.

Вместо того чтобы запускать собственный локальный узел, вы можете использовать существующего поставщика инфраструктуры, который обслуживает узлы как облачные сервисы и выполняет запросы узлов для вас. Два популярных варианта включают Alchemy API и Infura.

## web3.js Контрактное базовое взаимодействие в неблокируемой (асинхронной) моде

Убедитесь, что у вас есть действительная версия npm:

```
$ npm -v
5.6.0
```
 
Если вы этого не сделали, инициализируйте npm:

`$ npm init`
 
Установите основные зависимости:

```
$ npm i command-line-args
$ npm i web3
$ npm i node-rest-client-promise
 ```

Это обновит ваш файл конфигурации package.json с новыми зависимостями.

### Выполнение сценариев Node.js
Базовое исполнение:

`$ node code/web3js/web3js_demo/web3-contract-basic-interaction.js`
 
Получите токен доступа от провайдера узла, например, Alchemy API или Infura, и сохраните api-ключ в локальном файле под названием alchemyFileToken или infuraFileToken):

```
$ node code/web3js/web3js_demo/web3-contract-basic-interaction.js \
  --alchemyFileToken /path/to/file/with/alchemy_token
 ```

или:

```
$ node code/web3js/web3js_demo/web3-contract-basic-interaction.js \
  --infuraFileToken /path/to/file/with/infura_token
 ```
 
Это позволит прочитать файл с вашим собственным маркером и передать его в качестве аргумента командной строки в фактическую команду.

## Просмотр демонстрационного сценария

Далее рассмотрим наш демонстрационный скрипт web3-contract-basic-interaction.

Мы используем объект Web3 для получения базового провайдера web3:

`var web3 = new Web3(node_host);`

Затем мы можем взаимодействовать с web3 и попробовать некоторые базовые функции. Рассмотрим версию протокола:

```
web3.eth.getProtocolVersion().then(function(protocolVersion) {
      console.log(`Protocol Version: ${protocolVersion}`);
  })
```
Теперь давайте посмотрим на текущую цену на газ:

```
web3.eth.getGasPrice().then(function(gasPrice) {
      console.log(`Gas Price: ${gasPrice}`);
  })
```

Какой последний добытый блок в текущей цепи?

```
web3.eth.getBlockNumber().then(function(blockNumber) {
      console.log(`Block Number: ${blockNumber}`);
  })
```

## Взаимодействие по контракту
Теперь давайте попробуем несколько базовых взаимодействий с контрактом. Для этих примеров мы будем использовать контракт WETH9_ в тестовой сети Kovan.

Во-первых, давайте инициализируем наш контрактный адрес:

`var our_contract_address = "0xd0A1E359811322d97991E03f863a0C30C2cF029C";`

Затем мы можем посмотреть на его баланс:

```
web3.eth.getBalance(our_contract_address).then(function(balance) {
      console.log(`Balance of ${our_contract_address}: ${balance}`);
})
```

и посмотреть его байткод:

```
web3.eth.getCode(our_contract_address).then(function(code) {
      console.log(code);
})
```

Далее мы подготовим нашу среду для взаимодействия с API проводника Etherscan.

Давайте инициализируем URL нашего контракта в API проводника Etherscan для цепочки Kovan:

```
var etherscan_url =
  "https://kovan.etherscan.io/api?module=contract&action=getabi&
  address=${our_contract_address}"
```

И давайте инициализируем REST-клиент для взаимодействия с API Etherscan:

`var client = require('node-rest-client-promise').Client();`

и получить обещание клиента:

`client.getPromise(etherscan_url)`

После того, как мы получили действительное обещание клиента, мы можем получить ABI нашего контракта из Etherscan API:

```
.then((client_promise) => {
  our_contract_abi = JSON.parse(client_promise.data.result);
```

И теперь мы можем создать наш объект контракта в виде обещания, чтобы использовать его позже:

```
  return new Promise((resolve, reject) => {
      var our_contract = new web3.eth.Contract(our_contract_abi,
                                               our_contract_address);
      try {
        // If all goes well
        resolve(our_contract);
      } catch (ex) {
        // If something goes wrong
        reject(ex);
      }
    });
})
```

Если наше обещание контракта возвращается успешно, мы можем начать взаимодействие с ним:

`.then((our_contract) => {`

Давайте посмотрим адрес нашего контракта:

```
console.log(`Our Contract address:${our_contract._address}`);
```

или альтернативно:

```
console.log(`Our Contract address in another way:
            ${our_contract.options.address}`);
```

Теперь давайте запросим наш контрактный ABI:

```
console.log("Our contract abi: " +
            JSON.stringify(our_contract.options.jsonInterface));
```

Мы можем увидеть общее количество поставок по нашему контракту с помощью обратного вызова:

```
our_contract.methods.totalSupply().call(function(err, totalSupply) {
    if (!err) {
        console.log(`Total Supply with a callback:  ${totalSupply}`);
    } else {
        console.log(err);
    }
});
```

Или мы можем использовать возвращаемое обещание вместо передачи обратного вызова:

```
our_contract.methods.totalSupply().call().then(function(totalSupply){
    console.log(`Total Supply with a promise:  ${totalSupply}`);
}).catch(function(err) {
    console.log(err);
});
```

## Асинхронные операции с помощью Await
Теперь, когда вы ознакомились с базовым учебником, вы можете попробовать выполнить те же взаимодействия, используя асинхронную конструкцию await. Просмотрите сценарий web3-contract-basic-interaction-async-await.js в code/web3js и сравните его с этим руководством, чтобы увидеть, чем они отличаются. Async-await легче читать, так как в нем асинхронное взаимодействие больше похоже на последовательность блокирующих вызовов.

