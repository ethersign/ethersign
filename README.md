

# Ethersign

http://ethersign.github.io

Ethersign is a javascript package and offline app that allows any user to prove to any other user or website that they know the Ethereum Private Key for any particular Ethereum Address.  This is done using the same cryptographic signatures used by miners to initiate transactions.  There are three steps:

    a. The service generates a secure-random cryptographic challenge which is given to the client. (generateEllipticCurveChallengeDigest)

    b. The client uses their private key to generate a signature of the challenge and they give it back to the service. (signEllipticCurveChallenge)

    c. The service checks that the signature is valid for that challenge and extracts the public key (and this public address) from the signature.   (validateEllipticCurveSignature)


Now the service knows that the client owns the private key for that public address.  The client never gave out their private key or exposed it online.  Step 'b' occurs offline.  

As an example use case, using these three tools, it is possible to build a webform  that asks a user for a public address, asks them to sign a challenge to prove ownership, and then records the fact that they must know the private key.  This is useful for tying their account identity to smartcontracts on the blockchain.

This is really just a nice wrapper for the library https://github.com/ethereumjs/ethereumjs-util

### How to Use

**In a terminal**
npm install ether-sign

```
var ethersign = require('ether-sign')
```


### Signing the Proof-Of-Key Challenges
Visit http://ethersign.github.io in order to sign these cryptographic challenges and prove that you own the private key (step 'b' above)


### Testing with Mocha

npm test


## Sample Use case
A client named "ETHan" owns a Cryptopunk icon and wants to use it as his avatar on Github.com.  This cryptopunk is stored at Public Address 0xacbFBdc72626c2264a72a352733ae58244ee3BEf.  

1. TETHan fills out a form on Github stating that his public address is 0xacbFBdc72626c2264a72a352733ae58244ee3BEf.  

2. Github doesn't believe him so it generates a Cryptographic Challenge with Ethersign using the message 'test' which results in the following which is shown to ETHan.  

Cryptographic Challenge:

4a5c5d454721bbbb25540c3317521e71c373ae36458f960d2ad46ef088110e95

3.  ETHan visits ethersign.github.io on a secure device and disconnects from the internet.  He pastes in the challenge and his private key which is 2c6036ab2f51cb1bfa17a3ffb57abf93a183d9d3887bc9e73cd28d9be57e4d56.  This results in a signature.  

Signature Response:

0x041a261a9988d60cc59347c217ac32268b4491fd90b7d367b5392d7b20dd63fc1d10c56dae8666e9a860719d6d4772af6f5ead8ce1f9150a461b5b618a3e5ea300

4.  ETHan gives Github this signature and they use Ethersign to validate it against the Public Key and the Challenge.  Github noticed that it came back valid so they add a new record in their database stating that ETHan does indeed control the account at Public Key 0xacbFBdc72626c2264a72a352733ae58244ee3BEf and his avatar is now one of the Cryptopunks at that address.

5. At no time did ETHan expose his private key on the internet, but now Github knows that he is the owner of the account.  Ethersign is not a service or a company, it is not in the cloud, it is just a small set of cryptographic math functions.  
