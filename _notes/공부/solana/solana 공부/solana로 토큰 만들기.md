# SOLANA로 토큰 만들기
[https://spl.solana.com/token](https://spl.solana.com/token)


# RUST 설치
solana로 작업을 하기 위하여 rust 필요
[https://rustup.rs/](https://rustup.rs/)   
위의 주소로 접속하여 `rustup-init.exe`를 클릭 혹은 curl을 사용하여 rust 설치
<img src="/assets/Pasted image 20240403133756.png">

exe 파일을 실행하면 아래와 같은 화면이 출력
<img src="/assets/Pasted image 20240403133918.png">
window visual studio 설치에 대한 내용입니다 필요하신 분은 1을 선택하시고 설치가 불필요하신 분은 3을 선택하시면 됩니다.


<img src="/assets/Pasted image 20240403135304.png">
rust 환경 설치에 대한 내용입니다.   
그냥 엔터로 넘어가시면 설치가 진행됩니다.   


# Solana Program Library 설치
solana 플랫폼 SOL 기반 지갑 sollet에서 사용되는 토큰은 SPL 토큰을 지원합니다.   
SPL은 솔라나의 Sealevel 병렬 런타임을 기반으로 하는 온체인 프로그램 콜렉션입니다.   
이더리움에서 ERC-20에 해당하는 spl-token-cli를 설치해줍니다.   
cmd창에 `cargo intall spl-token-cli`를 입력합니다.   

# Window에서 solana 설치
docs : [https://docs.solanalabs.com/cli/install](https://docs.solanalabs.com/cli/install)   
docs에서 운영체제에 맞는 명령어로 설치해주면 됩니다.   


<img src="/assets/Pasted image 20240403142803.png">
진행 당시 버전은 1.18.4였습니다. 아래의 명령어를 입력 하면 설치가 됩니다.   
`cmd /c "curl https://release.solana.com/v1.18.4/solana-install-init-x86_64-pc-windows-msvc.exe --output C:\solana-install-tmp\solana-install-init.exe --create-dirs"`    

`C:\solana-install-tmp\solana-install-init.exe v1.18.4`   
설치 후 cmd 창을 껏다가 키고 버전을 확인하면 설치가 된 것을 확인할 수 있습니다.

<img src="/assets/Pasted image 20240403142949.png">


# Solana 환경 설정
`solana config get`을 입력하여 현재 정보 확인   
<img src="/assets/Pasted image 20240403143548.png">

RPC URL을 확인하면 mainnet에 연결된 것을 알 수 있습니다.   

`solana config set --url https://api.devnet.solana.com`을 입력하여 연결된 RPC URL을 devnet으로 변경합니다.   
<img src="/assets/Pasted image 20240403143730.png">

# 키페어 생성
`solana-keygen new --outfile .config/solana/id.json`명령어를 입력 후 비밀번호를 입력하면 key 생성   
<img src="/assets/Pasted image 20240403144758.png">

# devnet airdrop
`solana config set --keypair .config/solana/id.json`명령어를 통하여 airdrop 받을 keypair를 지정
`solana airdrop 0.5 (pubkey) --url devnet`명령어를 사용하여 airdrop 실행   
pubkey keypair 생성 시 받은 pubkey입력


# token 생성
`spl-token create-token`을 실행하면 아래와 같이 address와 decimals, signature에 대한 정보가 나옵니다.    
<img src="/assets/Pasted image 20240403145536.png">

`spl-token supply (token address)`위에서 생성된 token address를 입력하여 발행량을 확인 할 수 있습니다.   
아직 mint를 하지 않아 0인 것을 알 수 있습니다.   
<img src="/assets/스크린샷 2024-04-03 145811.png">

`spl-token create-account (token address)` 
이건 왜 진행하는지 이해하지 못하였습니다.   
<img src="/assets/Pasted image 20240403145910.png">

`spl-token mint (token addree) 수량`이 명령을 실행하면 token address에 해당하는 token을 수량만큼 mint 합니다.   
<img src="/assets/Pasted image 20240403150009.png">

`spl-token balance (token address)`이 명령을 실행하면 해당 토큰의 보유량을 보여줍니다.   
<img src="/assets/Pasted image 20240403150019.png">

`spl-token accounts`이 명령어는 현재 연결된 주소가 보유하고 있는 token의 잔액을 보여줍니다.   
<img src="/assets/Pasted image 20240403150045.png">

[https://explorer.solana.com/](https://explorer.solana.com/) 주소에서 token address를 검색하면 아래와 같이 정보가 나옵니다.   

<img src="/assets/스크린샷 2024-04-03 151523.png">