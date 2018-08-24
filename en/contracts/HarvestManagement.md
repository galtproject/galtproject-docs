[comment]: Copyright © 2018 Galt•Space Society Construction and Terraforming Company 
([Nikolai Popeka](https://github.com/npopeka),
[Dima Starodubcev](https://github.com/xhipster), 
[Valery Litvin](https://github.com/litvintech) with 
[Basic Agreement](http://cyb.ai/QmSAWEG5u5aSsUyMNYuX2A2Eaz4kEuoYWUkVBRdmu9qmct:ipfs)).

# Harvest Management Smart Contract - Proof of Concept
## Description of the problem
It is necessary to create an accounting system for agricultural products that would allow for the unique identification of the packaging of the final product, for example wine, to trace the entire path from a particular land plot to the bottle on Ethereum blockchain or private blockchain.

## Goals of the contract
- for each land plot, determined by geohash or boundaries equations to take into account the harvest in kilograms or pieces;
- make sure that data can not be faked;
- make it possible to control and account for the loss of products all the way from harvesting to shelf;

## General
In the system for the main accounting unit, take a piece of land. Each plot of land is adresses by geohash or several geohash. For each land plot Ethereum ERC721 token is issued. 

An example of land plot adressed by 630 geohash <img width="800" alt="screen shot 2018-08-24 at 12 16 55" src="https://user-images.githubusercontent.com/29427584/44579726-9fefe700-a797-11e8-916f-58176d793a74.png">

Land Accounting Blockchain protocol is provided by https://galtproject.io/.

Each piece of land of a certain size will create a crop that will be counted in kilograms or pieces or any accounting unit. Each crop from each plot will be counted as a unique batch of products.

One need to use his own blockchain on the basis of Ethereum. One can use 7-8 nodes that will validate transactions and ensure the reliability of all the data being written. Performance 1000 transactions per second. Node software - https://www.parity.io/. Nodes can be distributed between independent product manufacturers.

For Smart Equipment Aira Lab Protocol can bu used: https://aira.life/en/. 

## User story

### Scenario # 1 Accounting for wine production.
1. The user - the crop collector collects the grapes in Cinqua Terra. The user has his unique address 0x4FDE31E09266423d5f1B8bf16dC8DeF085C197E5, and a private key to which he can sign transactions.

2. There is a token of the standard ERC721, which corresponds to the plot with the vineyard. This site is addressed to the geohash [spyfvqwnd](https://explorer.galtproject.io/map/#spyfvqwnd). The plot size is 4.77 x 4.77 meters. Also, the site can have any random shape or size.

3. The user - crop collector 0x4FDE31E09266423d5f1B8bf16dC8DeF085C197E5 collected 30 kg of grapes from the plot. The user puts the box on the Smart Scales. Enter the plot ID and its address, create a transaction for the packaging of grapes and sign the transaction with its private key. The scales also have their address 0x4FED1fC4144c223aE3C1553be203cDFcbD38C581 and the private key. The scales weigh the grapes, create and sign a transaction based on the weighing results. The scales print the label with the bar code 1E09266423d5f1B8b.

Transactions record data in blockchain. In fact, it is written that Employee 0x4FDE31E09266423d5f1B8bf16dC8DeF085C197E5 collected and packed 30 kg of grapes:

| id of the plot | Packer ID | Number | Employee / Robot |
| ---------- | ---------- | ---------- | ---------- |
|[spyfvqwnd](https://explorer.galtproject.io/map/#spyfvqwnd) | 1E09266423d5f1B8b | 30 | 0x4FDE31E09266423d5f1B8bf16dC8DeF085C197E5 |

These data can not be faked and changed.

4. Scales prints a label with the bar code 1E09266423d5f1B8b. and the collector pastes it on the box.

5. The user passes the box to the driver. When the box is transferred, the collector specifies the driver address 0xf3101865bd9dbe720464e684247a13269cca70660xf, specifies the box identifier, creates and signs the transaction for the transfer of the box. The driver also creates and signs a transaction to receive the box.

In the blockchain, the following data changes occur:

| id of the plot | Packer ID | Number | Employee / Robot |
|----------|----------|----------|----------|
|[spyfvqwnd](https://explorer.galtproject.io/map/#spyfvqwnd)|1E09266423d5f1B8b|0|0x4FDE31E09266423d5f1B8bf16dC8DeF085C197E5|
|[spyfvqwnd](https://explorer.galtproject.io/map/#spyfvqwnd)|1E09266423d5f1B8b|30|0xf3101865bd9dbe720464e684247a13269cca70660xf|

In fact, 30 kg of grapes passed from the Collector to the Driver.

6. The driver delivered a box of grapes to an automatic squeezing station. The driver opens the box and pours the grapes into the Smart Press tank. The driver specifies the barcode of the package, the address of the press, creates a transaction for the transfer of the box, signs it. Smart press with the address 0x4fde31e09266423d5f1b8bf16dc8def085c197e5 weigh the box. Automatic scales create and sign with their private key a transaction for changing data:

| id of the plot | Packer ID | Number | Employee / Robot |
| ---------- | ---------- | ---------- | ---------- |
| [spyfvqwnd](https://explorer.galtproject.io/map/#spyfvqwnd) | 1E09266423d5f1B8b | 0 | 0xf3101865bd9dbe720464e684247a13269cca70660xf |
| [spyfvqwnd](https://explorer.galtproject.io/map/#spyfvqwnd)| 1E09266423d5f1B8b | 30 | 0x4fde31e09266423d5f1b8bf16dc8def085c197e5 |

In fact, 30 kg of grapes were transferred from the Driver to the Automatic press.

7. From the weighing tank, the grapes enter the spin tank with identifier 5f1b8bf16dc8d. Smart press creates and signs a transaction and the following changes occur.

| id of the plot | Packer ID | Number | Employee / Robot |
| ---------- | ---------- | ---------- | ---------- |
| [spyfvqwnd](https://explorer.galtproject.io/map/#spyfvqwnd) | 1E09266423d5f1B8b | 0 | 0x4fde31e09266423d5f1b8bf16dc8def085c197e5 |
| [spyfvqwnd](https://explorer.galtproject.io/map/#spyfvqwnd) | 5f1b8bf16dc8d | 30 | 0x4fde31e09266423d5f1b8bf16dc8def085c197e5 |

In fact, 30 kg of grapes from the box were moved to the tank for spinning.

8. At the same time, in the reservoir, in the end, there is 100 kg of grapes from three sites and in the detachment we see the following:

| id of the plot | Packer ID | Number | Employee / Robot |
| ---------- | ---------- | ---------- | ---------- |
| [spyfvqwnd](https://explorer.galtproject.io/map/#spyfvqwnd)| 5f1b8bf16dc8d | 30 | 0x4fde31e09266423d5f1b8bf16dc8def085c197e5 |
| [spyfvqwn6](https://explorer.galtproject.io/map/#spyfvqwn6) | 5f1b8bf16dc8d | 30 | 0x4fde31e09266423d5f1b8bf16dc8def085c197e5 |
| [spyfvqwng](https://explorer.galtproject.io/map/#spyfvqwng) | 5f1b8bf16dc8d | 40 | 0x4fde31e09266423d5f1b8bf16dc8def085c197e5 |

9. The smart press produced a spin and received 100 liters of grape juice. Smart press creates a transaction to move 100 liters of juice and signs it. Through the pipes, the juice enters the fermentation tank. The cistern has the identifier 1f7b8bs1ddcld. A smart fluid volume sensor with the address 0x640bF693d3c06599300c1E2Be38c7F4AbCc597a1 signs the transaction and the following changes occur:

| id of the plot | Packer ID | Number | Employee / Robot |
| ---------- | ---------- | ---------- | ---------- |
|spyfvqwnd|5f1b8bf16dc8d|0|0x4fde31e09266423d5f1b8bf16dc8def085c197e5|
|spyfvqwn6|5f1b8bf16dc8d|0|0x4fde31e09266423d5f1b8bf16dc8def085c197e5|
|spyfvqwng|5f1b8bf16dc8d|0|0x4fde31e09266423d5f1b8bf16dc8def085c197e5|
|spyfvqwnd|1f7b8bs1ddcld|30|0x640bF693d3c06599300c1E2Be38c7F4AbCc597a1|
|spyfvqwn6|1f7b8bs1ddcld|30|0x640bF693d3c06599300c1E2Be38c7F4AbCc597a1|
|spyfvqwng|1f7b8bs1ddcld|40|0x640bF693d3c06599300c1E2Be38c7F4AbCc597a1|

10. In a fermentation tank, a total volume of 684 liters.

| id of the plot | Packer ID | Number | Employee / Robot |
| ---------- | ---------- | ---------- | ---------- |
| spyfvqwnd | 1f7b8bs1ddcld | 30 | 0x640bF693d3c06599300c1E2Be38c7F4AbCc597a1 |
| spyfvqwn6 | 1f7b8bs1ddcld | 30 | 0x640bF693d3c06599300c1E2Be38c7F4AbCc597a1 |
| spyfvqwng | 1f7b8bs1ddcld | 40 | 0x640bF693d3c06599300c1E2Be38c7F4AbCc597a1 |
| all other plots id | 1f7b8bs1ddcld | 584 | 0x640bF693d3c06599300c1E2Be38c7F4AbCc597a1 |

11. After fermentation 684 liters of wine is bottled in 3 barrels. The IDs of the barrels are 1f7b8bs1ddcln, 5f7b8hs1dscld, 2f7bfs1ddcld.

12. Filling is done by the worker manually. The worker has the address 0xb32242B1353638ffE3485ab523b5ed8C0522595B. A smart tank creates a transaction to transfer 684 liters of wine. The worker performs bottling, creates and signs a transaction for the fact that he poured wine into 3 barrels.

| id of the plot | Packer ID | Number | Employee / Robot |
| ---------- | ---------- | ---------- | ---------- |
|spyfvqwnd|1f7b8bs1ddcld|0|0x640bF693d3c06599300c1E2Be38c7F4AbCc597a1|
|spyfvqwn6|1f7b8bs1ddcld|0|0x640bF693d3c06599300c1E2Be38c7F4AbCc597a1|
|spyfvqwng|1f7b8bs1ddcld|0|0x640bF693d3c06599300c1E2Be38c7F4AbCc597a1|
|all other plots id|1f7b8bs1ddcld|0|0x640bF693d3c06599300c1E2Be38c7F4AbCc597a1|
|spyfvqwnd|1f7b8bs1ddcln|10|0xb32242B1353638ffE3485ab523b5ed8C0522595B|
|spyfvqwn6|1f7b8bs1ddcln|10|0xb32242B1353638ffE3485ab523b5ed8C0522595B|
|spyfvqwng|1f7b8bs1ddcln|13.3|0xb32242B1353638ffE3485ab523b5ed8C0522595B|
|all other plots id|1f7b8bs1ddcln|194.7|0xb32242B1353638ffE3485ab523b5ed8C0522595B|
|spyfvqwnd|5f7b8hs1dscld|10|0xb32242B1353638ffE3485ab523b5ed8C0522595B|
|spyfvqwn6|5f7b8hs1dscld|10|0xb32242B1353638ffE3485ab523b5ed8C0522595B|
|spyfvqwng|5f7b8hs1dscld|13.3|0xb32242B1353638ffE3485ab523b5ed8C0522595B|
|all other plots id|5f7b8hs1dscld|194.7|0xb32242B1353638ffE3485ab523b5ed8C0522595B|
|spyfvqwnd|2f7bfs1ddcld|10|0xb32242B1353638ffE3485ab523b5ed8C0522595B|
|spyfvqwn6|2f7bfs1ddcld|10|0xb32242B1353638ffE3485ab523b5ed8C0522595B|
|spyfvqwng|2f7bfs1ddcld|13,3|0xb32242B1353638ffE3485ab523b5ed8C0522595B|
|all other plots id|2f7bfs1ddcld|194.7|0xb32242B1353638ffE3485ab523b5ed8C0522595B|

13. After aging, wine from one barrel is automatically bottled with a volume of 0.75 liters. The worker sets up the barrel 1f7b8bs1ddcln in the filling machine, creates and signs a transaction for the bottling of the wine. Automatically, the machine with the address 0x32Be343B94f860124dC4fEe278FDCBD38C102D88 pours the barrel over the bottles, creates and signs the transaction. Each bottle has a unique identifier. The following changes occur:

| id of the site | Packer ID | Number | Employee / Robot |
| ---------- | ---------- | ---------- | ---------- |
|spyfvqwnd|1f7b8bs1ddcln|0|0xb32242B1353638ffE3485ab523b5ed8C0522595B|
|spyfvqwn6|1f7b8bs1ddcln|0|0xb32242B1353638ffE3485ab523b5ed8C0522595B|
|spyfvqwng|1f7b8bs1ddcln|0|0xb32242B1353638ffE3485ab523b5ed8C0522595B|
|all other plots id|1f7b8bs1ddcln|0|0xb32242B1353638ffE3485ab523b5ed8C0522595B|
|spyfvqwnd|4f7bns1dlclr|0.03|0xb32242B1353638ffE3485ab523b5ed8C0522595B|
|spyfvqwn6|4f7bns1dlclr|0.03|0xb32242B1353638ffE3485ab523b5ed8C0522595B|
|spyfvqwng|4f7bns1dlclr|0.03|0xb32242B1353638ffE3485ab523b5ed8C0522595B|
|all other plots id|4f7bns1dlclr|0.64|0xb32242B1353638ffE3485ab523b5ed8C0522595B|
|all other plots id|all other bottles|227.25|0xb32242B1353638ffE3485ab523b5ed8C0522595B|

14. On the store shelf, any user can enter the application. Indicate the number of the bottle 4f7bns1dlclr and get information that the wine from this bottle is made from the grapes that was grown here:

| Bottle | Section | Number |
| ------ | ------ | --------- |
|1f7b8bs1ddcln|[spyfvqwnd](https://explorer.galtproject.io/map/#spyfvqwnd)|0.03|
|1f7b8bs1ddcln|[spyfvqwn6](https://explorer.galtproject.io/map/#spyfvqwn6)|0.03|
|1f7b8bs1ddcln|[spyfvqwng](https://explorer.galtproject.io/map/#spyfvqwng)|0.03|
|1f7b8bs1ddcln|other plots|0.64|

The reliability of this data will be guaranteed by cryptography.
