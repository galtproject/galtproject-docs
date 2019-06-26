# ProtocolFeeMixer

* Contract has a single owner
* There are several manager roles allowed performing fee withdrawal and distribution actions. These roles are managed by the owner.
* Withdrawal sources are managed by the owner and represented as:
    * Contract (address)
    * Data to send (includes method to call and args to pass in) (bytes[])
* Destination sources are managed by the owner and represented as:
    * Address
    * Share (uint256) 0 <= share <= 100
