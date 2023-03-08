# RNS.js V2

## Overview of the API

### Setup

```
import { getEnsAddress, RNS } from '@rns-name-service/rnsjs'
import { ethers } from 'ethers'


const provider = new ethers.providers.JsonRpcProvider(
    "https://dataseed2.redlightscan.finance/",
    {
        chainId: 2611,
        name: "RedlightMainnet"
    }
)

const rns = new RNS({ 
    provider,
    rnsAddress: getEnsAddress('106') 
})

console.log(await rns.name('test.redlc').getAddress())
console.log(await rns.getName('0xA00edba30dD5F07fE4756988544E1b7613655002'))
```

### exports

```
default - RNS
getEnsAddress
getResolverContract
getRNSContract
namehash
labelhash
```

### RNS Interface

```
name(name: String) => Name
```

Returns a Name Object, that allows you to make record queries.

```
resolver(address: EthereumAddress) => Resolver
```

Returns a Resolver Object, allowing you to query names from this specific resolver. Most useful when querying a different resolver that is different than is currently recorded on the registry. E.g. migrating to a new resolver

```
async getName(address: EthereumAddress) => Promise<Name>
```

Returns the reverse record for a particular Ethereum address.

```
async setReverseRecord(name: Name) => Promise<EthersTxObject>
```

Sets the reverse record for the current Ethereum address

### Name Interface

```ts
async getOwner() => Promise<EthereumAddress>
```

Returns the owner/controller for the current RNS name.

```ts
async setOwner(address: EthereumAddress) => Promise<Ethers>
```

Sets the owner/controller for the current RNS name.

```ts
async getResolver() => Promise<EthereumAddress>
```

Returns the resolver for the current RNS name.

```ts
async setResolver(address: EthereumAddress) => Promise<EthereumAddress>
```

Sets the resolver for the current RNS name.

```ts
async getTTL() => Promise<Number>
```

Returns the TTL for the current RNS name.

```ts
async getAddress(coinId: String) => Promise<EthereumAddress>
```

Returns the address for the current RNS name for the coinId provided.

```ts
async setAddress(coinId: String, address: EthereumAddress) => Promise<EthersTxObject>
```

Sets the address for the current RNS name for the coinId provided.

```ts
async getContent() => Promise<ContentHash>
```

Returns the contentHash for the current RNS name.

```ts
async setContenthash(content: ContentHash) => Promise<EthersTxObject>
```

Sets the contentHash for the current RNS name.

```ts
async getText(key: String) => Promise<String>
```

Returns the text record for a given key for the current RNS name.

```ts
async setText(key: String, recordValue: String) => Promise<EthersTxObject>
```

Sets the text record for a given key for the current RNS name.

```ts
async setSubnodeOwner(label: String, newOwner: EthereumAddress) => Promise<EthersTxObject>
```

Sets the subnode owner for a subdomain of the current RNS name.

```ts
async setSubnodeRecord(label: String, newOwner: EthereumAddress, resolver: EthereumAddress, ttl: ?Number) => Promise<EthersTxObject>
```

Sets the subnode owner, resolver, ttl for a subdomain of the current RNS name in one transaction.

```ts
 async createSubdomain(label: String) => Promise<EthersTxObject>
```

Creates a subdomain for the current RNS name. Automatically sets the owner to the signing account.

```ts
async deleteSubdomain(label: String) => Promise<EthersTxObject>
```

Deletes a subdomain for the current RNS name. Automatically sets the owner to "0x0..."

## Resolver Interface

```ts
address
```

Static property that returns current resolver address

```ts
name(name) => Name
```

Returns a Name Object that hardcodes the resolver
