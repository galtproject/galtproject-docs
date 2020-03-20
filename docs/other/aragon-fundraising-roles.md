## Presale
|Role|shareVoting|anyone|noone|Description|
|---|---|---|---|---|
|presale.OPEN_ROLE|x|||Run presale|
|presale.CONTRIBUTE_ROLE|x|x||Buy tokens on presale|
|controller.OPEN_PRESALE_ROLE|x||||

## Fundraising for User
|Role|shareVoting|anyone|noone|Description|
|---|---|---|---|---|
|marketMaker.OPEN_BUY_ORDER_ROLE|x|x|||
|marketMaker.OPEN_SELL_ORDER_ROLE|x|x|||

## Fundraising tapped balance: control, widthdraw
|Role|shareVoting|anyone|noone|Description|
|---|---|---|---|---|
|tap.UPDATE_BENEFICIARY_ROLE|x||||
|tap.UPDATE_MAXIMUM_TAP_RATE_INCREASE_PCT_ROLE|x||||
|tap.UPDATE_MAXIMUM_TAP_FLOOR_DECREASE_PCT_ROLE|x||||
|tap.ADD_TAPPED_TOKEN_ROLE|x||||
|tap.UPDATE_TAPPED_TOKEN_ROLE|x||||
|tap.RESET_TAPPED_TOKEN_ROLE|x||||
|tap.WITHDRAW_ROLE|x|x||Withdraw funds to beneficiar|
|controller.UPDATE_MAXIMUM_TAP_RATE_INCREASE_PCT_ROLE|x||||
|controller.UPDATE_MAXIMUM_TAP_FLOOR_DECREASE_PCT_ROLE|x||||
|controller.ADD_TOKEN_TAP_ROLE|x||||
|controller.UPDATE_TOKEN_TAP_ROLE|x||||

## Market Fees
|Role|shareVoting|anyone|noone|Description|
|---|---|---|---|---|
|marketMaker.UPDATE_BENEFICIARY_ROLE|x||||
|marketMaker.UPDATE_FEES_ROLE|x||||
|controller.UPDATE_BENEFICIARY_ROLE|x||||
|controller.UPDATE_FEES_ROLE|x||||

## Market tokens control
|Role|shareVoting|anyone|noone|Description|
|---|---|---|---|---|
|marketMaker.ADD_COLLATERAL_TOKEN_ROLE|x||||
|marketMaker.REMOVE_COLLATERAL_TOKEN_ROLE|x||||
|marketMaker.UPDATE_COLLATERAL_TOKEN_ROLE|x||||
|controller.REMOVE_COLLATERAL_TOKEN_ROLE|x||||
|controller.UPDATE_COLLATERAL_TOKEN_ROLE|x||||

## Market other
|Role|shareVoting|anyone|noone|Description|
|---|---|---|---|---|
|marketMaker.OPEN_ROLE|x|||Run fundraising|
|controller.OPEN_TRADING_ROLE|x||||

## BOARD token
|Role|shareVoting|anyone|noone|Description|
|---|---|---|---|---|
|boardTM.MINT_ROLE|x||||
|boardTM.BURN_ROLE|x||||

## SHARE token
|Role|shareVoting|anyone|noone|Description|
|---|---|---|---|---|
|shareTM.MINT_ROLE|||x||
|shareTM.ISSUE_ROLE|x||||
|shareTM.ASSIGN_ROLE|x||||
|shareTM.REVOKE_VESTINGS_ROLE|x||||
|shareTM.BURN_ROLE|||x||

## Finance
|Role|shareVoting|anyone|noone|Description|
|---|---|---|---|---|
|vault.TRANSFER_ROLE|x||||
|finance.EXECUTE_PAYMENTS_ROLE|x||||
|finance.MANAGE_PAYMENTS_ROLE|x||||
|finance.CREATE_PAYMENTS_ROLE|x||||

## SHARE voting
|Role|shareVoting|anyone|noone|Description|
|---|---|---|---|---|
|shareVoting.MODIFY_QUORUM_ROLE|x||||
|shareVoting.MODIFY_SUPPORT_ROLE|`o`||`x`||
|shareVoting.CREATE_VOTES_ROLE|x||||

## BOARD voting
|Role|shareVoting|anyone|noone|Description|
|---|---|---|---|---|
|boardVoting.MODIFY_QUORUM_ROLE|x||||
|boardVoting.MODIFY_SUPPORT_ROLE|x||||
|boardVoting.CREATE_VOTES_ROLE|x||||

## DAO managment
|Role|shareVoting|anyone|noone|Description|
|---|---|---|---|---|
|**registry.REGISTRY_MANAGER_ROLE**|x||||
|**registry.REGISTRY_ADD_EXECUTOR_ROLE**|x||||
|**dao.APP_MANAGER_ROLE**|x||||
|**acl.CREATE_PERMISSIONS_ROLE**|x||||

## Other
|Role|shareVoting|anyone|noone|Description|
|---|---|---|---|---|
|reserve.SAFE_EXECUTE_ROLE|x|||???|
|reserve.ADD_PROTECTED_TOKEN_ROLE|x|||???|
|reserve.TRANSFER_ROLE|x|||???|

