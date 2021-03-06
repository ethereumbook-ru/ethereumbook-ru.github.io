# Что такое Ethereum

- Дата актуальности: ноябрь 2018
- [Англоязычный исходник](https://github.com/ethereumbook/ethereumbook/blob/develop/01what-is.asciidoc)
- Переводчик: [Илья Дружинин](https://github.com/ilyadruzhinin)
- GitHub перевода: [https://github.com/ethereumbook-ru](https://github.com/ethereumbook-ru)

Ethereum часто описывается как "мировой компьютер". Но что же это значит?
Давайте начнем с описания, которое ближе к компьютерным наукам,  а затем постараемся расшифровать используя практический анализ возможностей и характеристик платформы Ethereum. А также сравнивая его с Bitcoin и другими децентрализованными платформами обмена информации (их будем называть блокчейнами).

С точки зрения компьютерных наук, Ethereum это детерминированная, но практически неограниченная машина состояний (state machine), состоящей из глобально доступного singleton состояния и вирутальной машины, которая применяет изменения к этому состоянию.

С более практической точки зрения, Ethereum это открытая, глобально децентрализованная вычислительная инфраструктура, которая выполняет программы, которые таже называют _умные контракты_. Он использует блокчейн для синхронизации и сохранения изменений состояния системы, а также криптовалюту, казываемую _эфир (ether)_ для измерения и ограничения расходов вычислительных ресурсов.

Платформа Ethereum позволяет разработчикам создавать мощные, децентрализованные приложения со встроенными экономическими функциями. Обеспечивая высокую доступность, аудитоспособность, прозрачность и нейтральность, Ethereum также уменьшает или устраняет цензуру и уменьшает риски работы с контрагентами.

## Сравнение с Биткоином

Много людей приходят в Ethereum с уже имеющимся опытом в криптовалютах, особенно с Биткоином. В Ethereum'e много общих элементов с другими открытыми блокчейнами: одноранговая коммуникация между участниками, алгоритм консенсуса BFT (Byzantine fault-tolerant) для синхронизации обновлений состояния (т.н. proof-of-work блокчейн), используемые криптографические примитивы, такие как цифровые подписи, хеши и конечно цифровая валюта (эфир).

Однако, во многих отношениях, цель и постороение Ethereum'a поразительно отличается от других открытых блокчейнов, которые предшествовали ему, включая Биткоин.

Цель Ethereum'a не заключается быть просто сетью цифровой валюты. Хотя цифровая валюта эфир является неотъемлемой и необходимой для работы Ethereum'a. Валюта Ether предназначена является скорее _утилитарной валютой_ , нужная чтобы оплачивать работу на мировом комьютере и его использовать.

В отличии от Биткоина, который имеет очень ограниченный скриптовый язык, Ethereum проектировался как программируемый блокчейн общего назначения, запущенный на _виртуальной машине_ способный исполнять код произвольной и неограниченной сложности. Скриптовый язык Биткоина намеренно ограничивается простыми _true_/_false_ оценками условий расходов, язык Ethereum является _Тьюринг полным_, имея ввиду, что Ethereum может работать как комьютер общего назначения.

### Компоненты Блокчейна

Компоненты открытых, публичных блокчейнов (обычно):

* Одноранговая (P2P) сеть, соединяющая участников и распространнению транзакций и блоков верифицированных транзакций, основанная на стандартизированном "gossip" протоколе
* Сообщения в форме транзакции, представляющие изменения состояния
* Набор правил консенсуса, определяющих, что является транзакцией и что делает возможным правильный пререход состояния из одного в другое
* Машина состояний, конечный автомат, обрабатывающий транзакции в соотвествии с правилами консенсуса
* Цепь из криптографически защищеных блоков, которая является своеобразным журналом для всех проверенных и принятых транзакций
* Консенсусный алгоритм, который обеспечивает децентрализованный контроль над блокчейном, завставляя участников сотрудничать для обеспечения правил консенсуса
* Теоретически обоснованныя схема стумулирования (например затраты на обеспечение pow консенсуса и награда за блок) экономической защиты машины состояний в открытой среде.
* Один и более реализаций программного обеспечения с открытым исходным кодом ("клиенты").

Все или большинство из этих компонентов, обычно, объединено в одном программном клиенте. Для примера, в Биткоине, эталонной реализацией является проект с открытым исходным кодом _Bitcoin Core_ и реализован как _bitcoind_ клиента. В Ethereum, вместо эталонной реализации есть т.н. _reference specification_, математическое описание системы в Желтой Бумаге (Yellow Paper) (см. Further Reading). Существует несколько клиентов, которые построены согласно данной спецификации.

В прошлом, мы использовали термин "blockchain" для представления всех только что перечислиных компонентов, как на комбинация технологий, которые включают все описанные характеристики. Однако, сегодня, существует огромное разнообразие блокчейнов с отличными свойствами. Нам нужны квалификаторы, которые помогут нам понять характетрисики рассматриваемого блоккчейна, например такие как _open, public, global, decentralized, neutral,_ и _censorship-resistant_, для определения важных для блокчейна характеристик, на которые влияют данные компоенты.

Не все блокчейны созданы равными. Когда кто-то говорит вам. что что-то является блокчейном, вы скорее всего не получите ответа, вам необходимо задать множество вопросов, чтобы уточнить, что они означают, когда они использубт слово "блокчейн". Начните с вопроса про описание компонентов в предыдущем списке, затем спросите обладает ли этот блокчейн характеристиками _open, public_, и так далее.

### Рождение Ethereum

Все великие инновации решают реальные проблемы и Ethereum не исключение. Ethereum был задуман в то время, когда люди узнали приемущества модели Биткоина и попытались выйти за пределы криптовалютных прилоожений. Но разработчики столкнулись с головоломкой: им нужно было люби строить всё поверх текщей сети биткоина или создавать свой новый блокчейн. Если основываться на биткоине, то это значит жить внутри уже очерченных правил и ограничений сети и стараться находить обходные пути. Ограниченный набор типов транзакций, типов данных и размеров хранилища данных, повидимому ограничивал типы приложений, которые могли бы работать на сети Биткоина. Всё остальное требовало дополнительных слоев вне сети и это сразу бы отрицательно сказывалось на многих примемуществах использования публичного блокчейна. Для проектов, которые нуждались бы в большей свободе и гибкости блокчейна, единственным вариантом был новый блокчейн. Но это означало бы большую работу: создание всех инфраструктурных элементов, бесппрерыное тестирование и так далее

К концу 2013 года, Виталик Бутерин, юный программист и энтузиаст биткоинов, начал думать о дальнейшем расширении возможностей Bitcoin и Mastercoin (для наложения протокола, который расширил биткоин, предалгающие рудиментарные умные контракты). В октябре того года, Виталик предложил более обощенный подход к команде Mastercoin, один из которых позщволяет гибкий и доступный скриптовые (но не Тьюринг полные) контракты для замены специализирлованно языка контрактов в Mastercoin. В то время, пока команда Mastercoin была впечатлена, это предложение было слишком радикально, чтобы вписаться в их план развития.

В декабре 2013, Виталик начал делиться своей белой ьумагой, в которой была изложена идея Ethereum: Тьюринг-полный, блокчейн общего назначения. Несколько десятков человек увидили ранный вариант и дали свой фдбек, помогая Виталику разработать приложение.

Оба автора этой книги получили ранний вариант документа и прокоментировали его. Andreas M. Antonopoulos был заинтригован идеей и задал Виталику множество вопросов о испольщовании отдельного блокчейна для обеспечения соблюдения правил консенсуса при исполнении умных контрактов и реализации Тьюринг полного языка. Andreas с большим интересом продолжил следить за развитием Ethereum, но был занят написанием книги _Mastering Bitcoin_, поэтому не принимал непосредственного участия позже. Gavin Wood, однако, был один из первых людей, кто обратился к Виталику и предложил ему помощь со своими навыками программирования на C++. Gavin стал соучередителем, разработчиком и техническим директором Ethereum'а.

Как говорит Виталик в своём [посте "Ethereum Предыстория"](https://vitalik.ca/general/2017/09/14/prehistory.html): 

    Это было время, когда протокол Ethereum был полностью моим собственным творением. С этого момента, однако, новые участники начали объединяться. Самым выдающимся со стороны протокола был Gavin Wood...

    Gavin также может быть в ряды тех, кто повлиял на общую философию Ethereum, как на платформу программируемых денег с основанными на блокчейне контрактами, которые могут хранить цифровые активы и передавать их с заранее установленными правилами в универсальной вычислительной платформе. Это началось с тонких изменений в концептах и терминологии, и позже это влияние усилилось с увелицением акцента на “Web 3”, в котором Ethereum представлял собой одну из частей набор децентрализованных технологий, а два других Whisper и Swarm.

Начиная с декабря 2013, Виталик и Gavin усовершенствовали и развили идею, вместе создавая протокольный уровень, который и стал Ethereum.

Основатели Ethereum думали о блокчейне без конкретной цели, который могу бы поддерживать широкий спектр приложений, будучи _программируеммым_. Идея заключалась в том, что используя блокчейн общего назначения, такой как Ethereum, разработчик может запрограммирование своё конкретногое приложение бещ реализации нижележащих механизмов, например одноранговой сети, блокчейнв, алгоритмов консенсуа и так далее. Платформа Ethereum была спректрована, чтобы абстрагировать эти детали и предоставить детерминированную и безопасную среду программирования для децентрализованных блокчейн приложений.

Подобно Satoshi, Виталик и Gavin не просто изобрели новую технологию, они по новому соеденили новые изобретения с существующими технологиями и сделали прототип для проверки идемонстрации своих идей миру.

Основатели работали годы и уточняли видение. И 30 июля 2015, первый Ethereum блок был смайнен. Мировой компьютер начал служить миру.

__Заметка__ 
Статья Виталика Бутерина "Предыстория Ethereum'a" была опубликвана в Сентябре 2017 и показывает захватывающий вид от первого лица о самых ранних моментах Ethereum'а. Вы можете прочитать её здесь: [https://vitalik.ca/general/2017/09/14/prehistory.html](https://vitalik.ca/general/2017/09/14/prehistory.html).

### Четыре стадии разработки Ethereum

Развитие Ethereum'а запланировано на четыре различных стадии, причем в каждой стадии происходят значительные изменения. Стадия может включать подрелизы, известные как "жесткие форки", которые изменяют функциональность таким образом, что они становятся обратно несовместимыми.

Четыре основных этапа разработки имеют кодовые имена - _Frontier_, _Homestead_, _Metropolis_, и _Serenity_. Промежуточные жесткие форки, которые произошли (или запланированны) имеют кодовые названия _Ice Age_, _DAO_, _Tangerine Whistle_, _Spurious Dragon_, _Byzantium_, и _Constantinople_. Как и стадии разработки, так и промежуточные жесткие форки показаны на следющей временной шкале, которая датируется номером блока:


__Block #0__\
*Frontier* -- начальный этап Ethereum, который длился с 30 июля 2015 по март 2016.

__Block #200,000__\
*Ice Age* -- Жесткий форк для увеличения экспонциональной сложности, чтобы мотивировать переход на PoS, когда он будет готов.

__Block #1,150,000__\
*Homestead* -- Вторая стадия Ethereum, запущен в марте 2016.

__Block #1,192,000__\
*DAO* -- Жетский форк, который возместил средства жертвам взломанного контракта DAO и разделил Ethereum и Ethereum Classic на две конкурирующие системы.

__Block #2,463,000__\
*Tangerine Whistle* -- Жесткий форк, который изменит расчет газа для определенных операций ввода и вывода и очистит накопленное состояние от атаки denial-of-service (DoS), которая использовала низкую стоимость газа для этой атаки.

__Block #2,675,000__\
*Spurious Dragon* -- Жесткий форк, чтобы различные векторы DoS атак и другие очистки состояния. Кроме того, механизм защиты от повторных атак.

__Block #4,370,000__\
*Metropolis Byzantium* -- Метрополис это третяя стадия развития Ethereum, существующий на момент написания данной книги, запущен в октябре 2017. Byzantium это первый из двух жетских форков, запланированных для Metropolis.

После Byzantium в Metropolis есть ещё один жесткий форк: Constantinople. За Metropolis последует заключительный этап развития Ethereum под кодовым названием Serenity.

### Ethereum: главная цель блокчейна

The original blockchain, namely Bitcoin's blockchain, tracks the state of units of bitcoin and their ownership. You can think of Bitcoin as a distributed consensus _state machine_, where transactions cause a global _state transition_, altering the ownership of coins. The state transitions are constrained by the rules of consensus, allowing all participants to (eventually) converge on a common (consensus) state of the system, after several blocks are mined.

Ethereum is also a distributed state machine. But instead of tracking only the state of currency ownership, Ethereum tracks the state transitions of a general-purpose data store, i.e., a store that can hold any data expressible as a _key–value tuple_. A key–value data store holds arbitrary values, each referenced by some key; for example, the value "Mastering Ethereum" referenced by the key "Book Title". In some ways, this serves the same purpose as the data storage model of _Random Access Memory_ (RAM) used by most general-purpose computers. Ethereum has memory that stores both code and data, and it uses the Ethereum blockchain to track how this memory changes over time. Like a general-purpose stored-program computer, Ethereum can load code into its state machine and _run_ that code, storing the resulting state changes in its blockchain. Two of the critical differences from most general-purpose computers are that Ethereum state changes are governed by the rules of consensus and the state is distributed globally. Ethereum answers the question: "What if we could track any arbitrary state and program the state machine to create a world-wide computer operating under consensus?"

### Компоненты Ethereum'a

В Ethereum, компоненты блокчейн системы описаны в `Blockchain компоненты` и особенно:

__P2P сеть__\
Ethereum запускается на _Ethereum main network_, который адресуется на TCP порт 30303 и запускает протокол с именем _ÐΞVp2p_.

__Правила консенсуса__\
Правила консенсуса Ethereum описаны в спецификации the Yellow Paper (см.see `Дополнительное чтение`).

__Транзакции__\
Транзакции Ethereum представляют собой сетевые сообщения, которые включают (помимо всего прочего) отправителя, получателя, значение и полезную нагрузку.

__State machine__\
Ethereum state transitions are processed by the _Ethereum Virtual Machine_ (EVM), a stack-based virtual machine that executes _bytecode_ (machine-language instructions). EVM programs, called "smart contracts," are written in high-level languages (e.g., Solidity) and compiled to bytecode for execution on the EVM.

__Структура данных__\
Ethereum's state is stored locally on each node as a _database_ (usually Google's LevelDB), which contains the transactions and system state in a serialized hashed data structure called a _Merkle Patricia Tree_.

__Алгоритм консенсуса__\
Ethereum uses Bitcoin's consensus model, Nakamoto Consensus, which uses sequential single-signature blocks, weighted in importance by PoW to determine the longest chain and therefore the current state. However, there are plans to move to a PoS weighted voting system, codenamed _Casper_, in the near future.

__Economic security__\
Ethereum currently uses a PoW algorithm called _Ethash_, but this will eventually be dropped with the move to PoS at some point in the future.

__Клиенты__\
Ethereum has several interoperable implementations of the client software, the most prominent of which are _Go-Ethereum_ (_Geth_) and _Parity_.

#### Дополнительное чтение

The following references provide additional information on the technologies mentioned here:

* Желтая бумага Ethereum: https://ethereum.github.io/yellowpaper/paper.pdf
* The Beige Paper, a rewrite of the Yellow Paper for a broader audience in less formal language: https://github.com/chronaeon/beigepaper
* ÐΞVp2p network protocol: https://github.com/ethereum/wiki/wiki/%C3%90%CE%9EVp2p-Wire-Protocol
* Ethereum Virtual Machine list of resources: https://github.com/ethereum/wiki/wiki/Ethereum-Virtual-Machine-(EVM)-Awesome-List
* LevelDB database (used most often to store the local copy of the blockchain): http://leveldb.org
* Merkle Patricia trees: https://github.com/ethereum/wiki/wiki/Patricia-Tree
* Ethash PoW algorithm: https://github.com/ethereum/wiki/wiki/Ethash
* Casper PoS v1 Implementation Guide: https://github.com/ethereum/research/wiki/Casper-Version-1-Implementation-Guide
* Клиент Go-Ethereum (Geth): https://geth.ethereum.org/
* Клиент Parity Ethereum: https://parity.io/

### Ethereum и полнота по Тьюрингу

As soon as you start reading about Ethereum, you will immediately encounter the term "Turing complete." Ethereum, they say, unlike Bitcoin, is Turing complete. What exactly does that mean?

The term refers to English mathematician Alan Turing, who is considered the father of computer science. In 1936 he created a mathematical model of a computer consisting of a state machine that manipulates symbols by reading and writing them on sequential memory (resembling an infinite-length paper tape). With this construct, Turing went on to provide a mathematical foundation to answer (in the negative) questions about _universal computability_, meaning whether all problems are solvable. He proved that there are classes of problems that are uncomputable. Specifically, he proved that the _halting problem_ (whether it is possible, given an arbitrary program and its input, to determine whether the program will eventually stop running) is not solvable.

Alan Turing further defined a system to be _Turing complete_ if it can be used to simulate any Turing machine. Such a system is called a _Universal Turing machine_ (UTM).

Ethereum's ability to execute a stored program, in a state machine called the Ethereum Virtual Machine, while reading and writing data to memory makes it a Turing-complete system and therefore a UTM. Ethereum can compute any algorithm that can be computed by any Turing machine, given the limitations of finite memory.

Ethereum's groundbreaking innovation is to combine the general-purpose computing architecture of a stored-program computer with a decentralized blockchain, thereby creating a distributed single-state (singleton) world computer. Ethereum programs run "everywhere," yet produce a common state that is secured by the rules of consensus.

#### Полнота по Тьюрингу, как "фича"

Hearing that Ethereum is Turing complete, you might arrive at the conclusion that this is a _feature_ that is somehow lacking in a system that is Turing incomplete. Rather, it is the opposite. Turing completeness is very easy to achieve; in fact, http://bit.ly/2ABft33[the simplest Turing-complete state machine known]  has 4 states and uses 6 symbols, with a state definition that is only 22 instructions long. Indeed, sometimes systems are found to be "accidentally Turing complete." A fun reference of such systems can be found at http://bit.ly/2Og1VgX[].

However, Turing completeness is very dangerous, particularly in open access systems like public blockchains, because of the halting problem we touched on earlier. For example, modern printers are Turing complete and can be given files to print that send them into a frozen state. The fact that Ethereum is Turing complete means that any program of any complexity can be computed by Ethereum. But that flexibility brings some thorny security and resource management problems. An unresponsive printer can be turned off and turned back on again. That is not possible with a public blockchain.

#### Смысл полноты по Тьюрингу

Turing proved that you cannot predict whether a program will terminate by simulating it on a computer. In simple terms, we cannot predict the path of a program without running it. Turing-complete systems can run in "infinite loops," a term used (in oversimplification) to describe a program that does not terminate. It is trivial to create a program that runs a loop that never ends. But unintended never-ending loops can arise without warning, due to complex interactions between the starting conditions and the code. In Ethereum, this poses a challenge: every participating node (client) must validate every transaction, running any smart contracts it calls. But as Turing proved, Ethereum can't predict if a smart contract will terminate, or how long it will run, without actually running it (possibly running forever). Whether by accident or on purpose, a smart contract can be created such that it runs forever when a node attempts to validate it. This is effectively a DoS attack. And of course, between a program that takes a millisecond to validate and one that runs forever are an infinite range of nasty, resource-hogging, memory-bloating, CPU-overheating programs that simply waste resources. In a world computer, a program that abuses resources gets to abuse the world's resources. How does Ethereum constrain the resources used by a smart contract if it cannot predict resource use in advance?

To answer this challenge, Ethereum introduces a metering mechanism called _gas_. As the EVM executes a smart contract, it carefully accounts for every instruction (computation, data access, etc.). Each instruction has a predetermined cost in units of gas. When a transaction triggers the execution of a smart contract, it must include an amount of gas that sets the upper limit of what can be consumed running the smart contract. The EVM will terminate execution if the amount of gas consumed by computation exceeds the gas available in the transaction. Gas is the mechanism Ethereum uses to allow Turing-complete computation while limiting the resources that any program can consume.

The next question is, 'how does one get gas to pay for computation on the Ethereum world computer?' You won't find gas on any exchanges. It can only be purchased as part of a transaction, and can only be bought with ether. Ether needs to be sent along with a transaction and it needs to be explicitly earmarked for the purchase of gas, along with an acceptable gas price. Just like at the pump, the price of gas is not fixed. Gas is purchased for the transaction, the computation is executed, and any unused gas is refunded back to the sender of the transaction.

### From General-Purpose Blockchains to Decentralized Applications (DApps)

Ethereum started as a way to make a general-purpose blockchain that could be programmed for a variety of uses. But very quickly, Ethereum's vision expanded to become a platform for programming DApps. DApps represent a broader perspective than smart contracts. A DApp is, at the very least, a smart contract and a web user interface. More broadly, a DApp is a web application that is built on top of open, decentralized, peer-to-peer infrastructure services.

A DApp is composed of at least:

- Smart contracts on a blockchain
- A web frontend user interface

In addition, many DApps include other decentralized components, such as:

- A decentralized (P2P) storage protocol and platform
- A decentralized (P2P) messaging protocol and platform

__Заметка__
You may see DApps spelled as _&#208;Apps_. The &#208; character is the Latin character called "ETH," alluding to Ethereum. To display this character, use the Unicode codepoint +0xD0+, or if necessary the HTML character entity +eth+ (or decimal entity +#208+).

### Третяя эра Интернета

In 2004 the term "Web 2.0" came to prominence, describing an evolution of the web toward user-generated content, responsive interfaces, and interactivity. Web 2.0 is not a technical specification, but rather a term describing the new focus of web applications.

The concept of DApps is meant to take the World Wide Web to its next natural evolutionary stage, introducing decentralization with peer-to-peer protocols into every aspect of a web application. The term used to describe this evolution is _web3_, meaning the third "version" of the web. First proposed by Gavin Wood, web3 represents a new vision and focus for web applications: from centrally owned and managed applications, to applications built on decentralized protocols.

In later chapters we'll explore the Ethereum web3.js JavaScript library, which bridges JavaScript applications that run in your browser with the Ethereum blockchain. The web3.js library also includes an interface to a P2P storage network called _Swarm_ and a P2P messaging service called _Whisper_. With these three components included in a JavaScript library running in your web browser, developers have a full application development suite that allows them to build web3 DApps.

### Культура разработки Ethereum'а

So far we've talked about how Ethereum's goals and technology differ from those of other blockchains that preceded it, like Bitcoin. Ethereum also has a very different development culture.

In Bitcoin, development is guided by conservative principles: all changes are carefully studied to ensure that none of the existing systems are disrupted. For the most part, changes are only implemented if they are backward compatible. Existing clients are allowed to opt-in, but will continue to operate if they decide not to upgrade.

In Ethereum, by comparison, the community's development culture is focused on the future rather than the past. The (not entirely serious) mantra is "move fast and break things." If a change is needed, it is implemented, even if that means invalidating prior assumptions, breaking compatibility, or forcing clients to update. Ethereum's development culture is characterized by rapid innovation, rapid evolution, and a willingness to deploy forward-looking improvements, even if this is at the expense of some backward compatibility.

What this means to you as a developer is that you must remain flexible and be prepared to rebuild your infrastructure as some of the underlying assumptions change. One of the big challenges facing developers in Ethereum is the inherent contradiction between deploying code to an immutable system and a development platform that is still evolving. You can't simply "upgrade" your smart contracts. You must be prepared to deploy new ones, migrate users, apps, and funds, and start over.

Ironically, this also means that the goal of building systems with more autonomy and less centralized control is still not fully realized. Autonomy and decentralization require a bit more stability in the platform than you're likely to get in Ethereum in the next few years. In order to "evolve" the platform, you have to be ready to scrap and restart your smart contracts, which means you have to retain a certain degree of control over them.

But, on the positive side, Ethereum is moving forward very fast. There's little opportunity for "bike-shedding," an expression that means holding up development by arguing over minor details such as how to build the bicycle shed at the back of a nuclear power station. If you start bike-shedding, you might suddenly discover that while you were distracted the rest of the development team changed the plan and ditched bicycles in favor of autonomous hovercraft.

Eventually, the development of the Ethereum platform will slow down and its interfaces will become fixed. But in the meantime, innovation is the driving principle. You'd better keep up, because no one will slow down for you.

### Зачем учить Ethereum?

Blockchains have a very steep learning curve, as they combine multiple disciplines into one domain: programming, information security, cryptography, economics, distributed systems, peer-to-peer networks, etc. Ethereum makes this learning curve a lot less steep, so you can get started quickly. But just below the surface of a deceptively simple environment lies a lot more. As you learn and start looking deeper, there's always another layer of complexity and wonder.

Ethereum is a great platform for learning about blockchains and it's building a massive community of developers, faster than any other blockchain platform. More than any other, Ethereum is a _developer's blockchain_, built by developers for developers. A developer familiar with JavaScript applications can drop into Ethereum and start producing working code very quickly. For the first few years of Ethereum's life, it was common to see T-shirts announcing that you can create a token in just five lines of code. Of course, this is a double-edged sword. It's easy to write code, but it's very hard to write _good_ and _secure_ code.

### Чему эта книга научит вас?

This book dives into Ethereum and examines every component. You will start with a simple transaction, dissect how it works, build a simple contract, make it better, and follow its journey through the Ethereum system.

You will learn not only how to use Ethereum -- how it works -- but also why it is designed the way it is. You will be able to understand how each of the pieces works, and how they fit together and why.