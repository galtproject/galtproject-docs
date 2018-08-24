# Harvest Management - Concept
## Description of the problem
It is necessary to create an accounting system for agricultural products that would allow for the unique identification of the packaging of the final product, for example wine, to trace the entire path from a particular land plot to the bottle on Ethereum blockchain or private blockchain.

## Goals of the contract
- for each land plot, determined by geohash or boundaries equations to take into account the harvest in kilograms or pieces;
- make sure that data can not be faked;
- make it possible to control and account for the loss of products all the way from harvesting to shelf;

## General Provisions
In the system for the main accounting unit, take a piece of land. Each plot of land is adresses by geohash or several geohash. For each land plot Ethereum ERC721 token is issued. 

An example of land plot adressed by 630 geohash <img width="800" alt="screen shot 2018-08-24 at 12 16 55" src="https://user-images.githubusercontent.com/29427584/44579726-9fefe700-a797-11e8-916f-58176d793a74.png">

Each piece of land of a certain size will create a crop that will be counted in kilograms or pieces or any accounting unit. Each crop from each plot will be counted as a unique batch of products.

A blockchain one need to use your own on the basis of Ether. One can use 7-8 nodes that will validate transactions and ensure the reliability of all the data being written. Performance 1000 transactions per second. Node software - https://www.parity.io/.

