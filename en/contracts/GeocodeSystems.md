# Geocode Systems Used in Galt Project

* [UTM](#utm)
* [Lat/Long](#latlong)
* [Geohash](#geohash-string)
* [Geohash5](#geohash5-number)
* [Geohash5z](#geohash5z-number)

## UTM

References:
* https://en.wikipedia.org/wiki/Universal_Transverse_Mercator_coordinate_system

## Lat/Long
...

## Geohash (string)

* maximum precision is `12` symbols
* only base32 symbols are used: `0123456789bcdefghjkmnpqrstuvwxyz`

References:

* https://en.wikipedia.org/wiki/Geohash
* https://github.com/galtspace/galtproject-utils-js/commit/15c8d5180669565b6297547d531dd6242a6c1fc4

## Geohash5 (number)

A specific standard for Galt Project.

Each symbol in geohash is encoded into a 5-bit representation of it's position in bytes32 `0123456789bcdefghjkmnpqrstuvwxyz`:

* `a` becomes 10
* `z` becomes 31
* `zzzzzzzzzzzz` becomes 1152921504606846975

References:
* Geohash => Geohash5 JavaScript conversion script https://github.com/galtspace/galtproject-utils-js/blob/master/src/common.js#L27

## Geohash5z (number)

Another specific standard for Galt Project.

* Represents geohash5 + height above the sea level in centimeters.
* The sea level value is signed integer encoded into a geohash with a shift of 24 bytes from the right and takes 8 bytes (int64 solidity type).

Example of encoding for 179.59 meters (`0x00004627` int64) above the sea level and `zzzzzzzzzzzz` geohash: 

```
* Geohash format (string): `zzzzzzzzzzzz`
* Geohash5 format (number): 1152921504606846975
* Geohash5 format (EVM word):  0x0000000000000000000000000000000000000000000000000fffffffffffffff
* Geohash5z format (EVM word): 0x0000000000000000000000000000000000004627000000000fffffffffffffff
* Geohash5z description:       0xReserved........................Height..Geohash5................
```

And a negative example of -8000 centimeters (`0xffffe0c0` int64) encoded along with the same `zzzzzzzzzzzz` geohash:

```
* Geohash5 format (EVM word):  0x0000000000000000000000000000000000000000000000000fffffffffffffff
* Geohash5z format (EVM word): 0x00000000000000000000000000000000ffffe0c0000000000fffffffffffffff
* Geohash5z description:       0xReserved........................Height..Geohash5................
```

## Example

* UTM: U33 362705.634106E 5762926.812914N
* Geohash (string): u33d9u9n4juh
* Geohash5 (number): 940245506947434320
* Lat/Lon (number, number): 52.496484, 13.437744

## References

* CLI Converter script: https://github.com/galtspace/galtproject-utils-js/blob/add-cli/cli.js

