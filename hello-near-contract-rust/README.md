# Hello NEAR Contract

The smart contract exposes two methods to enable storing and retrieving a greeting in the NEAR network.

```rust
const DEFAULT_GREETING: &str = "Hello";

#[near_bindgen]
#[derive(BorshDeserialize, BorshSerialize)]
pub struct Contract {
    greeting: String,
}

impl Default for Contract {
    fn default() -> Self {
        Self { greeting: DEFAULT_GREETING.to_string() }
    }
}

#[near_bindgen]
impl Contract {
    // Public: Returns the stored greeting, defaulting to 'Hello'
    pub fn get_greeting(&self) -> String {
        return self.greeting.clone();
    }

    // Public: Takes a greeting, such as 'howdy', and records it
    pub fn set_greeting(&mut self, greeting: String) {
        // Record a log permanently to the blockchain!
        log!("Saving greeting {}", greeting);
        self.greeting = greeting;
    }
}
```

<br />

# Quickstart

1. Make sure you have installed [rust](https://rust.org/).
2. Install the [`NEAR CLI`](https://github.com/near/near-cli#setup)

<br />

## 1. Build, Test and Deploy
To build the contract you can execute the `./build.sh` script, which will in turn run:

```bash
rustup target add wasm32-unknown-unknown
cargo build --target wasm32-unknown-unknown --release
```

create account
```bash
cargo-near near create-dev-account use-random-account-id autogenerate-new-keypair save-to-legacy-keychain network-config testnet create
```

```
Your transaction:
signer_id:    testnet
actions:
   -- create account:      fine-border.testnet
   -- add access key:     
                   public key:   ed25519:3hf3P2NBtA3V3vdX2HmyZ6hmrUJ1xS6y5VZjLp91kTQp
                   permission:   FullAccess
```


Then, run the `./deploy.sh` script, which will in turn run:

```bash
near deploy <account-id> <wasm-file>
near deploy fine-border.testnet ./target/wasm32-unknown-unknown/release/hello_near.wasm
```

<br />

## 2. Retrieve the Greeting

`get_greeting` is a read-only method (aka `view` method).

`View` methods can be called for **free** by anyone, even people **without a NEAR account**!

```bash
# Use near-cli to get the greeting
near view <dev-account> get_greeting
near view fine-border.testnet get_greeting
```

<br />

## 3. Store a New Greeting
`set_greeting` changes the contract's state, for which it is a `change` method.

`Change` methods can only be invoked using a NEAR account, since the account needs to pay GAS for the transaction. In this case, we are asking the account we created in step 1 to sign the transaction.

```bash
# Use near-cli to set a new greeting
near call <dev-account> set_greeting '{"greeting":"howdy"}' --accountId <dev-account>

near call fine-border.testnet set_greeting '{"greeting":"howdy"}' --accountId fine-border.testnet
```

**Tip:** If you would like to call `set_greeting` using your own account, first login into NEAR using:

```bash
# Use near-cli to login your NEAR account
near login
```

and then use the logged account to sign the transaction: `--accountId <your-account>`.