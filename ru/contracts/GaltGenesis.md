# Контракт GALTGenesis - Требования

## Ссылки на термины
[Территория](https://github.com/andromedaspace/galtproject-docs/blob/npopeka-review-big/ru/Glossary.md#%D0%A2%D0%B5%D1%80%D1%80%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D1%8F)
[Аукцион земли](https://github.com/andromedaspace/galtproject-docs/blob/npopeka-review-big/ru/Glossary.md#%D0%90%D1%83%D0%BA%D1%86%D0%B8%D0%BE%D0%BD-%D0%97%D0%B5%D0%BC%D0%BB%D0%B8)
[Владелец Территории](https://github.com/andromedaspace/galtproject-docs/blob/npopeka-review-big/ru/Glossary.md#%D0%92%D0%BB%D0%B0%D0%B4%D0%B5%D0%BB%D0%B5%D1%86-%D0%A2%D0%B5%D1%80%D1%80%D0%B8%D1%82%D0%BE%D1%80%D0%B8)
[Оператор Ввода](https://github.com/andromedaspace/galtproject-docs/blob/npopeka-review-big/ru/Glossary.md#%D0%9E%D0%BF%D0%B5%D1%80%D0%B0%D1%82%D0%BE%D1%80-%D0%B2%D0%B2%D0%BE%D0%B4%D0%B0-%D0%A2%D0%B5%D1%80%D1%80%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D0%B8-%D0%B2-%D0%BF%D1%80%D0%BE%D0%B5%D0%BA%D1%82-%D0%B8%D0%BB%D0%B8-%D0%9E%D0%BF%D0%B5%D1%80%D0%B0%D1%82%D0%BE%D1%80-%D0%B2%D0%B2%D0%BE%D0%B4%D0%B0)
[Фонд](https://github.com/andromedaspace/galtproject-docs/blob/npopeka-review-big/ru/Glossary.md#%D0%A4%D0%BE%D0%BD%D0%B4-%D0%9F%D1%80%D0%BE%D0%B5%D0%BA%D1%82%D0%B0-%D0%B8%D0%BB%D0%B8-%D0%A4%D0%BE%D0%BD%D0%B4)
[GALT](https://github.com/andromedaspace/galtproject-docs/blob/npopeka-review-big/ru/Glossary.md#galt)
[Участник проекта](https://github.com/andromedaspace/galtproject-docs/blob/npopeka-review-big/ru/Glossary.md#%D0%A3%D1%87%D0%B0%D1%81%D1%82%D0%BD%D0%B8%D0%BA-%D0%9F%D1%80%D0%BE%D0%B5%D0%BA%D1%82%D0%B0)
[Проект](https://github.com/andromedaspace/galtproject-docs/blob/npopeka-review-big/ru/Glossary.md#%D0%9F%D1%80%D0%BE%D0%B5%D0%BA%D1%82)
[Генезис GALT Территории](https://github.com/andromedaspace/galtproject-docs/blob/npopeka-review-big/ru/Glossary.md#%D0%93%D0%B5%D0%BD%D0%B5%D0%B7%D0%B8%D1%81-galt-%D0%A2%D0%B5%D1%80%D1%80%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D0%B8)
[Земельный участок](https://github.com/andromedaspace/galtproject-docs/blob/npopeka-review-big/ru/Glossary.md#%D0%97%D0%B5%D0%BC%D0%B5%D0%BB%D1%8C%D0%BD%D1%8B%D0%B9-%D1%83%D1%87%D0%B0%D1%81%D1%82%D0%BE%D0%BA-%D0%B8%D0%BB%D0%B8-%D1%83%D1%87%D0%B0%D1%81%D1%82%D0%BE%D0%BA-%D0%B7%D0%B5%D0%BC%D0%BB%D0%B8)

## Описание проблем
- для создания экономики необходимо выпустить токены GALT, который будет выполнять функцию обьекта долевой собственности на Территорию и пая инвестиционного Фонда, который будет ее развивать;
- для покупки земель на Аукционе земли и взаимодействия с другим функционалом Проекта у Участников проекта должна быть возможность купить токены GALT за ETH на этапе Генезиса GALT Территории;
- может быть неограниченное количество параллельных Генезисов GALT Территории на разные Территории для привлечения дополнительных средств для их развития;
- генезис может запускать контракт Аукциона земли на Территорию при запуске Генезиса GALT Территории или при его завершении;
- выпуск GALT на конкретную Территорию должен быть фиксирован по времени, по сумме выпущенных GALT и по количеству привлекаемых Эфиров;
- привлекаемые Эфиры нужно распределять между Оператором ввода Территории, Владельцем Территории и Фондом;

## Цели контракта
- Обеспечить выпуск GALT токенов;
- Обеспечить покупку GALT токенов любому пользователю за ETH;
- Обеспечить запуск Аукциона земли на Территорию в начале или при завершении Генезиса GALT Территории;
- Обеспечить несколько сценариев реализации выпуска GALT;
- Обеспечить уничтожение непроданных GALT;
- Обеспечить возврат Эфиров, если цель по привлечению Эфиров не будет достигнута;

## Ограничения
Существует 2 принципиальных варианта исполнения:
- Тип№1: Генезис GALT Территории продает большое количество GALT без зафиксированной цели в Эфирах. Генезис GALT Территории считается успешным при привлечении любой сумму эфиров. Токены GALT передаются Участникам проекта сразу после перечисления Эфиров. Не распределенные токены GALT уничтожаются после завершения выполнения Генезис GALT Территории.
- Тип№2: Генезис GALT Территории продает фиксированное количество GALT за фиксированное количество ETH. Генезис GALT Территории выполняется фиксированное время. Если по истечении заданного времени Цель в количестве Эфиров не достигнута, то все выпущенные GALT уничтожаются, а Эфиры можно забрать обратно. Если цель достигнута, то те, кто перечислял Эфиры на контракт получают GALT, а те, кто должен получить Эфиры - Эфир.

## Входные параметры

| Параметр | Название параметра | Контракт - источник | Тип данных |
|----------|----------------| --------------- | ------------- |
|Количество выпускаемых токенов GALT на Территорию|GaltMintAmmount|Контракт CreateTerritory|uint|
|Геохеши Территории|TerritoryID|Контракт CreateTerritory|массив string|
|Адрес Контракта Аукциона земли|LandAuctionAdress|Контракт CreateTerritory|adress|
|id Генезиса|GenesisID|Контракт CreateTerritory|adress|
|Количество привлекамых Эфиров|ETHAmmount|Контракт CreateTerritory|uint|
|Признак запуска Аукциона земли на Территорию (В начала / в конце)|AuctionStartType|Контракт CreateTerritory|string|
|Признак типа  Генезиса GALT Территории (Тип 1 / Тип 2)|GALTGenesysType|Контракт CreateTerritory|string|
|Длительность проведения Генезиса| GenesisDuration|Контракт CreateTerritory|day|
|Адрес Оператора ввода|TerritoryOperatorAdress|Контракт CreateTerritory|adress|
|Адрес Владельца Территории|TerritoryOwnerAdress|Контракт CreateTerritory|adress|
|Адрес Фонда|TerritoryFundAdress|Контракт CreateTerritory|adress|

## Сценарий контракта
### Сценарий 1: GALTGenesis
1. При деплое контракта происходит mint N GALT токенов на контракт GALTGenesis. ETH полученные при продаже GALT токенов идут на multisig.
2. После выпуска каждый пользователь на этапе GALTGenesis, который длится T времени ( T - 3 месяца ), может купить GALT токены за ETH.
3. Пользователь А отправляет 1 ETH на контракт GALTGenesis:

До выполнения Транзакции пользователя А:

| Адрес пользователя | Сумма отправленных пользователем ETH за раунд | Баланс пользователя в ETH | Баланс пользователя в GALT |
| ---------- | --------------- | ------ | ------ |
| 0x477...b65 | 22 | 100 | 0 |

После выполнения Транзакции пользователя А:

| Адрес пользователя | Сумма отправленных пользователем ETH за раунд | Баланс пользователя в ETH | Баланс пользователя в GALT |
| ---------- | --------------- | ------ | ------ |
| 0x477...b65 | 22 | 99 | 1000 |

4. Контракт GALTGenesis проверяет, достаточно ли токенов GALT на балансе и достаточно ли ETH у пользователя при курсе 1 ETH = 1000 GALT. После успешной проверки контракт производит транзакцию в ETH с адреса пользователя на multisig и GALT токенов с контракта GALTGenesis на адрес пользователя. X% от купленных GALT токенов отправляется на отдельный "multisig команды".
5. На момент окончания времени T, если на балансе GALTGenesis multisig остались GALT токены, любой пользователь, который хочет купить GALT токены инициирует метод burn, который уничтожает все оставшиеся токены и выставляет флаг об окончании GALTGenesis в true. ETH, отправленный пользователем при покупке будет возвращен за исключением вычета газа. Все последующие пользователи, которые будут инициировать покупку GALT токенов получат ошибку при транзакции с возвращением ETH на счета.

## Спецификация контракта
- Наследуется от OpenZeppelin Crowdsale[2] контракта
- Использует OpenZeppelin TimedCrowdsale[3] для обеспечения периода действия контракта
- Рейт продажи определяется при деплое контракта и не может быть изменен в процессе действия контракта
- Количество GALT токенов определяется исходя из требований моделирования экономики контрактов
- Завершение действия контракта происходит по истечению установленного времени или по факту продажи всех GALT токенов на контракте GALTGenesis

## Детальный Сценарий пользователя и описание интерфейса
[Ссылка на сценарий пользователя и описание интерфейса](https://www.mindmeister.com/1108202997?t=8pWYATCo39)

## Особенности реализации на Solidity

## Особенности реализации на TypeScript

## Неоднозначные вопросы и ответы на них
### multisig команды ли? Что именно он должен представлять?

### Какой процент от купленных токенов идет на multisig команды?

## Референсы
1. [GALT Токен](./GALT-Токен.md)
2. [OpenZeppelin Crowdsale](https://github.com/OpenZeppelin/openzeppelin-solidity/blob/master/contracts/crowdsale/Crowdsale.sol)
3. [OpenZeppelin TimedCrowdsale](https://github.com/OpenZeppelin/openzeppelin-solidity/blob/master/contracts/crowdsale/validation/TimedCrowdsale.sol)
## Контракты
1. Контракт [CreateTerritory](https://github.com/andromedaspace/galtproject-docs/blob/npopeka-review-big/ru/contracts/CreateTerritory.md#%D0%92%D0%B2%D0%BE%D0%B4-%D0%BD%D0%BE%D0%B2%D0%BE%D0%B9-%D1%82%D0%B5%D1%80%D1%80%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D0%B8---%D0%94%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82%D0%B0%D1%86%D0%B8%D1%8F)
