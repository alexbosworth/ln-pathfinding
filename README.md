# Lightning Network Pathfinding

[![npm version](https://badge.fury.io/js/ln-service.svg)](https://badge.fury.io/js/ln-pathfinding)

## Methods

- [calculateHops](#calculateHops) - Pathfind to get payment hops from channels
- [calculatePaths](#calculatePaths) - Pathfind to find multiple routes to pay

### calculateHops

Calculate hops between start and end nodes

    {
      channels: [{
        capacity: <Capacity Tokens Number>
        id: <Standard Channel Id String>
        policies: [{
          base_fee_mtokens: <Base Fee Millitokens String>
          cltv_delta: <CLTV Delta Number>
          fee_rate: <Fee Rate Number>
          is_disabled: <Channel is Disabled Bool>
          max_htlc_mtokens: <Maximum HTLC Millitokens String>
          min_htlc_mtokens: <Minimum HTLC Millitokens String>
          public_key: <Public Key Hex String>
        }]
      }]
      end: <End Public Key Hex String>
      [ignore]: [{
        [channel]: <Standard Format Channel Id String>
        public_key: <Public Key Hex String>
      }]
      mtokens: <Millitokens Number>
      start: <Start Public Key Hex String>
    }

    @throws
    <Error>

    @returns
    {
      [hops]: [{
        base_fee_mtokens: <Base Fee Millitokens String>
        channel: <Standard Channel Id String>
        channel_capacity: <Channel Capacity Tokens Number>
        cltv_delta: <CLTV Delta Number>
        fee_rate: <Fee Rate Number>
        public_key: <Public Key Hex String>
      }]
    }

Example:

```node
const {calculateHops} = require('ln-pathfinding');
const {getIdentity, getNetworkGraph} = require('ln-service');
const {channels} = await getNetworkGraph({lnd});
const end = 'destinationPublicKeyHexString';
const start = (await getIdentity({lnd})).public_key;_
const {hops} = calculateHops({channels, end, start, mtokens: '1000'});
```

### calculatePaths

Calculate multiple routes to a destination

    {
      channels: [{
        capacity: <Capacity Tokens Number>
        id: <Standard Channel Id String>
        policies: [{
          base_fee_mtokens: <Base Fee Millitokens String>
          cltv_delta: <CLTV Delta Number>
          fee_rate: <Fee Rate Number>
          is_disabled: <Channel is Disabled Bool>
          max_htlc_mtokens: <Maximum HTLC Millitokens String>
          min_htlc_mtokens: <Minimum HTLC Millitokens String>
          public_key: <Public Key Hex String>
        }]
      }]
      end: <End Public Key Hex String>
      [limit]: <Paths To Return Limit Number>
      mtokens: <Millitokens Number>
      start: <Start Public Key Hex String>
    }

    @throws
    <Error>

    @returns
    {
      [paths]: [{
        hops: [{
          base_fee_mtokens: <Base Fee Millitokens String>
          channel: <Standard Channel Id String>
          channel_capacity: <Channel Capacity Tokens Number>
          cltv_delta: <CLTV Delta Number>
          fee_rate: <Fee Rate Number>
          public_key: <Public Key Hex String>
        }]
      }]
    }

Example:

```node
const {calculatePaths} = require('ln-pathfinding');
const {getIdentity, getNetworkGraph} = require('ln-service');
const {channels} = await getNetworkGraph({lnd});
const end = 'destinationPublicKeyHexString';
const start = (await getIdentity({lnd})).public_key;
const {paths} = calculatePaths({channels, end, start, mtokens: '1000'});
```
