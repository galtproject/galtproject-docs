# ArbitratorVoting contract

## Мотивация

Ввиду технических ограничений EVM, технически невозможно поддерживать актуальным вес голосов, отданных за арбитраторов, пересчитывая всех при каждом голосе. Для решения этой проблемы введен метод, вполняя который, пересчитать голоса и изменить позицию арбитратора в топе может любой адрес без авторизации. Кто замотивирован выполнять эти действия:
* конкуренты, если текущий вес голоса в контракте голосования выше реального
* сам арбитратор, иначе оне не сможет получить вознаграждение

## Общие Утверждения

* Кол-во `uint256` топ-кандидатов для пуша в мультисиг управляется ролью GALT_SPACE
* В любой момент любой адрес может выполнить метод, который пушит текущий топ-список валидаторов из контракта голосования в сам мультисиг
* Голосовать имеют право либо владельцы SPACE токенов либо Оракулы.
* 100% голосов состоит из
    * 50% - равны 100% голосам всех участков Space токенов
    * 50% - равны 100% голосам держателей всех стейков
* Веса голосов
    * Вес голоса адреса-владельца SPACE токена определяется площадью всех заложенных им участком на конкретном мультисиге
    * Вес голоса оракула определяется размером заложенного им стейком. Если баланс стейка в минусе - это так же учитываются (суммируется).
    * Если адрес является и оракулом и владельцем SPACE токена, он может (но не принуждается) использовать обе роли при голосовании.

## Источники данных
### Голосование Space owner
* Владельцы SPACE токенов для голосования блокируют свой SPACE токен к конкретному мультисигу.
    * Возможность передачи токена блокируется
    * Чтобы передать SPACE токен, необходимо сначала его разблокировать.
    * Разные SPACE токены можно лочить на разные мультисиги даже если у них один владелец
* Текущий вес голоса на момент голосования рассчитывается как (owner stake at given multisig / total multisig stakes).
* Total multisig stakes суммирует только те участки, владельцы которых явно сделали стейк на этот мультисиг. Участки, у которых не назначены мультисиги не учитываются.

Пример набора контрактов:

````solidity
pragma solidity ^0.4.18;

interface Accounting {
    function balanceOf(address _for) public returns (uint256);
    function totalSupply() public returns (uint256);
}

contract SpaceReputationAccounting is Accounting {
    uint256 totalSpace;
    uint256 totalStakedSpace;

    // SpaceOwner => totalStakedSpace
    mapping(address => uint256) ownerStakedSpace;
    // SpaceOwner => (multisig => space)
    mapping(address => mapping(address => uint256)) ownerTotalStakedSpacePerSpaceToken;

    function balanceOf(address _for) public returns (uint256);
    function totalSupply() public returns (uint256);
}

contract OraclesStakesAccounting is Accounting {
}


contract ArbitratorVoting {
    modifier onlySpaceHolder() {
        _;
    }

    modifier onlyOracle() {
        _;
    }

    SpaceReputationAccounting sra;
    OraclesStakesAccounting osa;

    address arbitratorsMultiSig;
    uint256 public limit = 50;

    struct Candidate {
        address current;
        address next;
        address prev;
        uint256 weight;
    }
    
    mapping(address => Candidate) candidates;

    // candidate from Top-N with the highest weight
    address firstCandidate;
    // candidate from Top-N with the lower weight
    address lastCandidate;

    // space owner => candidate
    mapping(address => address) spaceOwnerVotesFor;
    
    // oracle => candidate
    mapping(address => address) oracleVotesFor;

    // candidate => space
    mapping(address => uint256) candidateTotalSpace;
    
    // candidate => stake
    mapping(address => uint256) candidateTotalStake;

    address[50] pool;

    function voteAsSpaceOwner(address _for) external onlySpaceHolder {
        uint256 weight = sra.balanceOf(msg.sender);
        spaceOwnerVotesFor[msg.sender] = _for;
        candidateTotalSpace[_for] = candidateTotalSpace[_for] + weight;
    }

    function voteAsOracle(address _for) external onlyOracle {
        uint256 weight = osa.balanceOf(msg.sender);
        spaceOwnerVotesFor[msg.sender] = _for;
        candidateTotalStake[_for] = candidateTotalStake[_for] + weight;
    }

    function recalculateCandidateVotes(address _candidate) external {
        // recalcualte space weight
        uint256 totalSpace = sra.totalSupply();
        uint256 candidateSpaceWeight = candidateTotalSpace[_candidate] * 100 / totalSpace;

        // recalcualte stakes weight
        uint256 totalStake = osa.totalSupply();
        uint256 candidateStakesWeight = candidateTotalStake[_candidate] * 100 / totalStake;
        
        // save the sum
        uint256 weight = candidateSpaceWeight + candidateStakesWeight;
        candidates[_candidate].weight = weight;
        
        // existing element
        if (candidates[_candidate].active) {
            address currentWeight = candidates[_candidate].current;

            // walk up
            if (weight > candidates[_candidate].weight) {
                while (weight > candidates[current].weight) {
                    current = candidates[current].prev;
                }
                // insert and re-link elements
                // remove the last
            // walk down
            } else {
                while (weight < candidates[current].weight) {
                    current = candidates[current].next;
                }
                // insert and re-link elements
                // remove the last
            }
        //new element
        } else {
            // try push to the top
            if (weight > candidates[firstCandidate].weight) {
                // insert to the top
                // remove the last
            } else if (weight > candidates[lastCandidate].weight) {
                address current = candidates[lastCandidate].current;
    
                while (weight > candidates[current].weight) {
                    current = candidates[current].prev;
                }
    
                // insert and re-link elements
                // remove the last
            } else {
                // do nothing
            }
        }
    }
}

````


## Интеграция с существующими контрактами
### SpaceToken
`SpaceToken` перед выполнением нижеперечисленных действий вызывает SpaceReputationAccounting, который выполняет внутренние проверки в своем реестре и, при необходимости, вызывает отмену транзакции (в случае, если токен застейкан). Список действий 721 токена:
* setApprovalForAll()
* approve()
* transferFrom()
* safeTransferFrom()
* burn()

![alt text](https://docs.google.com/drawings/d/e/2PACX-1vTHs-0ZSvvgisoPGW1V434Y2JwptSRCx2TqxWG6VOrvYOQJwJz2nBZIyflnUyPmVFxZDPKLJDTiV0pE/pub?w=960&h=720)



## Обсуждение 3 Декабря
* Контракты учета владельцев space токенов и ораклов разделяются на 2 составляющие:
   * минт репутации - для каждой сущности реализуется свое решение, наследующее абстрактаный класс
   * передача и учет репутации - реализуется в абстрактном классе
* После минта репутации, ее можно передать неограниченное кол-во раз в любом количестве, не превышающем баланс
* Владелец репутации в любой момент может отозвать переданную репутацию
* Если репутация была передана адресу и была переназначена другому, ее отозвать и перераспределить нельзя
* Передать репутацию можно только адресу, который владеет минимум одним 721 токеном

![](../../images/IMG_20181203_153430.jpg)

## Questions

* Все ли готовы голосовать публично?

