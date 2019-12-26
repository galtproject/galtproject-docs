---
id: ppr-governance-contract
title: Private property registry governance contract
sidebar_label: Private property registry governance contract
---

# Contract description
The contract is designed to manage one Private Property Registry and can be established initially when the registry is created or later for the purpose of decentralization. 
By default, the private registry is managed by its owner, assigning roles that carry out operations to issue tokens and change data on them.  The described contracts allow to manage the Private property registry using tokens of land and real estate. Thus, the registry becomes decentralized.

# General architecture
![General architecture](https://github.com/galtproject/galtproject-docs/blob/master/docs/applications/images/ppr-governance-contract-01.png)

# Requirements
- the contract is created upon deployment together with the registry or separately;
- the contract fully fulfills all the roles in the ERC721 and controller contracts;
- the contract caches the token area data block;
- the contract is used to manage only one private registry;
- data on voting parameters (support, minimum approval, duration) is stored in the config;
