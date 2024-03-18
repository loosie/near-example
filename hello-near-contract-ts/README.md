# Hello NEAR Contract

The smart contract exposes two methods to enable storing and retrieving a greeting in the NEAR network.

```ts
@NearBindgen({})
class HelloNear {
  greeting: string = "Hello";

  @view // This method is read-only and can be called for free
  get_greeting(): string {
    return this.greeting;
  }

  @call // This method changes the state, for which it cost gas
  set_greeting({ greeting }: { greeting: string }): void {
    // Record a log permanently to the blockchain!
    near.log(`Saving greeting ${greeting}`);
    this.greeting = greeting;
  }
}
```

<br />

# Quickstart

1. Make sure you have installed [node.js](https://nodejs.org/en/download/package-manager/) >= 16.
2. Install the [`NEAR CLI`](https://github.com/near/near-cli#setup)

<br />

## 1. Build and Deploy the Contract
You can automatically compile and deploy the contract in the NEAR testnet by running:

```bash
npm run build
npm run test 
npm run deploy
```

create account
```bash
npm i -g cargo-near
cargo-near near create-dev-account use-random-account-id autogenerate-new-keypair save-to-legacy-keychain network-config testnet create
```

```
signer_id:    testnet
actions:
   -- create account:      quirky-head.testnet
   -- add access key:     
                   public key:   ed25519:AK3YRBqeEbEBfvyALnMgzQgUHDb87NQSZ6Krj72HLbuG
                   permission:   FullAccess
```

<br />

## 2. Deploy the Contract
```bash
near deploy <account-id> <wasm-file>
near deploy quirky-head.testnet ./build/hello_near.wasm
```

```
Deploying contract ./build/hello_near.wasm in quirky-head.testnet
Done deploying to quirky-head.testnet
Transaction Id 4VaUPQz2Wdz5LyBvk3B8Bc6MsMEMWKsQeuNGZ38uiPKz
Open the explorer for more info: https://testnet.nearblocks.io/txns/4VaUPQz2Wdz5LyBvk3B8Bc6MsMEMWKsQeuNGZ38uiPKz
```

## 3. Retrieve the Greeting

`get_greeting` is a read-only method (aka `view` method).

`View` methods can be called for **free** by anyone, even people **without a NEAR account**!

```bash
# Use near-cli to get the greeting
near view <dev-account> get_greeting

near view quirky-head.testnet get_greeting
```

```bash
> near view quirky-head.testnet get_greeting
View call: quirky-head.testnet.get_greeting()
'Hello'
```

<br />

## 4. Store a New Greeting
`set_greeting` changes the contract's state, for which it is a `call` method.

`Call` methods can only be invoked using a NEAR account, since the account needs to pay GAS for the transaction.

```bash
# Use near-cli to set a new greeting
near call <dev-account> set_greeting '{"greeting":"howdy"}' --accountId <dev-account>

near call quirky-head.testnet set_greeting '{"greeting": "Hello, World!"}' --accountId quirky-head.testnet
```

```
> near call quirky-head.testnet set_greeting '{"greeting": "Hello, World!"}' --accountId quirky-head.testnet
Scheduling a call: quirky-head.testnet.set_greeting({"greeting": "Hello, World!"})
Receipt: DkK23o6twDNDUrtcFMdqXY6CW7L9kE7fTeibcFwBtY67
        Log [quirky-head.testnet]: Saving greeting Hello, World!
Transaction Id GzVNmG8ipAcHzUJKiMXTEpSLku9JzNfZPwT2jPmNxZYd
Open the explorer for more info: https://testnet.nearblocks.io/txns/GzVNmG8ipAcHzUJKiMXTEpSLku9JzNfZPwT2jPmNxZYd
```

**Tip:** If you would like to call `set_greeting` using your own account, first login into NEAR using:

```bash
# Use near-cli to login your NEAR account
near login

near login --accountId quirky-head.testnet
```

and then use the logged account to sign the transaction: `--accountId <your-account>`.