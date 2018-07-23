# Galt Токен - Описание

## Описание проблемы
Проекту необходим ERC20 контракт и токен для учета вложений участников проекта в [Фонды](https://github.com/andromedaspace/galtproject-docs/blob/master/ru/Golossary.md#%D0%A4%D0%BE%D0%BD%D0%B4), которые будут развивать [Территории](https://github.com/andromedaspace/galtproject-docs/blob/master/ru/Golossary.md#%D0%A2%D0%B5%D1%80%D1%80%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D1%8F).

## Основные задачи токена

## Спецификация контракта
* Название токена (name) - `GALT Token`
* Символ токена (symbol) - `GALT`
* Кол-во знаков после запятой (decimals) - `18` (по аналогии с самим эфиром)
* Макс. возможное кол-во выпущенных токенов - `2^256/1e18 = 1.1579209e+59`

Контракт использует имплементацию стандарта [OpenZeppelin Mintable ERC20](https://github.com/OpenZeppelin/openzeppelin-solidity/tree/master/contracts/token/ERC20).

## Особенности реализации на Solidity

## Особенности реализации на TypeScript

## Неоднозначные вопросы и ответы на них
