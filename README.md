

# Ether-sign

http://ethersign.github.io

Ether-sign is a javascript package and offline app that allows any user to prove to any other user or website that they know the Ethereum Private Key for any particular Ethereum Address.  This is done using the same cryptographic signatures used by miners to initiate transactions.  There are three steps:

    a. The service generates a secure-random cryptographic challenge which is given to the client. (generateEllipticCurveChallengeDigest)

    b. The client uses their private key to generate a signature of the challenge and they give it back to the service. (signEllipticCurveChallenge)

    c. The service checks that the signature is valid for that challenge and extracts the public key (and this public address) from the signature.   (validateEllipticCurveSignature)


Now the service knows that the client owns the private key for that public address.  The client never gave out their private key or exposed it online.  Step 'b' occurs offline.  

As an example use case, using these three tools, it is possible to build a webform  that asks a user for a public address, asks them to sign a challenge to prove ownership, and then records the fact that they must know the private key.  This is useful for tying their account identity to smartcontracts on the blockchain.

### How to Use

npm install ether-sign

```
var ethersign = require('ether-sign')
```


### Signing the Proof-Of-Key Challenges
Visit http://ethersign.github.io in order to sign these cryptographic challenges and prove that you own the private key (step 'b' above)


### Testing with Mocha

npm test
