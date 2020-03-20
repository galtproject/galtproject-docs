## How the grant permissions works
ACL create a permissions granting **entity** the ability to perform actions, setting **manager** as the permission's manager.

## Permissions
**entity**: Address of the whitelisted entity that will be able to perform the role

**manager**: Address of the entity that will be able to grant and revoke the permission further.

## Presale
|Role|manager|entity|Description|
|---|---|---|---|
|presale.OPEN_ROLE|shareVoting|controller|Run presale|
|presale.CONTRIBUTE_ROLE|shareVoting|controller, anyone|Buy tokens on presale|
|controller.OPEN_PRESALE_ROLE|shareVoting|controller||

## Fundraising for User
|Role|manager|entity|Description|
|---|---|---|---|
|marketMaker.OPEN_BUY_ORDER_ROLE|shareVoting|controller,anyone||
|marketMaker.OPEN_SELL_ORDER_ROLE|shareVoting|controller,anyone||

## Fundraising tapped balance: control, widthdraw
|Role|manager|entity|Description|
|---|---|---|---|
|tap.UPDATE_BENEFICIARY_ROLE|shareVoting|shareVoting||
|tap.UPDATE_MAXIMUM_TAP_RATE_INCREASE_PCT_ROLE|shareVoting|shareVoting||
|tap.UPDATE_MAXIMUM_TAP_FLOOR_DECREASE_PCT_ROLE|shareVoting|shareVoting||
|tap.ADD_TAPPED_TOKEN_ROLE|shareVoting|controller||
|tap.UPDATE_TAPPED_TOKEN_ROLE|shareVoting|controller||
|tap.RESET_TAPPED_TOKEN_ROLE|shareVoting|controller||
|tap.WITHDRAW_ROLE|shareVoting|controller,anyone|Withdraw funds to beneficiar|
|controller.UPDATE_MAXIMUM_TAP_RATE_INCREASE_PCT_ROLE|shareVoting|controller||
|controller.UPDATE_MAXIMUM_TAP_FLOOR_DECREASE_PCT_ROLE|shareVoting|controller||
|controller.ADD_TOKEN_TAP_ROLE|shareVoting|shareVoting||
|controller.UPDATE_TOKEN_TAP_ROLE|shareVoting|shareVoting||

## Market Fees
|Role|manager|entity|Description|
|---|---|---|---|
|marketMaker.UPDATE_BENEFICIARY_ROLE|shareVoting|controller||
|marketMaker.UPDATE_FEES_ROLE|shareVoting|controller||
|controller.UPDATE_BENEFICIARY_ROLE|shareVoting|shareVoting||
|controller.UPDATE_FEES_ROLE|shareVoting|shareVoting||

## Market tokens control
|Role|manager|entity|Description|
|---|---|---|---|
|marketMaker.ADD_COLLATERAL_TOKEN_ROLE|shareVoting|controller||
|marketMaker.REMOVE_COLLATERAL_TOKEN_ROLE|shareVoting|controller||
|marketMaker.UPDATE_COLLATERAL_TOKEN_ROLE|shareVoting|controller||
|controller.REMOVE_COLLATERAL_TOKEN_ROLE|shareVoting|shareVoting||
|controller.UPDATE_COLLATERAL_TOKEN_ROLE|shareVoting|shareVoting||

## Market other
|Role|manager|entity|Description|
|---|---|---|---|
|marketMaker.OPEN_ROLE|shareVoting|controller|Run fundraising|
|controller.OPEN_TRADING_ROLE|shareVoting|presale||

## BOARD token
|Role|manager|entity|Description|
|---|---|---|---|
|boardTM.MINT_ROLE|shareVoting|boardVoting||
|boardTM.BURN_ROLE|shareVoting|boardVoting||

## SHARE token
|Role|manager|entity|Description|
|---|---|---|---|
|shareTM.MINT_ROLE|noone|marketMaker||
|shareTM.ISSUE_ROLE|shareVoting|presale||
|shareTM.ASSIGN_ROLE|shareVoting|presale||
|shareTM.REVOKE_VESTINGS_ROLE|shareVoting|presale||
|shareTM.BURN_ROLE|noone|marketMaker,presale||

## Finance
|Role|manager|entity|Description|
|---|---|---|---|
|vault.TRANSFER_ROLE|shareVoting|finance||
|finance.EXECUTE_PAYMENTS_ROLE|shareVoting|boardVoting||
|finance.MANAGE_PAYMENTS_ROLE|shareVoting|boardVoting||
|finance.CREATE_PAYMENTS_ROLE|shareVoting|boardVoting||

## SHARE voting
|Role|manager|entity|Description|
|---|---|---|---|
|shareVoting.MODIFY_QUORUM_ROLE|shareVoting|shareVoting||
|shareVoting.MODIFY_SUPPORT_ROLE|`shareVoting => noone`|`shareVoting => noone`||
|shareVoting.CREATE_VOTES_ROLE|shareVoting|boardTM||

## BOARD voting
|Role|manager|entity|Description|
|---|---|---|---|
|boardVoting.MODIFY_QUORUM_ROLE|shareVoting|boardVoting||
|boardVoting.MODIFY_SUPPORT_ROLE|shareVoting|boardVoting||
|boardVoting.CREATE_VOTES_ROLE|shareVoting|boardTM||

## DAO managment
|Role|manager|entity|Description|
|---|---|---|---|
|**registry.REGISTRY_MANAGER_ROLE**|shareVoting|shareVoting||
|**registry.REGISTRY_ADD_EXECUTOR_ROLE**|shareVoting|shareVoting||
|**dao.APP_MANAGER_ROLE**|shareVoting|shareVoting||
|**acl.CREATE_PERMISSIONS_ROLE**|shareVoting|shareVoting||

## Other
|Role|manager|entity|Description|
|---|---|---|---|
|reserve.SAFE_EXECUTE_ROLE|shareVoting|shareVoting|???|
|reserve.ADD_PROTECTED_TOKEN_ROLE|shareVoting|controller|???|
|reserve.TRANSFER_ROLE|shareVoting|tap,marketMaker|???|

