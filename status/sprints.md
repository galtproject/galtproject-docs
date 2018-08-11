# Sprint 1

## Web3 Application

## GaltToken
 - Все готово

## SpaceToken

### Методы
  - Разработка метода [encode](../ru/contracts/SpaceToken.md#encode), нужно разработать
    - из 5-бит пакетов нереализовано 
      - написать unit test, 15 минут
    - из 8-бит пакетов вообще нереализовано, 2 часа
  - Разработка метода [decode](../ru/contracts/SpaceToken.md#decode), нужно разработать
    - из 5-бит пакетов нереализовано
      - написать unit test, 15 минут
    - из 8-бит пакетов вообще нереализовано, 2 часа
  - Разработка метода mint (выпуск токена), готово на 90%
    - Нужно опеределить права (роли) на вызов метода mint, 15 мин
    - Написать код на проверку прав метода mint, 1 час
  - Перенести метод mintPack в контракт SplitMerge, Выпилить в будущем
  - Перенести метод swapToPack в контракт SplitMerge, Выпилить в будущем
    - Убрать импорт контракта SplitMerge
  - Входят в стандарт и должны быть включены методы из контрактов:
    - ERC721Token, реализовано
    - Ownable, реализовано
    - Initializable, реализовано
  - generatePackTokenId
    - Написать Unit test, 10 мин
  - isPack
    - Написать Unit test, 10 мин
  - isGeohash
    - Написать Unit test, 10 мин
  - tokenIdToGeohash
    - Написать Unit test, 10 мин
  - geohashToTokenId
    - Написать Unit test, 10 мин
  - setTokenURI
    - Нужно опеределить права на вызов метода setTokenURI, 15 мин
    - Написать код на проверку прав метода setTokenURI, 30 мин
  - burn
    - Нужно опеределить права на вызов метода burn, 15 мин
    - Написать код на проверку прав метода burn, 30 мин
  - canTransfer
    - Написать Unit test, 15 мин

## PlotManager

### Методы
 - Наследование и импорт стандартных контрактов (Initializable, Ownable)
   - Проверить правильность наследования и импорта, ???
 - Метод initialize
   - Определить переменные
     - Размер комиссии за создание заявки
     - Проценты комиссии за проверку заявки, получаемый Galt Space и Валидатором
     - address SpaceToken
     - address SplitMerge
 - Метод addValidator
   - Покрыть тестами
 - Метод removeValidator
   - Покрыть тестами
 - Метод applyForPlotOwnership
   - Перевод X эфиров в контракт
   - Выполнять mint одного geohash или использование готового, если он принадлежит контракту PlotManager, mint упаковки, обмен одного geohash на упаковку с записью во все мапинги SplitMerge и созданием заявки со статусом Новая - одной транзакцией.
     - mint одного geohash на контракт PlotManager
     - mint упаковки на контракт SplitMerge
     - обмен одного geohash на упаковку
     - запись во все мапинги SplitMerge
     - создание заявки со статусом Новая
 - Метод addGeohashesToApplication
   - Проверка наличия конкрентных токенов на контракте PlotManager
   - mint geohash в случае отсутствия
   - Добавление geohash в упаковку
   - Проверка статуса заявки
 - Метод submitApplication
   - Изменение статуса заявки
   - Проверка статуса заявки
 - Метод changePack
   - Вызов метода контракта SplitMerge который создает новую упаковку, меняет статус старой упаковки на частично-разобранную, переносит один geohash из старой упаковки в новую.
 - Метод transferToPack
   - Вызов метода контракта SplitMerge и перенос одного или нескольких geohash из старой упаковки в новую со ссылкой на заявку.
 - Метод removeGeohashFromPack
   - Вызов метода контракта SplitMerge, который передает токен geohash от контракта SplitMerge контракту PlotManager и меняет маппинг geohash -> упаковка для заявки в статусе Новая.
 - Метод approveApplication
   - Проверить статус заявки
   - Получить на входе hash
   - Сравнить hashes
   - Передать токен упаковки заявителю
   - Изменить статус заявки на `Утверждена`
 - Метод revertApplication
   - Изменить статус заявки на `Новая`
 - Метод rejectApplication
   - Изменить статус заявки на `Отказ`
 - Метод claimValidatorReward
   - для заявок со статусом утверждена для перечисления эфиров валидаторам без проверок
   - для заявок со статусом Отказ проверка для упаковки указанной в заявке, что количество geohash в упаковке равно нулю 
 
## SplitMerge

## TerritoryCrowdsale

## SpaceAuctionPack

## SPACEAuctionRegistry

## GALTGenesisRegistry

## Explorer Testnet

## Solidity Telegram Bot

## TypeScript Telegram Bot

 - Bintan
 - Маркетинговый бот (общего назначения)


