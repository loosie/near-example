# FT tutorial
- https://docs.near.org/tutorials/fts/introduction
- https://github.com/near-examples/ft-tutorial

# Learning Step
1. Pre-deployed contract
    - 스마트 컨트랙트를 코딩, 생성 또는 배포할 필요 없이 FT를 받을 수 있다.
2. Contract architecture	
    - FT 스마트 컨트랙트의 기본 아키텍처를 알아보고 코드를 컴파일해보자.
3. Defining a Token
    - FT를 갖는다는 것이 무엇을 의미하는지, 어떻게 나만의 토큰을 사용자 정의할 수 있는지 알아보자.
4. Circulating Supply
    초기 공급량을 생성하고 지갑에 토큰이 표시되도록 하는 방법을 알아보자.
5. Registering Accounts	
    - 악의적인 사용자의 자금 유출을 방지하기 위해 스토리지 관리 표준을 구현하고 이해하는 방법을 알아보자.
6. Transferring FTs	
    - FT를 전송하는 방법을 알아보고 핵심 표준이 제공하는 진정한 힘을 알아보자.
7. Marketplace	
    - NEAR에서 일반적인 마켓플레이스가 어떻게 운영되는지 알아보고 대체 불가능한 토큰을 사용하여 대체 불가능한 토큰을 사고 팔 수 있는 코드에 대해 자세히 알아보자.


# 1. Pre-deployed contract
- https://docs.near.org/tutorials/fts/predeployed-contract

## execute 
1. `near login`
2. `export NEARID=won999.testnet`
3. `echo $NEARID`
4. `near call ft.predeployed.examples.testnet ft_mint '{"account_id": "'$NEARID'", "amount": "10000000000000000000000"}' --accountId $NEARID`
result
```
Scheduling a call: ft.predeployed.examples.testnet.ft_mint({"account_id": "won999.testnet", "amount": "10000000000000000000000"})
Receipt: 5Jupopa7BMT4rNssLQnU8JW5RNA9NLgsfsHNGFumkHUd
        Log [ft.predeployed.examples.testnet]: EVENT_JSON:{"standard":"nep141","version":"1.0.0","event":"ft_mint","data":[{"owner_id":"won999.testnet","amount":"10000000000000000000000","memo":"FTs Minted"}]}
Transaction Id 8X18wm2Ka6m8RFGEEBrkcQD6fbN2FvBZgQ8Yu5gykiPY
Open the explorer for more info: https://testnet.nearblocks.io/txns/8X18wm2Ka6m8RFGEEBrkcQD6fbN2FvBZgQ8Yu5gykiPY
```
5. `near view ft.predeployed.examples.testnet ft_balance_of '{"account_id": "'$NEARID'"}'`
result 
```
View call: ft.predeployed.examples.testnet.ft_balance_of({"account_id": "won999.testnet"})
'10000000000000000000000'
```


# 2. Contract architecture	
- https://docs.near.org/tutorials/fts/skeleton

## source files
- `ft_core.rs`: [core(NEP-141)](https://nomicon.io/Standards/Tokens/FungibleToken/Core) 표준 구현으로 FT를 전송하고 제어하는 로직이 포함되어 있다. 
- `lib.rs`: 스마트 컨트랙트 초기화 함수를 담고 있으며 어떤 정보를 온체인에 보관할지 정한다.
- `metadata.rs`: [metadata(NEP-148)](https://nomicon.io/Standards/Tokens/FungibleToken/Metadata) 표준 구현으로 메타데이터 구조를 정의한다.
- `storage.rs`: 등록 및 저장을 위한 로직을 포함한다. 이 파일은 스토리지 관리 표준의 구현을 나타낸다.

## execute
1. ` cd 1.skeleton`
2. `./build.sh`


# 3. Defining a Token
`1.skeleton` 뼈대 -> 완성된 코드 `2.define-a-token`
- FT란? 대체가능한 토큰. 나눌 수 있지만 고유하지 않은 교환 가능한 자산이다. 

## FT 정의하기
`metadata.rs`파일에서 시작한다. [NEP-141 표준](https://nomicon.io/Standards/Tokens/FungibleToken/Core#metadata)을 토대로 FT를 작성한다. 
1. `metadata.rs` metadata 형식을 맞춘다. 
2. `lib.rs` contract 구조체에 metadata를 포함한다.
3. `lib.rs - new()`contract 초기화 함수에 metadata를 생성한다. 
4. `lib.rs - new_default_meta()` contract 여러 번 배포할 때 metadata를 매번 전달하면 불편하므로 default meatdata 집합으로 컨트랙트 초기화하는 함수를 만든다. 

## near-cli로 FT contract 배포해서 사용하기 
1. `near login`
2. `export FT_CONTRACT_ID="YOUR_ACCOUNT_NAME"`, ex) export FT_CONTRACT_ID=won999.testnet
3. `echo $FT_CONTRACT_ID`
4. `near deploy <account-id> <wasm-file>`,  ex) near deploy $FT_CONTRACT_ID out/contract.wasm
result
```
Deploying contract out/contract.wasm in won999.testnet
Done deploying to won999.testnet
Transaction Id Bm4pWhrQthw5uzBfYuDG4VWwBhFon4AfKrY1TBAihkB9
Open the explorer for more info: https://testnet.nearblocks.io/txns/Bm4pWhrQthw5uzBfYuDG4VWwBhFon4AfKrY1TBAihkB9
```
5. `near call $FT_CONTRACT_ID new_default_meta '{"owner_id": "'$FT_CONTRACT_ID'", "total_supply": "0"}' --accountId $FT_CONTRACT_ID`
result
```
Scheduling a call: won999.testnet.new_default_meta({"owner_id": "won999.testnet", "total_supply": "0"})
Transaction Id 9E1DJkGgPRmybiq9NYUocrffVtDjoJsJU5CK8XMR6dLm
Open the explorer for more info: https://testnet.nearblocks.io/txns/9E1DJkGgPRmybiq9NYUocrffVtDjoJsJU5CK8XMR6dLm
```
6. `near view $FT_CONTRACT_ID ft_metadata`
result
```
View call: won999.testnet.ft_metadata()
{
  spec: 'ft-1.0.0',
  name: 'Team Token FT Tutorial',
  symbol: 'gtNEAR',
  icon: 'data:image/jpeg;base64, ... 생략',
  reference: null,
  reference_hash: null,
  decimals: 24
}
```


# 4. Circulating Supply
https://docs.near.org/ko/tutorials/fts/circulating-supply

컨트랙트를 작성할 때 이를 구현할 수 있는 다양한 방법이 있다. 몇 가지 예는 다음과 같다.
- 시작 총 공급량을 지정하고 일련의 매개변수에 따라 분배하기 (Benji는 20%, Josh는 2.5%, 나머지는 Mike에게 할당).
- 모든 사람이 최대 X 개의 토큰을 청구할 수 있는 선착순 서비스 풀 만들기
- 주문형 토큰을 생성하여 지정된 상한선까지 순환 공급이 꾸준히 증가시키기 

간단한 방법은 총 공급량을 지정하는 것이다. 

## 컨트랙트 수정하기 
`1.skeleton` 뼈대 -> `2.define-a-token` -> `3.initial-supply` -> 완성된 코드 `4.storage`

이 로직을 구현하려면 스마트 컨트랙트에서 두 가지 사항을 추적해야 한다.
- 소유한 토큰 수와 계정의 매핑
- 토큰의 총 공급량

1. `lib.rs` contract 구조체에 accounts, total_supply를 추가한다.
2. `src/internal.rs 생성` 토큰을 소유자의 계정에 입금하는 기능을 추가하기 위해 금액과 account ID를 받아 입금 로직을 수행하는 도우미 함수를 만든다. `pub(crate) fn internal_deposit(&mut self, account_id: &AccountId, amount: Balance)`
3. `lib.rs`에 가서 `internal` 모듈을 추가하고 초기화 함수(`new`)에 total_supply, accounts를 추가한다. 
4. `ft_core.rs` 해당 모듈로 가서 `ft_total_supply`, `ft_balance_of`를 사용하여 공급량을 가져오면 된다. 
5. 1~4까지 초기 토큰 공급을 생성하고 주어진 계정의 잔고를 쿼리하는 데 필요한 것들 모두 완료!
6. `src/event.rs 생성` 컨트랙트가 FT contract이고 contract owner가 해당 ft 토큰을 소유하고 있음을 지갑(사용자)이 알 수 있게 하기 위해 `이벤트`를 생성해줘야 한다. transfer, mint 이벤트는 표준이다. 
7. `lib.rs`에 가서 `event` 모듈을 추가하고 초기화 함수(`new`)에 가서 발행한 FTMint 이벤트 로그를 넣는다. 

## near-cli로 FT contract 배포해서 테스트하기 
1. `near create-account events.$FT_CONTRACT_ID --masterAccount $FT_CONTRACT_ID --initialBalance 25`
result
```
> near create-account events.$FT_CONTRACT_ID --masterAccount $FT_CONTRACT_ID --initialBalance 25
Creating account events.won999.testnet using won999.testnet
Transaction Id CCvcdbXckfSez1y7vk11yYJLyKJs6yzdKPBdLY8sx6P3
Open the explorer for more info: https://testnet.nearblocks.io/txns/CCvcdbXckfSez1y7vk11yYJLyKJs6yzdKPBdLY8sx6P3
Storing credentials for account: events.won999.testnet (network: testnet)
Saving key to '~/.near-credentials/testnet/events.won999.testnet.json'
```
2. `export EVENTS_FT_CONTRACT_ID=events.$FT_CONTRACT_ID`
3. `cd 1.skeleton && ./build.sh && cd .. && near deploy $EVENTS_FT_CONTRACT_ID out/contract.wasm`
result
```
Deploying contract out/contract.wasm in events.won999.testnet
Done deploying to events.won999.testnet
Transaction Id 5RTEn2Nfw5mBBKe2RqPTxeZxrAPXDcb3QLkQMyzwPuTN
Open the explorer for more info: https://testnet.nearblocks.io/txns/5RTEn2Nfw5mBBKe2RqPTxeZxrAPXDcb3QLkQMyzwPuTN
```
4. ft_contract 초기화(총 공급량 생성). `near call $EVENTS_FT_CONTRACT_ID new_default_meta '{"owner_id": "'$EVENTS_FT_CONTRACT_ID'", "total_supply": "1000000000000000000000000000"}' --accountId $EVENTS_FT_CONTRACT_ID`
result
```
Scheduling a call: events.won999.testnet.new_default_meta({"owner_id": "events.won999.testnet", "total_supply": "1000000000000000000000000000"})
Receipt: GoPwtBrtLHXGkVm7udyjcCjBFKSugAP1PUw6tMPA34c2
        Log [events.won999.testnet]: EVENT_JSON:{"standard":"nep141","version":"1.0.0","event":"ft_mint","data":[{"owner_id":"events.won999.testnet","amount":"1000000000000000000000000000","memo":"Initial token supply is minted"}]}
Transaction Id FSUvBehk32zkjyPjjNonZ5Kvxjq7R1xwtnX1cRs3igag
Open the explorer for more info: https://testnet.nearblocks.io/txns/FSUvBehk32zkjyPjjNonZ5Kvxjq7R1xwtnX1cRs3igag
```
5. 공급량 정보 쿼리. `near view $EVENTS_FT_CONTRACT_ID ft_total_supply`
result
```
View call: events.won999.testnet.ft_total_supply()
'1000000000000000000000000000'
```
6. 다음 함수 또한 공급량 정보와 일치해야 한다. `near view $EVENTS_FT_CONTRACT_ID ft_balance_of '{"account_id": "'$EVENTS_FT_CONTRACT_ID'"}'`
result
```
View call: events.won999.testnet.ft_balance_of({"account_id": "events.won999.testnet"})
'1000000000000000000000000000'
```
7. 다른 계정의 잔고를 쿼리하면 0이 나와야한다. `near view $EVENTS_FT_CONTRACT_ID ft_balance_of '{"account_id": "benjiman.testnet"}'`
result
```
View call: events.won999.testnet.ft_balance_of({"account_id": "benjiman.testnet"})
'0'
```


# 5. Registering Accounts	
새로운 사람이 대체 가능한 토큰(FT)을 받을 때마다 컨트랙트의 accounts 조회 맵에 추가된다. FT 발급이 쉽게 짜여진 컨트랙트인 경우 모든 자금을 "탈취"당하는 등 시스템이 악용될 수 있다. 때문에 사용자가 사용하는 바이트에 대해 요금을 청구하는 방법이 모든 컨트랙트에서 작동하도록 표준화되어야 한다. 

표준은 다음과 같다.
- `storage_deposit`: 사용자가 일정량의 스토리지를 컨트랙트에 예치할 수 있다. 사용자가 초과된 금액을 예지하면, 초과한 $NEAR는 환불된다.
- `storage_balance_of`: 주어진 사용자가 지불한 스토리지를 쿼리한다.
- `storage_balance_bounds`: 주어진 컨트랙트와 상호 작용하는 데 필요한 최소 및 최대 스토리지 양을 쿼리한다.

이러한 함수 개요를 통해, 흐름이 다음과 같다고 가정할 수 있다.
- 사용자가 컨트랙트에 존재하지 않는 경우, 사용하는 바이트를 충당하기 위해 일부 스토리지를 예치해야 한다.
- 사용자가 `storage_deposit` 함수를 통해 $NEAR를 입금하면, 컨트랙트와 자유롭게 상호 작용할 수 있다.

보증금이 얼마인지 스스로에게 물어볼 수 있다. 이 정보를 얻는 방법에는 두 가지가 있다.
- 모든 개별 사용자가 `storage_deposit` 함수에서 차지하는 바이트를 맵에 삽입하고, 바이트를 측정한 다음, 나중에 accounts 맵에서 제거하여 동적으로 계산한다.
- 컨트랙트를 초기화할 때, 가능한 한 가장 큰 계정 ID를 삽입하기 위한 바이트를 계산하고, 모든 사용자에게 동일한 금액을 청구한다.

## 컨트랙트 수정하기 
1. `lib.rs` contract 구조체에 `bytes_for_longest_account_id`를 추가한다. 
2. `internal.rs` 초기화 함수(`new`)에서 수행될 금액을 계산하는 함수(`measure_bytes_for_longest_account_id`)를 추가한다. 
3. `internal.rs` 스토리지 비용을 지불한 후 계정을 등록하는 함수(`internal_register_account`)를 추가한다. 
4. `internal.rs` 사용자가 아직 존재하지 않는 경우, 사용자 정의 메시지로 패닉하는 함수(`internal_unwrap_balance_of`)를 추가한다.
5. 초기 공급량을 할 때 사용했던 함수(`internal_deposit`)에 `internal_unwrap_balance_of`함수를 통해 balance를 체크하는 로직을 재활용할 수 있다. 
6. `lib.rs`에서 초기화 함수(`new`)에서 수행될 금액을 계산하는 함수와 스토리지 비용 지불 후 계정 등록한 함수를 추가한다.
7. `storage.rs` 이젠 스토리지 표준을 구현하자. 
    1. 주어진 컨트랙트와 상호 작용하는 데 필요한 최소 및 최대 스토리지 양을 쿼리하는 `storage_balance_bounds`를 작성한다. 
    2. 지정된 사용자가 지불한 스토리지에 대해 쿼리하는 `storage_balance_of`를 작성한다.
    3. 사용자가 일정량의 스토리지를 컨트랙트에 예치할 수 있다. 사용자가 초과된 보증금을 예치하면, 초과 $NEAR 액수에 대해 환불을 진행하는 `storage_deposit` 함수를 작성한다. 

## near-cli로 FT contract 배포해서 테스트하기 
1. `near create-account storage.$FT_CONTRACT_ID --masterAccount $FT_CONTRACT_ID --initialBalance 25`
result
```
Creating account storage.won999.testnet using won999.testnet
Transaction Id Ghei25GWqfwxcCVtjeEJopmqPUkyLiVKDqkVMw1u8y2y
Open the explorer for more info: https://testnet.nearblocks.io/txns/Ghei25GWqfwxcCVtjeEJopmqPUkyLiVKDqkVMw1u8y2y
Storing credentials for account: storage.won999.testnet (network: testnet)
Saving key to '~/.near-credentials/testnet/storage.won999.testnet.json'
```
2. `export STORAGE_FT_CONTRACT_ID=storage.$FT_CONTRACT_ID`
3. `cd 1.skeleton && ./build.sh && cd .. && near deploy $STORAGE_FT_CONTRACT_ID out/contract.wasm`
result
```
Deploying contract out/contract.wasm in storage.won999.testnet
Done deploying to storage.won999.testnet
Transaction Id vxR4LtADKZpTJ6qFzjK8GyrsAHBPnQ1PbiXQANRNjDD
Open the explorer for more info: https://testnet.nearblocks.io/txns/vxR4LtADKZpTJ6qFzjK8GyrsAHBPnQ1PbiXQANRNjDD
```
4. 컨트랙트 초기화. `near call $STORAGE_FT_CONTRACT_ID new_default_meta '{"owner_id": "'$STORAGE_FT_CONTRACT_ID'", "total_supply": "1000000000000000000000000000"}' --accountId $STORAGE_FT_CONTRACT_ID`
result
```
Scheduling a call: storage.won999.testnet.new_default_meta({"owner_id": "storage.won999.testnet", "total_supply": "1000000000000000000000000000"})
Receipt: FEQXuJAy2nFs2jMHGSzN78iStogEhbBwA4V9CLpPMnxp
        Log [storage.won999.testnet]: EVENT_JSON:{"standard":"nep141","version":"1.0.0","event":"ft_mint","data":[{"owner_id":"storage.won999.testnet","amount":"1000000000000000000000000000","memo":"Initial token supply is minted"}]}
Transaction Id 8mX8YuMATkGjLodbHGjLE9QNT42rGyDfdENqicjgVnU6
Open the explorer for more info: https://testnet.nearblocks.io/txns/8mX8YuMATkGjLodbHGjLE9QNT42rGyDfdENqicjgVnU6
```

5. 총 금액은 대략 등록에 0.00125 $NEAR가 든다. 소유자가 지불한 스토리지 쿼리해보자. `near view $STORAGE_FT_CONTRACT_ID storage_balance_of '{"account_id": "'$STORAGE_FT_CONTRACT_ID'"}'`
result
```
View call: storage.won999.testnet.storage_balance_of({"account_id": "storage.won999.testnet"})
{ total: '1250000000000000000000', available: '0' }
```
6. 컨트랙트와 상호 작용하는 데 필요한 스토리지 잔액 쿼리해보기. `near view $STORAGE_FT_CONTRACT_ID storage_balance_bounds`
result
```
View call: storage.won999.testnet.storage_balance_bounds()
{ min: '1250000000000000000000', max: '1250000000000000000000' }
```


# 6. Transferring FTs	
사용자가 FT을 전송하고 받을 수 있도록 스마트 컨트랙트를 확장하려고 한다.


단순 전송 로직(`ft_transfer`)은 간단하다. Benji가 Mike에게 100 개의 대체 가능한 토큰을 전송하려고 한다고 가정해 보자. 컨트랙트는 다음과 같은 몇 가지 작업을 수행해야 한다.
1. Benji가 최소 100개의 토큰을 소유하고 있는지 확인한다.
2. Benji가 함수를 호출하는지 확인한다.
3. Mike가 컨트랙트에 등록되어 있는지 확인한다.
4. Benji의 계정에서 토큰 100개를 가져온다.
5. Mike의 계정에 100개의 토큰을 넣는다.

크로스 컨트랙트 호출(`ft_transfer_call`)은 조금 더 복잡하다. 계정은 서비스 수행을 위해 FT를 스마트 컨트랙트로 전송하려고 한다고 해보자. 전통적인 접근 방식은 서비스를 수행한 다음 두 개의 개별 트랜잭션에서 토큰을 요청하는 것이다. FT가 수신자에게 전송되고, 동일한 트랜잭션에서 수신자의 컨트랙트에 있는 메서드도 호출된다. 이를 단일 트랜잭션에 "전송 및 호출" 워크플로우를 도입하면 프로세스가 크게 개선될 수 있다.


## 컨트랙트 수정하기 
1. `ft_core.rs` ft 토큰을 전송하는 `ft_transfer`를 만든다. 
    1. `assert_one_yocto()`: 이 메서드는 사용자가 호출에 정확히 하나의 yoctoNEAR를 연결했는지 확인한다. 함수에 입금이 필요한 경우, 해당 트랜잭션에 서명하려면 전체 액세스 키가 필요하다. 이는 하나의 yoctoNEAR 보증금 요구 사항을 추가함으로써, 본질적으로 사용자가 전체 액세스 키로 트랜잭션에 서명하도록 강제할 수 있다. 전송 함수는 잠재적으로 매우 귀중한 자산을 전송하므로, 함수를 호출하는 사람이 전체 액세스 키를 가지고 있는지 확인해야 한다. 
    2. `internal_transfer`: 이것은 NFT를 전송하는 데 필요한 모든 로직을 수행한다. 
2. `internal.rs`로 이동한다. `internal_transfer` 함수는 (sender, receiver, amount, memo) 매개변수가 필요하다. 
    1. 기존에 구현한 `intenal_deposit`과 비슷한 개념인 `internal_withdraw`를 구현한다.
    2. `intenal_deposit`, `internal_withdraw` 두 함수를 통해 `internal_transfer`를 만들 수 있다. 
3. `ft_core.rs` 2번에서 구현한 함수를 사용하는 `ft_transfer_call`를 만든다. 
    1. 호출자가 보안을 위해 정확히 1 yocto를 첨부했는지 확인한다.
    2. 방금 작성한 `internal_transfer` 토큰을 사용하여 토큰을 전송한다.
    3. `receiver_id`의 컨트랙트에서 `ft_on_transfer` 메서드를 호출하는 Promise를 만든다.
    4. Promise 실행이 끝나면 `ft_resolve_transfer` 함수가 호출된다.
- [cross 컨트랙트 호출](https://docs.near.org/ko/develop/contracts/crosscontract)할 때 흔히 사용되는 방식이다.
- `ft_on_transfer`를 호출하면, 컨트랙트에서 원래 보낸 사람에게 환불해야 하는 토큰 수를 반환한다. 중요한 이유는 다음과 같다. 
        1. 수신자에게 너무 많은 FT를 보내서, 컨트랙트에서 초과분을 환불하려는 경우이다.
        2. 로직 패닉이 발생하면, 모든 토큰을 보낸 사람에게 다시 환불해야 한다.
        - 두 로직은 `ft_resolve_transfer`에서 처리된다.

## near-cli로 FT contract 배포해서 테스트하기 
1. `near create-account transfer.$FT_CONTRACT_ID --masterAccount $FT_CONTRACT_ID --initialBalance 25`
result
```
Creating account transfer.won999.testnet using won999.testnet
Transaction Id B1hoBsVTXKxEGRBbpjH4vgzZXvrvtohUfUjBfRzXXLUz
Open the explorer for more info: https://testnet.nearblocks.io/txns/B1hoBsVTXKxEGRBbpjH4vgzZXvrvtohUfUjBfRzXXLUz
Storing credentials for account: transfer.won999.testnet (network: testnet)
Saving key to '~/.near-credentials/testnet/transfer.won999.testnet.json'
```
2. `export TRANSFER_FT_CONTRACT_ID=transfer.$FT_CONTRACT_ID`
3. `cd 1.skeleton && ./build.sh && cd .. && near deploy $TRANSFER_FT_CONTRACT_ID out/contract.wasm`
result
```
Deploying contract out/contract.wasm in transfer.won999.testnet
Done deploying to transfer.won999.testnet
Transaction Id HrLeyWU4NmvAFbCQf9bfCKyeLfAyFS8DC5Q1ebYDnSQA
Open the explorer for more info: https://testnet.nearblocks.io/txns/HrLeyWU4NmvAFbCQf9bfCKyeLfAyFS8DC5Q1ebYDnSQA
```
4. 컨트랙트 초기화. `near call $TRANSFER_FT_CONTRACT_ID new_default_meta '{"owner_id": "'$TRANSFER_FT_CONTRACT_ID'", "total_supply": "1000000000000000000000000000"}' --accountId $TRANSFER_FT_CONTRACT_ID`
result
```
Scheduling a call: transfer.won999.testnet.new_default_meta({"owner_id": "transfer.won999.testnet", "total_supply": "1000000000000000000000000000"})
Receipt: 8M8gRNPnv2yuuNcwVtWHqEP1eWhY8n4ri5g3QXGuGczR
        Log [transfer.won999.testnet]: EVENT_JSON:{"standard":"nep141","version":"1.0.0","event":"ft_mint","data":[{"owner_id":"transfer.won999.testnet","amount":"1000000000000000000000000000","memo":"Initial token supply is minted"}]}
Transaction Id 8rKVs81NTAAD3kVRgN8sHsfoM2yB8KuErRpe7nzpmjsZ
Open the explorer for more info: https://testnet.nearblocks.io/txns/8rKVs81NTAAD3kVRgN8sHsfoM2yB8KuErRpe7nzpmjsZ
```
5. FT 소유하고 있는지 확인하기. `near view $TRANSFER_FT_CONTRACT_ID ft_balance_of '{"account_id": "'$TRANSFER_FT_CONTRACT_ID'"}'`
result
```
View call: transfer.won999.testnet.ft_balance_of({"account_id": "transfer.won999.testnet"})
'1000000000000000000000000000'
```

### 전송 함수 테스트 ft_transfer
1. benjamin 테스트 계정 등록. `near call $TRANSFER_FT_CONTRACT_ID storage_deposit '{"account_id": "benjiman.testnet"}' --accountId $TRANSFER_FT_CONTRACT_ID --amount 0.01`
result
```
Scheduling a call: transfer.won999.testnet.storage_deposit({"account_id": "benjiman.testnet"}) with attached 0.01 NEAR
Transaction Id D1tx6XQ2cokMSW6yjvZH5eFv31PSaFLqzKL9fC3YjJoS
Open the explorer for more info: https://testnet.nearblocks.io/txns/D1tx6XQ2cokMSW6yjvZH5eFv31PSaFLqzKL9fC3YjJoS
{ total: '1250000000000000000000', available: '0' }
```
2. 다음 명령을 통해 FT 전송. `near call $TRANSFER_FT_CONTRACT_ID ft_transfer '{"receiver_id": "benjiman.testnet", "amount": "1000000000000000000000000", "memo": "Go Team :)"}' --accountId $TRANSFER_FT_CONTRACT_ID --depositYocto 1`
result
```
Scheduling a call: transfer.won999.testnet.ft_transfer({"receiver_id": "benjiman.testnet", "amount": "1000000000000000000000000", "memo": "Go Team :)"}) with attached 0.000000000000000000000001 NEAR
Receipt: 5cLpXHCxwn7JvLqFX2DzeJZ4wqtMGEuRhts9CW28SNoK
        Log [transfer.won999.testnet]: EVENT_JSON:{"standard":"nep141","version":"1.0.0","event":"ft_transfer","data":[{"old_owner_id":"transfer.won999.testnet","new_owner_id":"benjiman.testnet","amount":"1000000000000000000000000","memo":"Go Team :)"}]}
Transaction Id 3VYkpmJRDA6XmgTsfdTLhdbtCtqvsLaK53LHwaZtUtD4
Open the explorer for more info: https://testnet.nearblocks.io/txns/3VYkpmJRDA6XmgTsfdTLhdbtCtqvsLaK53LHwaZtUtD4
```
3. 소유자 잔액은 999이어야 한다. `near view $TRANSFER_FT_CONTRACT_ID ft_balance_of '{"account_id": "'$TRANSFER_FT_CONTRACT_ID'"}'`
result
```
View call: transfer.won999.testnet.ft_balance_of({"account_id": "transfer.won999.testnet"})
'999000000000000000000000000'
```
4. Benjamin 잔액은 1이어야 한다. `near view $TRANSFER_FT_CONTRACT_ID ft_balance_of '{"account_id": "benjiman.testnet"}'`
result
```
View call: transfer.won999.testnet.ft_balance_of({"account_id": "benjiman.testnet"})
'1000000000000000000000000'
```
5. `near view $TRANSFER_FT_CONTRACT_ID ft_total_supply`

### 전송 호출 함수 테스트 ft_transfer_call
`ft_on_transfer` 함수를 구현하지 않은 수신자에게 토큰을 전송하려고 하면, 컨트랙트가 패닉 상태가 되고, FT가 환불되어야 한다. 이 기능을 테스트해보자.

1. 먼저 no_contract 계정을 만든다. `near call $TRANSFER_FT_CONTRACT_ID storage_deposit '{"account_id": "no-contract.testnet"}' --accountId $TRANSFER_FT_CONTRACT_ID --amount 0.01`
result
```
Scheduling a call: transfer.won999.testnet.storage_deposit({"account_id": "no-contract.testnet"}) with attached 0.01 NEAR
Transaction Id FoVM4nu1LaRh469KV4gJycUhUtjXjomZFh8M3vWcLsom
Open the explorer for more info: https://testnet.nearblocks.io/txns/FoVM4nu1LaRh469KV4gJycUhUtjXjomZFh8M3vWcLsom
{ total: '1250000000000000000000', available: '0' }
```
2. 반환되어야할 콜을 날려보자. `near call $TRANSFER_FT_CONTRACT_ID ft_transfer_call '{"receiver_id": "no-contract.testnet", "amount": "1000000000000000000000000", "msg": "foo"}' --accountId $TRANSFER_FT_CONTRACT_ID --depositYocto 1 --gas 200000000000000`
result
```
Scheduling a call: transfer.won999.testnet.ft_transfer_call({"receiver_id": "no-contract.testnet", "amount": "1000000000000000000000000", "msg": "foo"}) with attached 0.000000000000000000000001 NEAR
Receipts: EBjKBfTY4QCispwihBYZvCR5fHZNrCEcmVU4qwjFzYQy, AucztqZyDhZRpi85hGuVp5uvV6xjo3V61czu6ucoCbyV, 7BUKLCPiZ3e17m7WdJYqnwJ6DjRd3nbn5k8yJdeWZhAs
        Log [transfer.won999.testnet]: EVENT_JSON:{"standard":"nep141","version":"1.0.0","event":"ft_transfer","data":[{"old_owner_id":"transfer.won999.testnet","new_owner_id":"no-contract.testnet","amount":"1000000000000000000000000"}]}
Receipt: 4pSgHygTvBmYW1pJWsvscG1rLAt8oUrHrEqWui7EyZ1A
        Failure [transfer.won999.testnet]: Error: {"index":0,"kind":{"index":0,"kind":{"FunctionCallError":{"CompilationError":{"CodeDoesNotExist":{"account_id":"no-contract.testnet"}}}}}}
Receipt: G8Kw9LsCT8HwvsVQyYV6dg1bJZZKi7xK54umvEKJ2Ycd
        Log [transfer.won999.testnet]: EVENT_JSON:{"standard":"nep141","version":"1.0.0","event":"ft_transfer","data":[{"old_owner_id":"no-contract.testnet","new_owner_id":"transfer.won999.testnet","amount":"1000000000000000000000000","memo":"Refund"}]}
Transaction Id 4zGK1MmhmLsAnN4xU9Hn2swEDkD9kqjhuhjVZsA47Adq
Open the explorer for more info: https://testnet.nearblocks.io/txns/4zGK1MmhmLsAnN4xU9Hn2swEDkD9kqjhuhjVZsA47Adq
'0'
```
3. no-contract의 잔고는 여전히 0임을 확인할 수 있다. `near view $TRANSFER_FT_CONTRACT_ID ft_balance_of '{"account_id": "no-contract.testnet"}'`
result
```
View call: transfer.won999.testnet.ft_balance_of({"account_id": "no-contract.testnet"})
'0'
```