# keypom-docs-examples
Scripts referenced in the documentation tutorials

https://docs.keypom.xyz/


# 1. Simple Drop
## 1-1. keyPom core 사용
- https://docs.keypom.xyz/docs/next/Tutorials/Basics/simple-drops#testing
1. `cd keypom-docs-examples/basic-tutorials/simple-drop`
2. 계정 생성 후 `YOUR_ACCOUNT` 값을 내 계정으로 변경 
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
3. 루트에서 `yarn basic:simple:keypom` 실행

result 
```
$ node basic-tutorials/simple-drop/simple-example
Receipts: RDBAg6FFFFnAWAm749yiLHDkNnLEkmV9tQuqBLTE3p2, 92tBdoAdTMKUdgrPuJLerh5uEv5Gwi64i81sgo57qXcn
        Log [v2.keypom.testnet]: Current Block Timestamp: 1710814987623257482
        Log [v2.keypom.testnet]: 21 calls with 105000000000000 attached GAS. Pow outcome: 1.8602935. Required Allowance: 20248156910387200000000
        Log [v2.keypom.testnet]: Total required storage Yocto 17140000000000000000000
        Log [v2.keypom.testnet]: Current balance: 1.7010356, 
            Required Deposit: 1.2216215, 
            total_required_storage: 0.01714,
            Drop Fee: 0, 
            Key Fee: 0 Total Key Fee: 0,
            allowance: 0.1012407 total allowance: 0.2024815,
            access key storage: 0.001 total access key storage: 0.002,
            deposits less none FCs: 0.5 total deposits: 1 lazy registration: false,
            deposits for FCs: 0 total deposits for FCs: 0,
            uses per key: 5
            None FCs: 0,
            length: 2
            GAS to attach: 100000000000000
        Log [v2.keypom.testnet]: New user balance 0.479414
        Log [v2.keypom.testnet]: Fees collected 0
Public Keys:  [
  'ed25519:6aA8R2QSNUq5vn4rZoLBmTHPkSwhR6RS3FDjG53gHNKN',
  'ed25519:BXopzATb6LGzgtkVMMeT3356SPamKzM6vsQszm9L41H6'
]
Linkdrops:  [
  'https://testnet.mynearwallet.com/linkdrop/v2.keypom.testnet/4d3zPhovQRJxgCPYJQARvmdJENCPHvQZEPGj1w6HYS1zNvmJD7c5kYYsFTFL5uqJ5sNc724D8CeoGf7Q7DyFeK3i',
  'https://testnet.mynearwallet.com/linkdrop/v2.keypom.testnet/3h8XQzd5GfMpMGMqChJkrjTicHPuutP4PDKDgMuHYDHgsqyaj4SyyHsTuqjdGPehgtzXZm1pp87SqYx4BKcuuiFW'
]
Keypom Contract Explorer Link: explorer.testnet.near.org/accounts/v2.keypom.testnet.com
```
- (link-drop 주체) fine-border.testnet: https://testnet.nearblocks.io/txns/DoBcmBuLi3C87MK27fTDC8vEeedhaeHQ2EodMP9D2Zvf
- (link-drop 받은 계정) won999.testnet: https://testnet.nearblocks.io/txns/5dqK9ykWGXMNggDPRRH6h8yWJbiffmVSaABQ7t1ijpYZ

## 1-2. near-api-js 사용 
1. 1~2 계정 설정 및 입력 부분은 1-1과 일치
2. 루트에서 `yarn basic:simple:naj` 실행

result 
```
$ node basic-tutorials/simple-drop/simple-near-example
Receipts: hUYuZbsr8kQvT1jTTRT4FKVeAdWYnoGzk5c9BE5bxv6, JDh5Yds7tRFDwBFogHYHePnqZvrNkFhgLuFNd2dczQ1r
        Log [v2.keypom.testnet]: 21 calls with 105000000000000 attached GAS. Pow outcome: 1.8602935. Required Allowance: 20248156910387200000000
        Log [v2.keypom.testnet]: Total required storage Yocto 10880000000000000000000
        Log [v2.keypom.testnet]: Current balance: 1.5011211, 
            Required Deposit: 1.0321281, 
            total_required_storage: 0.01088,
            Drop Fee: 0, 
            Key Fee: 0 Total Key Fee: 0,
            allowance: 0.0202481 total allowance: 0.0202481,
            access key storage: 0.001 total access key storage: 0.001,
            deposits less none FCs: 1 total deposits: 1 lazy registration: false,
            deposits for FCs: 0 total deposits for FCs: 0,
            uses per key: 1
            None FCs: 0,
            length: 1
            GAS to attach: 100000000000000
        Log [v2.keypom.testnet]: New user balance 0.4689929
        Log [v2.keypom.testnet]: Fees collected 0
Public Keys and Linkdrops:  {
  'ed25519:HVYDc6Pg49LqLLqrsycPWnDm9D8h2KLhbHXC9S1m3D5S': 'https://testnet.mynearwallet.com/linkdrop/v2.keypom.testnet/iFY6o9QMixfYMG6XCTz4nqbPpgk9cyukuHLwfmkQMAD28FzzacHBmMt2RBJEQZXyWdDgvkqHUifumx5QXQ3Nkvk'
}
Keypom Contract Explorer Link: explorer.testnet.near.org/accounts/v2.keypom.testnet.com
```
- (link-drop 주체) fine-border.testnet: https://testnet.nearblocks.io/txns/Dw1jqjwnDPotuUKbWWezVmLJezwiSc5UN4vmXX5Go7en
- (link-drop 받은 계정) won999.testnet: https://testnet.nearblocks.io/txns/Gz6Jou9RFVxjd43nCauCw1PSQx5i3hEaTocWmxFzknFh