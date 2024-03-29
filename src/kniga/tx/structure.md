## Структура транзакции

Сначала давайте рассмотрим базовую структуру транзакции, как она сериализуется и передается в сети Ethereum. Каждый клиент и приложение, получающее сериализованную транзакцию, будет хранить ее в памяти, используя свою собственную внутреннюю структуру данных, возможно, дополненную метаданными, которых нет в самой сериализованной транзакции. Сетевая сериализация - это единственная стандартная форма транзакции.

Транзакция - это сериализованное двоичное сообщение, содержащее следующие данные:

### Nonce
Порядковый номер, выдаваемый отправляющим EOA, используемый для предотвращения повторного воспроизведения сообщения.

### Gas price
Количество ether (в wei), которое отправитель готов заплатить за каждую единицу газа

### Gas limit
Максимальное количество газа, которое отправитель готов использовать для данной транзакции

### Recipient
Адрес назначения в Ethereum

### Value
Количество ether (в wei) для отправки в пункт назначения

### Data
Полезная нагрузка в виде двоичных данных переменной длины

### v, r, s
Три компонента цифровой подписи ECDSA создающего EOA

Структура сообщения транзакции сериализуется с помощью схемы кодирования _Recursive Length Prefix (RLP)_, которая была создана специально для простой, байтовой сериализации данных в Ethereum. Все числа в Ethereum кодируются как большие целые числа, длина которых кратна 8 битам.

Обратите внимание, что метки полей (__to__, __gas_limit__ и т.д.) показаны здесь для наглядности, но не являются частью сериализованных данных транзакции, которые содержат значения полей в RLP-кодировке. В целом, RLP не содержит никаких разделителей или меток полей. Префикс длины RLP используется для определения длины каждого поля. Все, что превышает определенную длину, относится к следующему полю в структуре.

Хотя это фактическая структура передаваемой транзакции, большинство внутренних представлений и визуализаций пользовательского интерфейса украшают ее дополнительной информацией, полученной из транзакции или из блокчейна.

Например, вы можете заметить, что в адресе, идентифицирующем EOA отправителя, нет данных "from". Это потому, что открытый ключ EOA может быть получен из компонентов __v,r,s__ подписи ECDSA. Адрес, в свою очередь, может быть получен из открытого ключа. Когда вы видите транзакцию с полем "__from__", это поле было добавлено программным обеспечением, используемым для визуализации транзакции. Другие метаданные, часто добавляемые к транзакции клиентским программным обеспечением, включают номер блока (когда он добыт и включен в блокчейн) и идентификатор транзакции (вычисленный хэш). Опять же, эти данные получены из транзакции и не являются частью самого сообщения о транзакции.
