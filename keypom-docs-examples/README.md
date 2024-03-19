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

# 2. fungible-token-drop
## 2-1. keyPom core 사용
- ft-tutorial을 통해 자체적으로 만든 ft 토큰 사용
- `yarn basic:ft:keypom`

result
```
yarn run v1.22.21
$ node basic-tutorials/fungible-token-drop/ft-example
Funder Fungible Token Balance:  999000000000000000000000000
Receipts: GfvSG3Cc5VRq2UDRYD5mnauVWeMWEo8HNHsNCKLZWBeM, 5tj5VTfTkfongizK8gM8SEFrq1vgDYUUd943VmK3BhXC, 7BQkL3pnby1CryMouVcyw4Y84WrpnWbCSgqHUE14S7RX
        Log [v2.keypom.testnet]: Current Block Timestamp: 1710852899159190371
        Log [v2.keypom.testnet]: 21 calls with 105000000000000 attached GAS. Pow outcome: 1.8602935. Required Allowance: 20248156910387200000000
        Log [v2.keypom.testnet]: was_ft_registered: false
        Log [v2.keypom.testnet]: Total required storage Yocto 15060000000000000000000
        Log [v2.keypom.testnet]: Current balance: 1.0464157, 
            Required Deposit: 1.0363081, 
            total_required_storage: 0.01506,
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
        Log [v2.keypom.testnet]: New user balance 0.0101076
        Log [v2.keypom.testnet]: Fees collected 0
        Log [v2.keypom.testnet]: FT contract was not already registered. Removing from set
        Log [v2.keypom.testnet]: Performing CCC to get storage from FT contract
Receipts: DTUMU5nBuhswWSS25fa24HTynUjDPt8rLBEcbNyh7h6B, AiWyibBfun6ik6w69cf3iqHB5N9KhK3cC3ozS7YtSAUZ, ACKMr8xqGYAUyUCYgLCo5iQeXkxWrbv2p5cgpka1VC7W
        Log [v2.keypom.testnet]: User has enough balance to cover FT storage. Subtracting 0.0025 from user balance. User balance is now 0.0076076
        Log [v2.keypom.testnet]: 21 calls with 105000000000000 attached GAS. Pow outcome: 1.8602935. Required Allowance: 20248156910387200000000
        Log [v2.keypom.testnet]: FT contract not registered. Performing cross contract call to transfer.won999.testnet and inserting back into set
Retrying transaction transfer.won999.testnet:Fz6vyTaXiS5nj1r2Xqtq2StMoXm3WSRrcxKh6hqZLa3p with new nonce.
Receipts: A7d13txV3HqoCS6DEDqsp1jMxUxfktxJG9RJLteidLPU, 7hPcjg5exNjJrn5YcQ5LC2f45RvvyVJmiefmtZCE37va, 8qZ8nCyFA9hh3itXaHhU5CmYZkgunCN2VWwqzJu3tom
        Log [transfer.won999.testnet]: EVENT_JSON:{"standard":"nep141","version":"1.0.0","event":"ft_transfer","data":[{"old_owner_id":"transfer.won999.testnet","new_owner_id":"v2.keypom.testnet","amount":"1"}]}
Receipt: CESpazSAGdZAP4GPUgUkLwa3i5FbSraDmZxDDbpZoqyM
        Log [transfer.won999.testnet]: New uses registered 1
Public Keys:  [ 'ed25519:NxnW64RAPJw4nz45fUsq22p3dg5wVwNPsfHXSiDJ6NT' ]
Linkdrops:  [
  'https://testnet.mynearwallet.com/linkdrop/v2.keypom.testnet/4YXYhJ1yCS3qbULNLmQDEbvDKGK9STRBGAnhw397nVjU8tVo9MKfQSuuD2sASEQREMfLcjpKYqjx7kCCisuQCk1d'
]
Keypom Contract Explorer Link: explorer.testnet.near.org/accounts/v2.keypom.testnet.com
✨  Done in 17.97s.
```

## 2-2. near-api-js 사용
- ft-tutorial을 통해 자체적으로 만든 ft 토큰 사용
- `yarn basic:ft:naj` 

result
```
yarn run v1.22.21
$ node basic-tutorials/fungible-token-drop/ft-near-example
Funder Fungible Token Balance:  998999999999999999999999999
Receipts: 5UGoJWCLtR74dh2NJCKC1vmZmA8iQKQjEi5gXABQFD5W, y54c8sRhr6wZifSURK2CF13PQ3BJSfbCXG9yrJgR6g4, FhoUpSJNDpdjmafzgQABxhPV7REqd7LVUD8GUEFzQBTJ
        Log [v2.keypom.testnet]: 21 calls with 105000000000000 attached GAS. Pow outcome: 1.8602935. Required Allowance: 20248156910387200000000
        Log [v2.keypom.testnet]: was_ft_registered: true
        Log [v2.keypom.testnet]: Total required storage Yocto 11780000000000000000000
        Log [v2.keypom.testnet]: Current balance: 1.5146276, 
            Required Deposit: 1.0330281, 
            total_required_storage: 0.01178,
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
        Log [v2.keypom.testnet]: New user balance 0.4815994
        Log [v2.keypom.testnet]: Fees collected 0
        Log [v2.keypom.testnet]: Performing CCC to get storage from FT contract
Receipts: 42iSwYysHU3Y764XYUcGBSAsgXfeHkmgFUt55ZYy2fvC, BqkQJBRnMyLP8YDkARKusfZCMsMB38RhN2X39vF4GvH8
        Log [v2.keypom.testnet]: User has enough balance to cover FT storage. Subtracting 0.0025 from user balance. User balance is now 0.4790994
        Log [v2.keypom.testnet]: 21 calls with 105000000000000 attached GAS. Pow outcome: 1.8602935. Required Allowance: 20248156910387200000000
        Log [v2.keypom.testnet]: FT contract already registered. Refunding user balance for 0.00125. Balance is now 0.4803494
Retrying transaction transfer.won999.testnet:8HaaaFrPe1CDrys8w9P7p9Cv7TiqCWksCjg7JbQksAT with new nonce.
Receipts: 6zWFCUPWpWH7Mq9oqnr8wAZkjdq4PJzVVZWoDXVJqzZW, HyVoCGk9S9b1afr8hPctadTMEwtnE87vhLiwcZST3dFx
        Log [transfer.won999.testnet]: The account is already registered, refunding the deposit
dropSupplyForOwner:  2
dropsForOwner:  [
  {
    drop_id: '694',
    owner_id: 'transfer.won999.testnet',
    deposit_per_use: '1000000000000000000000000',
    ft: {
      contract_id: 'transfer.won999.testnet',
      sender_id: 'transfer.won999.testnet',
      balance_per_use: '1000000000000000000000000',
      ft_storage: '1250000000000000000000'
    },
    config: null,
    metadata: null,
    registered_uses: 0,
    required_gas: '100000000000000',
    next_key_id: 1
  }
]
694
Retrying transaction transfer.won999.testnet:6Mb6zZoygFaKDDqJott6eTBKdhL3crRvr1oTEnF5u7TY with new nonce.
Receipts: JCwsBSPimgw53kxgAsLtXdyd8b3jfm1yVRX8X8ra4kCd, 8Qv8mveQ22hMKS9L1EVfmGXEN9dC2PZ7r7P9XwRYNZKz, Dj2LNoqtvfTECkv1uwi2L1WaXJe5WiSKtr2Y6jx9nFYC
        Log [transfer.won999.testnet]: EVENT_JSON:{"standard":"nep141","version":"1.0.0","event":"ft_transfer","data":[{"old_owner_id":"transfer.won999.testnet","new_owner_id":"v2.keypom.testnet","amount":"1000000000000000000000000"}]}
Receipt: HE1YJjTa3EFybXGh1hCMmeEfRDSDPAAMFFHBX5Cxb4NQ
        Log [transfer.won999.testnet]: New uses registered 1
Public Keys and Linkdrops:  {
  'ed25519:7RquGu4rndLMA2iCkpJdp19eHqyG3gLC8S1wmpaXVBQv': 'https://testnet.mynearwallet.com/linkdrop/v2.keypom.testnet/2kRdFeUstFt2NKZJATPLqPjyu9aHJvvAmZHDgx3Zdot9ggXxP1KPZEhAZpb2ex6K6g4ixkmZc3WLGvefJX5CZSWn'
}
Keypom Contract Explorer Link: explorer.testnet.near.org/accounts/v2.keypom.testnet.com
✨  Done in 25.21s.
```