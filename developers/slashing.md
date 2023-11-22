---
description: This section covers the slashing mechanics for validators in Celestia.
---

# Slashing on Celestia

Slashing is mechanism employed in PoS blockchains that is used to deter
and punish malicious behavior. It functions by removing a percentage
of a validators stake each time they act harmfully towards the network.

Celestia is built with the Cosmos-SDK and implements the module `x/slashing`.

If a Validator gets slashed, delegators bonded to that validator will also
have the same percentage of their delegated funds slashed.

The following are the conditions for a validator to get slashed:

1. **Downtime**: If a validator is offline for more than 75% of a rolling window
   of the last 5,000 blocks, they will lose 0% of their stake.
   During this slashing event, the validator is removed from the validator set
   temporarily and spends time in "jail" for a period of 1 minute during which
   they will be unable to propose new blocks or earn rewards.
   After the jail period, the validator can send an unjail request to
   rejoin the validator set.

2. **Double signing**: This is a more severe offense and results in a larger
   percentage loss. If a validator engages in double signing, the validator
   will lose 2% of their stake and their stake will be returned to them.
   The validator will be permanently removed from the validator set and
   will not have the ability to unjail. Delegators bonded to that validator will
   automatically enter the unbonding period for 21 days, and can delegate to another
   validator after they have been unbonded.

For more details on the slashing parameters, refer to the
[Celestia App Specifications](https://celestiaorg.github.io/celestia-app/specs/params.html#module-parameters)
page.