# Oracles.sol contract

## Simple summary

Oracles is a well-known pattern in the blockchain sphere for feeding real-world data into blockchain registries.
In our system, oracles validate users inputs and guarantees the inputs correctness by their deposited stakes.

## Rationale

Oracles contract manages the following entities:

* Application type - corresponds to a specific application contract and groups `oracle types` participating in the application validation process.
* Oracle type - permission to take part in one or multiple verification steps of a specific application along with other `oracles` with the same role.
* Oracle - a unique ethereum address which could have one or multiple `oracle types`.

Furthermore Oracles contract provides external condition check methods.

### Applications Type

Galt Project has multiple application contract which serves as input interface for untrusted information. Each of this application contract has an associated `application type` record in `Oracles` contract. The two major purposes of this record is:
* Defining which roles could take part in this application verification
* Share of each role in the validators share of the total fee paid by an applicant.

The only exception is `ClaimManager` contract where the role of oracles granted to Arbitrators.

### Oracle Roles

An abstract application contract has at least one step where at least one oracle should prove that he is agree with the given action. Number of such steps depends on contract logic. Number of oracles to validate a specific step could be defined either by a contract logic (hardcoded) or by a managing contract role. Application contracts could have different names for such managing contract roles.

There is a restriction with `oracle types` and `application type` relation. Each `oracle role` could be associated with only one `application type`. And in another words, each `application type` could have multiple `oracle roles`.

### Oracle

Oracle is an address of organization or person who validates off-chain input data and signs his decisions. Oracle could have multiple roles.

For security reasons, it is recommended to use a MultiSig contract as an oracle address.

#### Oracle CRUD
* Create - To become an oracle, user should apply through `NewOracleManager` contract. In this contract, instead of oracles themself, the role of verifier is granted to `Auditors`. They have to verify whether or not the given address could act as an oracle with the roles specified in the application.
* Read - All oracle data is publicly available using corresponding getters.
* Update - To update an oracle information or/and role assigned to him, the similar `UpdateOracleManager` application contract is used.
* Delete - To temporarily or permanently disable an oracle, anyone could submit a new claim to `ClaimManager` and disable the oracle by slashing his stake.

#### Oracle Stakes
Having assigned roles is not enough to start working as an oracle and perform applications validations. Another important part of being an active oracle is keeping your stake deposit above required threshold.

#### Oracle Permissions
In most cases to participate in an application validation process an address has to satisfy the 3 following conditions:
* Address should be present in the Oracles registry
* A role of performing action should be assigned
* A deposit for this role should be above the threshold

# Specification
## Inheritance
* `Permissioned` - for role management
## Utils
no utils
## Limits
* Maximum 50 `Oracle Type` per `Application Type`
## Contract roles
| Role | Initial Owner | Planned Owner | Description
|------| ---- | ---- | ---
| `application_type_manager` | GaltSpace MultiSig | GaltSpace MultiSig | addresses allowed defining application type roles
| `oracles_type_manager` | GaltSpace MultiSig | GaltSpace MultiSig | addresses allowed defining shares for roles in applications_type
| `oracles_manager` | `NewOracleManager` and `UpdateOracleManager` | `NewOracleManager` and `UpdateOracleManager` | addresses allowed `create` & `update` actions on oracle profiles including `CRUD` actions on assigned roles
| `galt_share_manager` | GaltSpace MultiSig | GaltSpace MultiSig | address allowed defining Galt Project share in total fees paid by applicants
| `oracle_stake_manager` | GaltSpace MultiSig | GaltSpace MultiSig | address allowed defining stake values for `oracle_types` 
| `oracle_stakes_notifier` | `OracleStakesAccounting` | `OracleStakesAccounting` | address allowed trigger notification callback about changed oracle stake

## Information sources
No sources required for the contract functionality.

## Implementation

````solidity
interface Oracles is Permissioned {

    string public constant ROLE_APPLICATION_TYPE_MANAGER = "application_type_manager";
    string public constant ROLE_ORACLE_TYPE_MANAGER= "oracle_type_manager";
    string public constant ROLE_ORACLE_MANAGER = "oracle_manager";

    string public constant ROLE_GALT_SHARE_MANAGER = "galt_share_manager";
    string public constant ROLE_VALIDATOR_STAKES_MANAGER = "oracle_stakes_manager";
    string public constant ROLE_VALIDATOR_STAKES_NOTIFIER = "oracle_stakes_notifier";


    // ApplicationType management (define including roles and their shares)
    // Oracle Roles management (define bound application type and required stake)
    function addOracleType(bytes32 _role)
        external onlyRole();

    // Oracles management (crud)
    function addOracle(address _account, bytes32[] _roles)
        external onlyRole(ROLE_ORACLE_MANAGER);

    function updateOracle(address _account, bytes32[] _roles)
        external onlyRole(ROLE_ORACLE_MANAGER);
}
````


# Further improvements
Migrate to solidity 0.5.0
Upgrade role management to OpenZeppelin v2.0.0 Roles

# Initial setup
## Dependent contract roles
* `GaltToken`
## Upgradeability
No Upgradeability planned
## Actions on broken or stolen contract
Deploy a new contract with fixed bug and make proxy point to it.
Recover all settings either manually or using script
