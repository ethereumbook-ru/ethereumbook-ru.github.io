## Введение в языки Ethereum

EVM - это виртуальная машина, которая выполняет специальную форму кода, называемую EVM bytecode, аналогично процессору вашего компьютера, который выполняет машинный код, такой как x86_64. Мы рассмотрим работу и язык EVM гораздо более подробно в [evm_chapter]. В этом разделе мы рассмотрим, как пишутся смарт-контракты для запуска на EVM.

Хотя можно программировать смарт-контракты непосредственно в байткоде, байткод EVM довольно громоздкий и очень сложный для чтения и понимания программистами. Вместо этого большинство разработчиков Ethereum используют язык высокого уровня для написания программ и компилятор для их преобразования в байткод.

Хотя любой язык высокого уровня может быть адаптирован для написания смарт-контрактов, адаптация произвольного языка для компиляции в байткод EVM является довольно громоздким занятием и в целом приведет к некоторой путанице. Смарт-контракты работают в сильно ограниченной и минималистичной среде исполнения (EVM). Кроме того, необходимо иметь специальный набор системных переменных и функций, специфичных для EVM. Поэтому проще создать язык смарт-контрактов с нуля, чем язык общего назначения, подходящий для написания смарт-контрактов. В результате появилось несколько специализированных языков для программирования смарт-контрактов. В Ethereum есть несколько таких языков, а также компиляторы, необходимые для создания байткода, исполняемого EVM.

В целом, языки программирования можно разделить на две парадигмы: декларативную и императивную, также известные как функциональная и процедурная, соответственно. В декларативном программировании мы пишем функции, которые выражают логику программы, но не ее ход. Декларативное программирование используется для создания программ, в которых отсутствуют побочные эффекты, что означает отсутствие изменений состояния за пределами функции. К языкам декларативного программирования относятся Haskell и SQL. Императивное программирование, напротив, заключается в том, что программист пишет набор процедур, которые объединяют логику и поток программы. К императивным языкам программирования относятся C++ и Java. Некоторые языки являются "гибридными", то есть они поощряют декларативное программирование, но также могут быть использованы для выражения императивной парадигмы программирования. К таким гибридам относятся Lisp, JavaScript и Python. В целом, любой императивный язык можно использовать для написания в декларативной парадигме, но это часто приводит к неэлегантному коду. Для сравнения, чисто декларативные языки не могут быть использованы для написания в императивной парадигме. В чисто декларативных языках нет "переменных".

Хотя императивное программирование чаще всего используется программистами, бывает очень трудно писать программы, которые выполняются именно так, как ожидается. Способность любой части программы изменять состояние любой другой части затрудняет рассуждения о выполнении программы и создает множество возможностей для ошибок. Декларативное программирование, для сравнения, позволяет легче понять, как поведет себя программа: поскольку оно не имеет побочных эффектов, любую часть программы можно понять изолированно.

В смарт-контрактах ошибки буквально стоят денег. Поэтому критически важно составлять смарт-контракты без непредвиденных последствий. Для этого вы должны быть в состоянии четко сформулировать ожидаемое поведение программы. Таким образом, декларативные языки играют гораздо большую роль в смарт-контрактах, чем в программах общего назначения. Тем не менее, как вы увидите, наиболее широко используемый язык для смарт-контрактов (Solidity) является императивным. Программисты, как и большинство людей, сопротивляются изменениям!

В настоящее время поддерживаются следующие языки программирования высокого уровня для смарт-контрактов (в порядке возрастания):

#### LLL
Функциональный (декларативный) язык программирования с синтаксисом, похожим на Lisp. Это был первый язык высокого уровня для смарт-контрактов Ethereum, но сегодня он используется редко.
#### Serpent
Процедурный (императивный) язык программирования с синтаксисом, похожим на Python. Может также использоваться для написания функционального (декларативного) кода, хотя он не полностью свободен от побочных эффектов.
#### Solidity
Процедурный (императивный) язык программирования с синтаксисом, похожим на JavaScript, C++ или Java. Самый популярный и часто используемый язык для смарт-контрактов Ethereum.
#### Vyper
Недавно разработанный язык, похожий на Serpent и снова с Python-подобным синтаксисом. Предназначен для приближения к чисто функциональному Python-подобному языку, чем Serpent, но не для замены Serpent.
####  Bamboo
Новый язык, разработанный под влиянием Erlang, с явными переходами состояний и без итеративных потоков (циклов). Предназначен для уменьшения побочных эффектов и повышения проверяемости. Очень новый и еще не получил широкого распространения.

Как видите, существует множество языков, из которых можно выбирать. Однако из всех них Solidity, безусловно, является самым популярным, вплоть до того, что де-факто является языком высокого уровня Ethereum и даже других EVM-подобных блокчейнов. Мы проведем большую часть нашего времени, используя Solidity, но также изучим некоторые примеры на других языках высокого уровня, чтобы получить представление об их различных философиях.