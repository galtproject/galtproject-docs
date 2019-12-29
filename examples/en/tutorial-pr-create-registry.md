<!--- 
 * Copyright ©️ 2018 Galt•Core Blockchain Company
  Nikolai Popeka [Basic Agreement](ipfs/QmaCiXUmSrP16Gz8Jdzq6AJESY1EAANmmwha15uR3c1bsS).
  
  URL: https://app.galtproject.io/#/mainnet/ppr-registry/all
  
--->

# Create Private Property Registry

More information on Private property registries you can find in [corresponding section in our Whitepaper](https://github.com/galtproject/galtproject-docs/blob/master/en/Whitepaper.md#creating-property-records-disputes-resolution-and-use-cases-in-private-property-registries). 

![tutorial-pr-create-registry](https://github.com/galtproject/galtproject-docs/blob/master/examples/en/images/tutorial-pr-create-registry.png)

- **Token name** - name of the token according to ERC721 standart.
- **Token symbol** - token symbol according to ERC721 standart.
- **Default burn timeout for lost tokens** - The token holder's private key may be lost. In this case, the Owner of the registry, can create a new token. Registry Owner can also initiate the destruction of the old token after a specified time. The Owner of the token can always change this parameter, as well as cancel the destruction of the token.
- **Unit** - minutes, hours or days.
- **Property Locker Fee** - Each token holder must lock it in smart contract in order to join one or several Communities of homeowners. For each such operation, he will pay you commission.
- **Property Market Fee** - The protocol contains smart contracts for the purchase and sale of Property tokens. The owner of the token can create a sales order, receive offers and carry out transactions in smart contracts. Each time one creates such an order, the Token Holder will pay you commission.
- **Controller Proposal Fee** - Property token Owner can create proposals to change geographic coordinates and other data or burn his tokens. This proposal needs to be approved by you or other address assigned by you. For each such operation, he will pay you commission.
