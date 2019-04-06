# ACL
## Проблема.

Необходимо разработать систему управления доступами для вызовов между контрактами всех модулей.

## Варианты решения.
### Децентрализованные варианты
#### 1. Ownership
Контракт имеет 1 owner-а, опционально он может передавать свой ownership другому адресу
Пример:
* OpenZeppelin/Ownership - https://github.com/OpenZeppelin/openzeppelin-solidity/blob/master/contracts/ownership/Ownable.sol
* DS-Auth - https://dapp.tools/dappsys/ds-auth.html

#### 2. Roles
Каждый контракт имеет таблицу ролей, на каждую роль может быть назначено любое кол-во адресов (>=0).

Пример:
* OpenZeppelin/Roles - https://github.com/OpenZeppelin/openzeppelin-solidity/blob/master/contracts/access/Roles.sol
* DS-Roles - https://dapp.tools/dappsys/ds-roles.html

Минусы:
* Необходимо задавать роли в каждом контракте. В случае с контрактами мультисига, фондов, локеров и т.п. Например, в случае изменения контракта ClaimManager, кто-то должен бдует в каждом под-контракте мультисига поменять адрес этого контракта для соответствующей роли. Owner не будет этим заниматься точно, особенно, когда это будет контракт голосования. Голосованиям самого мультисига это право предоставлять так же сомнительно.

### Центарлизованные варианты
#### 3. Централизованный реестр контрактов.
Имеем глобальный контракт GGR, каждый контракт числится в нем по своему ключу:
```solidity
// contractKey => contractAddress
mapping(bytes32 => address) registry;
```


#### 4. Центарализованный реестр ролей.
Имеем глобальный контракт ACL, адреса назназначаются на конкретные роли. Один контракт может иметь >=0 ролей.

```solidity
// roleKey => grantedAddressesSet
mapping(bytes32 => AddressSet) registry;
```


## Необходимые права
### Реестр ролей

* ARBITRATION_STAKE_SLASHER
	* [ClaimManager] <=> [Arbitration/ArbitratorStakeAccounting]
* ORACLE_STAKE_SLASHER
	* [ClaimManager] <=> [Arbitration/OracleStakesAccounting]
* ORACLE_MODIFIER (currently Oracles contract resides at global-level, but it will be moved to Arbitration level later)
	* [NewOracleManager] <=> [Arbitration/Oracles]
	* [UpdateOracleManager] <=> [Arbitration/Oracles]
* SPACE_TOKEN_MINTER
	* [SplitMerge] <=> [SpaceToken]
* GEO_DATA_MANAGER
	* [PlotManager] <=> [SplitMerge]
	* [PlotClarificationManager] <=> [SplitMerge]
	* [ModifySpaceManager] <=> [SplitMerge]
* SPACE_REPUTATION (Information about locked space reputation)
	* [SpaceRA] <=> [Arbitration/DelegateSpaceReputation]
* GALT_REPUTATION (Information about locked space reputation)
	* [GaltRA] <=> [Arbitration/DelegateGaltReputation]

## Управление правами в других проектах.
Многим проектам не требуется комплексное управление правами и они используют просто dependency injection двух типов:
* единожды в конструкторе
* изменяемые owner-ом динамически с помощью setters

Наиболее подходящий для нас динамический вариант нашел в Aragon - https://github.com/aragon/aragonOS/tree/dev/contracts/acl

## Сценарий
1. (Списание стейков)
* Owner назначает  `oracle_stake_slasher`, `arbitartor_stake_slasher` роли контракту ClaimManager.
* Каждый контракт `ArbitartorStakeAccounting` спрашивает ACL, имеет ли текущий msg.sender роль `arbitartor_stake_slasher` (адрес ACL получает через GGR)
* При изменении адреса контракта ClaimManager: 
	1) Заменяет текущий адрес ClaimManager в ApplicationRegistry
	2) Удаляет старый адрес ClaimManager из ACL роли `arbitartor_stake_slasher`
	3) Добавляет новый адрес ClaimManager на роль `arbitartor_stake_slasher`
