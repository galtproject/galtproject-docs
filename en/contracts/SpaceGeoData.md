# SpaceGeoData smart contract

## Simple Summary

Smart contract for the storage of geographical and other identification data for land and real estate tokens in the Galt Project.
## Motivation
## Token types
There are three token types: 
- Land plot - represent particular land plot with unique geographical coordinates. Each token stores information about the boundaries of the land plot in smart contract in the form of coordinates of the vertices of the plot. 
- Whole buildings - represents a whole detached building.
- Room in building/Apartment - represents a separate room or several rooms in the building (apartment, office, retail space, etc.).
## Token identification data
Land plots and real estate must have unique identification data in order to ensure the impossibility of double ownership of the same property.
### Land plot
- coordinates of vertices of land in lat/lon, UTM and geohash and height above sea level in meters;
- address;
### Whole building
- coordinates of the building in the form of coordinates of the vertices of the polygon of the foundation of the building in lat/lon, UTM, geohash and height above sea level in meters;
- address of the building;
### Room/Apartment
- coordinates of the building in the form of coordinates of the vertices of the polygon of the foundation of the building in lat/lon, UTM, geohash and height above sea level in meters where the room is located;
- the zero point index of the local coordinate system of the building;
- coordinates of each point of the room perimeter in meters in the local coordinate system;
- alphanumeric designation of the floor of the building where the room is located;
- floor height in meters from ground level;
- alphanumeric designation of the room/apartment;
- address;
### Room
## Specification
## Rationale
## Test Cases and Reference Implementation
## Copyright
Copyright ©️ 2018 Galt•Space Society Construction and Terraforming Company(Founded by [Nikolai Popeka](https://github.com/npopeka),
[Dima Starodubcev](https://github.com/xhipster),
[Valery Litvin](https://github.com/litvintech) by
[Basic Agreement](http://cyb.ai/QmSAWEG5u5aSsUyMNYuX2A2Eaz4kEuoYWUkVBRdmu9qmct:ipfs)).

Copyright ©️ 2018 Galt•Core Blockchain Company
(Founded by [Nikolai Popeka](https://github.com/npopeka) and
Galt•Space Society Construction and Terraforming Company by
[Basic Agreement](http://cyb.ai/QmaCiXUmSrP16Gz8Jdzq6AJESY1EAANmmwha15uR3c1bsS:ipfs)).