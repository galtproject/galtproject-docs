# Harvest Management - Concept
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

A blockchain one need to use your own on the basis of Ether. One can use 7-8 nodes that will validate transactions and ensure the reliability of all the data being written. Performance 1000 transactions per second. Node software - https://www.parity.io/.

For Smart Equipment Aira Lab Protocol can bu used: https://aira.life/en/.

## User story

### Scenario # 1 Accounting for wine production.
1. The user - the crop collector collects the grapes in Cinqua Terra. The user has his unique address 0x4FDE31E09266423d5f1B8bf16dC8DeF085C197E5, and a private key to which he can sign transactions.

2. There is a token of the standard ERC721, which corresponds to the plot with the vineyard. This site is addressed to the geocache [spyfvqwnd] (https://explorer.galtproject.io/map/#spyfvqwnd). The plot size is 4.77 x 4.77 meters. Also, the site can have any random shape or size.

3. The user - crop collector 0x4FDE31E09266423d5f1B8bf16dC8DeF085C197E5 collected 30 kg of grapes from the plot. The user puts the box on the Smart Scales. Enter the site id and its address, create a transaction for the packaging of grapes and sign the transaction with its private key. The scales also have their address 0x4FED1fC4144c223aE3C1553be203cDFcbD38C581 and the private key. The scales weigh the grapes, create and sign a transaction based on the weighing results. The scales print the label with the bar code 1E09266423d5f1B8b.

There is a recording of data in the blockroom. In fact, it is written that Employee 0x4FDE31E09266423d5f1B8bf16dC8DeF085C197E5 collected and packed 30 kg of grapes:

| id of the site | Packer ID | Number | Employee / Robot |
| ---------- | ---------- | ---------- | ---------- |
| spyfvqwnd | 1E09266423d5f1B8b | 30 | 0x4FDE31E09266423d5f1B8bf16dC8DeF085C197E5 |

These data can not be faked and changed.

4. The balance prints a label with the bar code 1E09266423d5f1B8b. and the collector pastes it on the box.
