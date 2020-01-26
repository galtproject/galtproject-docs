<!--- 
 * Copyright ©️ 2018 Galt•Core Blockchain Company
  Nikolai Popeka [Basic Agreement](ipfs/QmaCiXUmSrP16Gz8Jdzq6AJESY1EAANmmwha15uR3c1bsS).
  
  URL: https://app.galtproject.io/#/mainnet/ppr-registry/all
  
--->

# Create Private Property Registry
Use  modal window to create your Private property Registry.

More information on Private property registries you can find in [corresponding section in our Whitepaper](https://github.com/galtproject/galtproject-docs/blob/master/en/Whitepaper.md#creating-property-records-disputes-resolution-and-use-cases-in-private-property-registries). 

In the upper part of the window, you can see Factory contract address. This Factory will create your Private property Registry.
![tutorial-pr-create-registry](https://raw.githubusercontent.com/galtproject/galtproject-docs/master/tutorials/en/images/tutorial-pr-create-registry.png)
Fill in the fields required to create Private Registry contracts:
- **Token name** - name of the token according to ERC721 standart. E.g. "Malibu Property registry".
- **Token symbol** - token symbol according to ERC721 standart. E.g. "MAL".
- **Default burn timeout for lost tokens** - The Token Owner's private key may be lost. In this case, the Registry Owner, can create a new token. Registry Owner can also initiate the destruction of the old token after a specified preiod of time. The Token Owner can always change this parameter, as well as cancel the destruction of the token. E.g. "28".
- **Unit** - minutes, hours or days. E.g. "days".
- **Property Locker Fee** - Each Token Owner must lock it in smart contract in order to join one or several Communities of Property Owners. For each such operation, he will pay commission to Private Registry.
- **Property Market Fee** - The protocol contains smart contracts for the purchase and sale of Property tokens. The owner of the token can create a sales order, receive offers and sell tokens. Each time Token Owner creates a sale order, the Token Owner will pay commission to Private Registry.
- **Controller Proposal Fee** - Property token Owner can create proposals to change geographic coordinates and other data or burn his tokens. This proposal needs to be approved by Private Registry owner or other address assigned by him. For each such operation, he will pay commission to Private Registry.

Push "Next step" button.

![tutorial-pr-create-registry](https://raw.githubusercontent.com/galtproject/galtproject-docs/master/tutorials/en/images/tutorial-pr-create-registry-2.png)
On the second screen, enter the text of the agreement with the Token Owners. If you want to use the default agreement press "Set default", scroll down and fill in the "Meaning and purpose of property token" section. The legal agreement should clearly determine the meaning and purpose of the token, as well as all the nuances of the interaction between the registry owner and the token owners.
![tutorial-pr-create-registry](https://raw.githubusercontent.com/galtproject/galtproject-docs/master/tutorials/en/images/tutorial-pr-create-registry-3.png)
You need to pay a small commission to support the project. Check checkbox and push "Create registry" button. Metamask will ask to confirm and send the transaction. Click the "Confirm" button and wait for the transaction to be confirmed. 
![tutorial-pr-create-registry](https://raw.githubusercontent.com/galtproject/galtproject-docs/master/tutorials/en/images/tutorial-pr-create-registry-4.png)
After the transaction is confirmed, you need to log in to GeeSome. GeeSome is a protocol for social networks, chats and file storages based on IPFS. You will need it, since not all data on Property tokens is stored in the blockchain. Additional features and media files are stored in IPFS. 
You can run your Geesome node or use our hosting. On our own hosting we offer free upload up to 100 megabytes per month. You can also buy additional space.
![tutorial-pr-create-registry](https://raw.githubusercontent.com/galtproject/galtproject-docs/master/tutorials/en/images/tutorial-pr-create-registry-5.png)
After clicking the "Authorize in Geesome" button, Metamask will start and ask you to sign the message.
![tutorial-pr-create-registry](https://raw.githubusercontent.com/galtproject/galtproject-docs/master/tutorials/en/images/tutorial-pr-create-registry-6.png)
Push "Go to Registry page" and mint your first Property token!



