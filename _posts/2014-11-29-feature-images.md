---
title: Tutorial
layout: post
feature-img: assets/img/sample_feature_img.png
---

# 1. Node.js와 NPM 설치하기
npm의 경우는 Node Package Manager이기 때문에 node.js를 설치하면 같이 설치된다. 

[Node.js](https://nodejs.org/ko/)

---

```shell
$node -v
```

![png](/Ethereum-Development-Tutorial/assets/tutorial/nodecheck.png)


---

---

```shell
$npm -v
```

![png](/Ethereum-Development-Tutorial/assets/tutorial/npmcheck.png)

---


# 2. 개발환경
## Solidity
##### 솔리디티는 기존에 있던 언어가 아닌 이더리움의 스마트 컨트랙트를 구현하기 위해서 만들어진 이더리움 전용 언어입니다. 
##### 솔리디티는 Python, C++, Javascript같은 널리 알려진 언어와 사용법이 유사
##### EVM(Ethereum Virtual Machine)에서 구동되어 집니다.

![png](/Ethereum-Development-Tutorial/assets/tutorial/solidity.png)

## Truffle
##### Truffle은 이더리움 DApp 개발 프레임워크
##### 스마트컨트랙트(Solidity 프로그램) 작성, 컴파일, 테스트, 배포를 쉽게 할 수 있도록 지원하는 Backend Framework이다.

![png](/Ethereum-Development-Tutorial/assets/tutorial/truffle.png)

## Ganache
##### 개발 목적의 메모리 내 블록체인이다.
#####  Ganache는 가상의 계좌 10개를 제공하며 각 계좌별로 100 ETH를 제공합니다.

![png](/Ethereum-Development-Tutorial/assets/tutorial/ganache.png)


## React.js
##### Frontend Framework이다. 


![png](/Ethereum-Development-Tutorial/assets/tutorial/react.png)


## web3.js
##### web3.js 는 Ethereum Compatible JavaScript API 이다. 
##### web3.js 는 JavaScript 기반으로 Dapp 이나 서비스를 구현할 때 매우 유용
##### 실질적으로 JSON RPC API 와 함께 Ethereum 의 표준 API 
##### web3.js 는 내부적으로 HTTP 나 IPC 를 통해 JSON RPC API 를 호출하도록 되어있다.


![png](/Ethereum-Development-Tutorial/assets/tutorial/web3.png)


## Meta Mask
##### 크롬 브라우저에서 DApp을 사용할 수 있게 해주는 확장 프로그램이다.

![png](/Ethereum-Development-Tutorial/assets/tutorial/metamask.png)


# 3. 설치 및 시작
제안하는 개발환경을 기반으로 간단한 튜토리얼을 진행

```shell

# truffle 설치

$npm install -g truffle 
```
![png](/Ethereum-Development-Tutorial/assets/tutorial/truffle_init.png)

---

```shell



# 튜토리얼을 진행할 폴더를 만든다.

$mkdir ethereum_test

$cd ethereum_test
```

---

```shell



```

[여기에서 다양한 box를 확인할 수 있다.](https://truffleframework.com/boxes)
```shell
# truffle unbox react을 통해서 
# truffle에 react가 붙어있는 상태의 프로젝트를 받을 수 있다.

$truffle unbox react
```
![png](/Ethereum-Development-Tutorial/assets/tutorial/truffleunbox.png)

---


폴더에 대한 설명을 간단하게 하자면

- **contracts**(폴더) : solidity로 개발된 smart contract 파일을 저장하는 폴더
	- **Migrations.sol**(파일) : 개발한 smart contract 프로그램을 배포를 해야하는데, 이 파일은 배포를 위한 solidity 파일로써 삭제하면 안된다.  

---


- **migrations**(폴더) : 배포를 위한 스크립트 파일 폴더 smart contract 프로그램을 하나 개발할때마다 migration 파일도 이에 대응되서 하나씩 추가되는것을 나중에 확인할 수 있다.
	- **1_initial_migration.js**(파일) : Migrations.sol을 배포하기 위한 스크립트 파일

---

- **test**(폴더) : 개발된 smart contract를 테스트 하기 위한 폴더 해당 폴더에 테스트 케이스를 작성하고, truffle test 는 명령어를 통해 개발된 smart contract를 테스트 해 볼 수 있다.

---


- **truffle-config.js**(파일) : truffle 설정 파일입니다. 개발을 위한 host, port, network ID 등을 설정해 놓고 사용

---

- **client/src**(폴더) : react.js 폴더

---







```shell





# Ganache를 설치하고 실행하면 아래와 같은 화면을 볼 수 있다.
```
![png](/Ethereum-Development-Tutorial/assets/tutorial/ganache_open.png)
```shell

# 우측 상단 설정을 들어가면 아래와 같이 서버의 호스트, 포트, 네트워크 id를 설정할 수 있다.
```
![png](/Ethereum-Development-Tutorial/assets/tutorial/ganache_setting.png)



```shell


# Project에서 Ganache를 사용하기 위해서 truffle-config.js를 수정해야한다.

# Ganache 설정 화면에서 봤던  호스트, 포트, 네트워크 id를 넣어서 수정한다.

module.exports = {
    networks: {
        development: {
            host: "127.0.0.1",
            port: 7545,
            network_id: "*" // Match any network id
        }
    }
};

```

```shell
기존  truffle-config.js
```
![png](/Ethereum-Development-Tutorial/assets/tutorial/before_config.png)
```shell
수정 후  truffle-config.js
```
![png](/Ethereum-Development-Tutorial/assets/tutorial/after_config.png)


```shell





# truffle compile과 migrate을 해준다.

$truffle compile
```
![png](/Ethereum-Development-Tutorial/assets/tutorial/truffle_compile.png)
```shell

# migrations가 있다면 migrate가 안되므로 --reset을 붙인다.
$truffle migrate --reset
```
![png](/Ethereum-Development-Tutorial/assets/tutorial/truffle_migrate_clear.png)

```shell

# 가나슈를 보면 배포과정에서 이더가 소모된 것을 확인 할 수 있다.
```
![png](/Ethereum-Development-Tutorial/assets/tutorial/truffle_migrate_ganache.png)

```shell

# 이러한 에러가 보인다면 가나슈를 가동시킨 상태에서 다시 명령어를 실행하면 해결가능하다.
```
![png](/Ethereum-Development-Tutorial/assets/tutorial/truffle_migrate.png)


```shell

# 우리가 이제 배포가 끝났기 때문에 본격적으로 웹에서 간단한 테스트를 진행하고자한다.

$cd client
$npm start
```
![png](/Ethereum-Development-Tutorial/assets/tutorial/npmstart.png)

```shell

# 시작부터 에러 발생
# mkdir ./src/contracts && cp -r ../build/contracts/ ./src/contracts/

$npm start
```
![png](/Ethereum-Development-Tutorial/assets/tutorial/error1.png)