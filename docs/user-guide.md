# User Guide

All information for developers using `vapjs-account` should consult this document.

## Install

```
npm install --save vapjs-account
```

## Usage

```js
const generate = require('vapjs-account').generate;

console.log(generate('892h@fs8sk^2h8s8shfs.jk39hsoi@hohskd..'));

/* result
{
  address: '0x...',
  privateKey: '0x...',
  publicKey: '0x....',
}
*/
```

## API Design

### generate

[index.js:vapjs-account](../../../blob/master/src/index.js "Source code on GitHub")

Intakes a string of entropy, and outputs an address private key and public key.

**Parameters**

- `entropy` **String** a single string of entropy (`IMPORTANT NOTE`: be sure to make it long, complex and well sourced entropy)

Result output generated account **Object**.

```js
const generate = require('vapjs-account').generate;

console.log(generate('892h@fs8sk^2h8s8shfs.jk39hsoi@hohskd..'));

/* result
{
  address: '0x...',
  privateKey: '0x...',
  publicKey: '0x....',
}
*/
```

### getAddress

[index.js:vapjs-account](../../../blob/master/src/index.js "Source code on GitHub")

Intakes a public key buffer object, outputs an Vapory 20 byte address

**Parameters**

- `publicKey` **Object** public key buffer object

Result output an Vapory 20 byte address **String**.

```js
const getAddress = require('vapjs-account').getAddress;

console.log(getAddress(<Buffer instance>));

/* result '0x......' */
```

### getChecksumAddress

[getChecksumAddress.js:vapjs-account](../../../blob/master/src/index.js "Source code on GitHub")

Intakes an address, outputs a checksum address.

**Parameters**

- `address` **String** a single Vapory address as a 20 byte hex string

Result output checksum address **String**.

```js
const getChecksumAddress = require('vapjs-account').getChecksumAddress;

console.log(getChecksumAddress('0x.....'));

/* result 0x..... */
```

### privateToPublic

[index.js:vapjs-account](../../../blob/master/src/index.js "Source code on GitHub")

Intakes a single private key, outputs a public key Buffer instance.

**Parameters**

- `privateKey` **String** a single 32 byte hex string (with hex prefix).

Result output public key Buffer instance **Object**.

```js
const privateToPublic = require('vapjs-account').privateToPublic;

console.log(privateToPublic(sha3('892h@fs8sk^2h8s8shfs.jk39hsoi@hohskd..')));

/* result <Buffer ...> */
```

### publicToAddress

[index.js:vapjs-account](../../../blob/master/src/index.js "Source code on GitHub")

Intakes a single public key instance, outputs an Vapory standard 20 byte hex string address.

**Parameters**

- `publicKey` **Object** a public key buffer instance object

Result output Vapory standard 20 byte checksum address **String**.

Note, the address exported is the checksum address, `.toLowerCase` when using with modules that do not support the casing mixture.

```js
const publicToAddress = require('vapjs-account').publicToAddress;

console.log(publicToAddress(<Buffer instance>));

// result '0x......'
```

### privateToAccount

[index.js:vapjs-account](../../../blob/master/src/index.js "Source code on GitHub")

Intakes a single private key, outputs an account object containing three hex strings, `publicKey`, `privateKey` and `address`.

**Parameters**

- `privateKey` **String** a single 32 byte private key string (hex prefixed).

Result output account **Object**.

```js
const privateToAccount = require('vapjs-account').privateToAccount;

console.log(privateToAccount(sha3('892h@fs8sk^2h8s8shfs.jk39hsoi@hohskd..')));

/* result
{
  address: '0x...',
  privateKey: '0x...',
  publicKey: '0x....',
}
*/
```

Note, the address exported is the checksum address, `.toLowerCase` when using with modules that do not support the casing mixture.

## A Note on Entropy and Account Safety

In order to generate an account that is safe for use, you must generate a lot of entropy. The larger, more complex, more hashed and more sourced the better. Please be sure to use very powerful entropy generation tools and sources.

See:
https://github.com/keybase/more-entropy
https://github.com/ConsenSys/eth-lightwallet
https://github.com/mdp/gibberish-aes/

## Entropy Used

This module uses [`randombytes`](https://github.com/crypto-browserify/randombytes) for some extra entropy. This module does not work in older browsers and will throw an error. In node, this module uses `crypto.randomBytes`, while in the browser it uses the `window` crypto module. Random bytes is purely for some basic entropy saftey and is in no way a solid replacement for good entropy. It is up to you to provide extensive entropy for your key generation.

## Browser Builds

`vapjs` provides production distributions for all of its modules that are ready for use in the browser right away. Simply include either `dist/vapjs-account.js` or `dist/vapjs-account.min.js` directly into an HTML file to start using this module. Note, an `vapSha3` object is made available globally.

```html
<script type="text/javascript" src="vapjs-account.min.js"></script>
<script type="text/javascript">
vapSha3(...);
</script>
```

Note, even though `vapjs` should have transformed and polyfilled most of the requirements to run this module across most modern browsers. You may want to look at an additional polyfill for extra support.

Use a polyfill service such as `Polyfill.io` to ensure complete cross-browser support:
https://polyfill.io/

## Latest Webpack Figures

```
Hash: ab378ace2dcbcdc84923                                                            
Version: webpack 2.1.0-beta.15
Time: 1041ms
               Asset    Size  Chunks             Chunk Names
    vapjs-account.js  313 kB       0  [emitted]  main
vapjs-account.js.map  385 kB       0  [emitted]  main
  [37] multi main 28 bytes {0} [built]
    + 37 hidden modules

Hash: f6b69ff438836239c7a6                                                            
Version: webpack 2.1.0-beta.15
Time: 4124ms
               Asset    Size  Chunks             Chunk Names
vapjs-account.min.js  164 kB       0  [emitted]  main
  [37] multi main 28 bytes {0} [built]
    + 37 hidden modules
```

## Other Awesome Modules, Tools and Frameworks

### Foundation
 - [web3.js](https://github.com/vaporyco/web3.js) -- the original Vapory JS swiss army knife **Vapory Foundation**
 - [vaporyjs](https://github.com/vaporycojs) -- critical vapory javascript infrastructure **Vapory Foundation**
 - [browser-solidity](https://vapory.github.io/browser-solidity) -- an in browser Solidity IDE **Vapory Foundation**

### Nodes
  - [geth](https://github.com/vaporyco/go-vapory) Go-Vapory
  - [parity](https://github.com/ethcore/parity) Rust-Vapory build in Rust
  - [testrpc](https://github.com/vaporycojs/testrpc) Testing Node (vaporyjs-vm)

### Testing
 - [wafr](https://github.com/silentcicero/wafr) -- a super simple Solidity testing framework
 - [truffle](https://github.com/ConsenSys/truffle) -- a solidity/js dApp framework
 - [embark](https://github.com/iurimatias/embark-framework) -- a solidity/js dApp framework
 - [dapple](https://github.com/nexusdev/dapple) -- a solidity dApp framework
 - [chaitherium](https://github.com/SafeMarket/chaithereum) -- a JS web3 unit testing framework
 - [contest](https://github.com/DigixGlobal/contest) -- a JS testing framework for contracts

### Wallets
 - [ethers-wallet](https://github.com/ethers-io/ethers-wallet) -- an amazingly small Vapory wallet
 - [metamask](https://metamask.io/) -- turns your browser into an Vapory enabled browser =D

## Our Relationship with Vapory & VaporyJS

 We would like to mention that we are not in any way affiliated with the Vapory Foundation or `vaporyjs`. However, we love the work they do and work with them often to make Vapory great! Our aim is to support the Vapory ecosystem with a policy of diversity, modularity, simplicity, transparency, clarity, optimization and extensibility.

 Many of our modules use code from `web3.js` and the `vaporyjs-` repositories. We thank the authors where we can in the relevant repositories. We use their code carefully, and make sure all test coverage is ported over and where possible, expanded on.

## A Special Thanks

A special thanks to Richard Moore for building `ethers-wallet` and other amazing things. Aaron Davis (@kumavis) for his guidence.
