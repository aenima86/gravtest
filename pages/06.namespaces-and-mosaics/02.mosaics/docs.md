---
title: Mosaics
taxonomy:
    category: docs
---

 
 NEM mosaics are assets that expose additional properties and other features. Each mosaic has an underlying mosaic definition. To be able to create a mosaic definition, an account must rent at least one root namespace which the mosaic definition can then refer to. The basic data for a mosaic definition consists of **mosaic id**: the mosaic id consists of two parts, a namespace id and a mosaic name. When representing the mosaic id as string the two parts are concatenated via a '*': For example if the namespace id is 'makoto.metals.silver' and the mosaic name is 'coin' then the string representation would be 'makoto.metals.silver * coin'. Since mosaic ids should be unique, the mosaic name has to be unique within the namespace the mosaic definition refers to. The maximum length for a mosaic name is 32 characters. Allowed characters are a, b, c, ..., z, 0, 1, 2, ..., 9, ', _ , - but the first character must be a letter from the alphabet. **description**: Each definition needs a description of the mosaic. The description may not exceed a length of 512 characters. There is no limitation for the characters used in the description. **properties**: The behavior of a mosaic can be customized by a set of properties. If no properties are supplied then default properties are applied. Supported properties are: **initialSupply**: The creator can specify an initial supply of mosaics when creating the definition. The supply is given in entire units of the mosaic, **not** in smallest sub-units. The initial supply must be in the range of 0 and 9,000,000,000. The default value is "1000". **divisibility**: The divisibility determines up to what decimal place the mosaic can be divided into. Thus a divisibility of 3 means that a mosaic can be divided into smallest parts of 0.001 mosaics, i.e. milli mosaics is the smallest sub-unit. When transferring mosaics via a transfer transaction the quantity transferred is given in multiples of those smallest parts. The divisibility must be in the range of 0 and 6. The default value is "0". **supplyMutable**: The creator can choose between a definition that allows a mosaic supply change at a later point or an immutable supply. Allowed values for the property are "true" and "false". The default value is "false". **transferable**: The creator can choose if the mosaic definition should allow for transfers of the mosaic among accounts other than the creator. If the property 'transferable' is set to "false", only transfer transactions having the creator as sender or as recipient can transfer mosaics of that type. If set to "true" the mosaics can be transferred to and from arbitrary accounts. Allowed values for the property are thus "true" and "false". The default value is "true". **levy**: The creator can demand that for each transfer of a mosaic of that type a special fee is collected from the sender and send to an account of his choice (thus the creator can specify his own account as recipient of this fee). The data for the levy is the following: **fee type:** There are two fee types supported, absolute fee and percentile fee. absolute fee: The fee is specified as absolute quantity and thus does not depend on the quantity that is transferred. percentile fee: The fee is specified as multiple of the percentile of the quantity that is transferred. The fee is thus linearly increasing with the transferred mosaic quantity. **recipient:** The recipient of the levy. This can be any account. **mosaic id:** The id of the mosaic in which the fee has to be paid. Any existing mosaic id can be specified. If the creator wants the fee to be paid in XEM, then (s)he has to use the mosaic id 'nem * xem'. **fee:** The fee quantity. The interpretation is dependent on the field 'fee type', see above. 

 
 A mosaic definition can be created via a Appendix A: MosaicDefinitionCreationTransaction . In addition to the usual transaction fee there is a creation fee. This fee is paid to the so called creation fee sink which is a special account with address NBMOSAICOD4F54EE5CDMR23CCBGOAM2XSIUX6TRS in the main net and TBMOSAICOD4F54EE5CDMR23CCBGOAM2XSJBR5OLC in the test net. The fee for creating a mosaic definition is 50000 XEM. 

 
There is one predefined mosaic which represents the XEM coin. The data for this XEM mosaic is: namespace: nem name: xem initial supply: 8,999,999,999 divisibility: 6 supply mutable: false transferable: true levy: none 

 
### 7.4.1 Retrieving mosaic definitions 
| API path: | Request type:  |
|------|------|
| /namespace/mosaic/definition/page | GET|

 
##### Description: 
Gets the mosaic definitions for a given namespace. The request supports paging. The request return an array of MosaicDefinitionMetaDataPair objects.

 
##### Parameter: 

| Parameter | Description |
|------|------|
|  namespace   |  The namespace id.   |
|  id   |  The topmost mosaic definition database id up to which root mosaic definitions are returned. The parameter is optional. If not supplied the most recent mosaic definitiona are returned.   |
|  pagesize   |  The number of mosaic definition objects to be returned for each request. The parameter is optional. The default value is 25, the minimum value is 5 and hte maximum value is 100.   |

 
##### Example: 
http://127.0.0.1:7890/namespace/mosaic/definition/page?namespace=makoto.metal.coins 

 
##### Example of returned JSON object: 
```json
{
        "data": [{
        "meta" {
        "id": 3541
        },
        "mosaic": {
        "creator": "10cfe522fe23c015b8ab24ef6a0c32c5de78eb55b2152ed07b6a092121187100",
        "id": {
        "namespaceId": "makoto.metal.coins",
        "name": "silver coin"
        },
        "description": "Real silver coins, pure silver",
        "properties": [{
        "name": "divisibility",
        "value": "0"
        },{
        "name": "initialSupply",
        "value": "1000"
        },{
        "name": "supplyMutable",
        "value": "false"
        },{
        "name": "transferable",
        "value": "true"
        }]
        }
        }]
        }
``` 
##### Possible Errors: 
NIS returns an error if the namespace parameter is missing or invalid. See Appendix B: NIS Errors for details about errors. 

 
