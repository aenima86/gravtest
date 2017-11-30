---
title: Transaction fees
taxonomy:
    category: docs
---

 
In order for the harvesters to have an incentive to run a node that is harvesting blocks, users have to pay a fee for every transaction that is going to be included in a block chain.

 
Different transaction types have different fees. In order to get a transaction validated by a NIS, the fee provided must be at least the minimum fee.

 
**Note:** Depending on the transaction type there could be additional fees due to the action during transaction execution (e.g. renting a namespace)

 
The following chart summarizes the minimum fees for each transaction type. All calculation are done with rounded amounts of XEM (i.e. micro XEM are ignored):

 

| Parameter | Description |
|------|------|
|  Transfer transaction   |  The fee is the sum of the fee for transferring an amount of XEM and the fee for appending a message to the transaction. 1) Fees for transferring XEM to another account: 1 xem per 10,000 xem transferred, capped at 25 xem Example: 4 xem fee for a 45,000 xem transfer, 25 xem fee for a 500,000 xem transfer. 2) Fees for appending a message to a transaction: 1 xem per commenced 32 message bytes (messageLength / 32 + 1). Example: The unencrypted message „The New Economy Movement will change the world!!!” has a length 49 characters and thus will cost 2 xem fee. 3) Fees for transferring a mosaic to another account: i) mosaics with divisibility of 0 and a maximum supply of 10,000 are called small business mosaics. 1 xem fee for any transfer of a small business mosaic. ii) For each mosaic that is transferred the fee is calculated the following way: a) given a mosaic with initial supply s, divisibility d and quantity q, the XEM equivalent is (round to the next smaller integer) xemEquivalent = (8,999,999,999 * q) / (s * 10^d)  To take into account the total quantities for different mosaics, an adjustment term is calculated. For a mosaic called m calculate maxMosaicQuantity = 9,000,000,000,000,000 totalMosaicQuantity = mosaic m supply * 10 ^ (mosaic m divisibility) supplyRelatedAdjustment = floor(0.8 * ln(maxMosaicQuantity / totalMosaicQuantity) Then the fee is calculated as fee = max(1L, xemFee - supplyRelatedAdjustment) Example: Suppose you have a mosaic with 9,000,000 supply and divisibility of 3. totalMosaicQuantity = 9,000,000 * 1,000 = 9,000,000,000 supplyRelatedAdjustment = floor(0.8 * ln(9,000,000,000,000,000 / 9,000,000,000)) = floor(11.052) = 11 Transferring 150 such mosaics (i.e. a quantity of 150,000 smallest units) has xemEquivalent = (8,999,999,999 * 150,000) / (9,000,000 * 10^3) = 149,999 xemFee = 14 xem So the transction will have the following fee: fee = 14 xem - 11 xem = 3 xem   |
|  Importance transfer transaction   |  6 XEM   |
|  Aggregate modification transaction   |  10 + 6 * number of modifications + 6 (if a min cosignatory change is involved) Example: Adding 3 cosignatories to an account without changing the min cosignatories will cost 10 + 6 * 3 = 28 XEM. Adding 3 cosignatories to an account and changing the min cosignatories will cost 10 + 6 * 3 + 6 = 34 XEM.    |
|  Multisig transaction   |  6 XEM   |
|  Multisig signature transaction   |  6 XEM   |
|  Provision namespace transaction   |  20 XEM   |
|  Mosaic definition creation transaction   |  20 XEM   |
|  Mosaic supply change transaction   |  20 XEM   |

 
