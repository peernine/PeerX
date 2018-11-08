# Local Ethereum Network
세 개의 노드와 모니터가있는 로컬 Ethereum 네트워크를 만드는 일련의 Docker 이미지. 이것은 로컬 Ethereum 네트워크를 설정하고 로컬 테스트 환경을 제공하는 방법을 이해하기 위해 작성되었습니다. ** docker-compose.yml에는 편의를 위해 하드 코딩 된 암호와 개인 키가 포함되어 있으므로 생산 환경에서는 사용하지 마십시오 **

## Usage
이 네트워크를 설정하려면 Docker를 설치해야합니다. 저장소를 복제하고, 저장소 루트에서`docker-compose up`을 실행하십시오. 추가 구성없이 네트워크가 시작되고 동기화되어야합니다. 네트워크는 go-ethereum 1.18.15와 0.3.4를 사용하며 네트워크는 Ethereum Rinkeby testnet과 비슷한 권한 증명 증명을 위해 설정됩니다. clique POA에 대한 자세한 내용은 https://github.com/ethereum/EIPs/issues/225를 참조하십시오.

## The bootnode
네트워크의 노드가 bootnode로 연결 중입니다. 이 노드는 네트워크에서 기존 노드의 레지스터를 제공하기 위해 설계된 특별한 에테 눔 노드입니다. `docker-compose.yml`의`nodekeyhex` 매개 변수는 나중에 다른 노드로 전달되는`enodeID`를 유도하는데 필요합니다. 다른 노드는 bootnode를 찾을 위치를 알아야하기 때문에 IP를 고정해야하며 DNS는 지원되지 않습니다. 부트 노드는 상태 또는 마이닝 동기화에 참여하지 않습니다.

## Miners / Geth Nodes
네트워크에 참여하는 세 개의 노드가 있습니다. 상태는 그들 사이에서 동기화되며 마이닝으로 블록을 만들려고합니다. 처음에는 고정 IP 및 노드 키에서 파생 된 정보로 부트 노드에 연결합니다. 네트워크와 상호 작용하려면 RPC를 통해 연결해야합니다. geth 인스턴스를 연결하거나 Remix IDE에 연결하거나 브라우저를 web3에 연결하고 ÐApp을 빌드 할 수 있습니다.

노드의 RPC 포트는 localhost에 매핑되며 주소는 다음과 같습니다.

* [http://localhost:8545](http://localhost:8545) - geth-miner-1
* [http://localhost:8546](http://localhost:8546) - geth-miner-2
* [http://localhost:8547](http://localhost:8547) - geth-miner-3

## Swarm (/BZZ:/)
Swarm은 분산 스토리지 플랫폼이자 컨텐츠 배포 서비스로, ethereum web3 스택의 기본 기본 계층 서비스입니다. Swarm의 주요 목표는 Ethereum의 공공 기록을 충분히 분산하고 여분으로 저장하는 것입니다. 특히 덤프 코드와 데이터는 물론 블록 체인 데이터를 저장하고 배포하는 것이 좋습니다. 경제적 인면에서 볼 때 참가자들은 Ethereum이 인센티브를 받으면서 네트워크의 모든 참여자에게 이러한 서비스를 제공하기 위해 스토리지 및 대역폭 리소스를 효율적으로 풀링 할 수 있습니다. 군중의 파일은 KECCAK256 체크섬으로 표시됩니다.


## Monitoring
모니터링은 두 노드, 모니터링 백엔드 및 모니터링 프론트 엔드에 의해 제공됩니다. 백엔드는 ethereum 노드에 연결하여 메트릭을 검색합니다. 모니터링 프론트 엔드와 웹 소켓을 통해 통신합니다. 프론트 엔드는 [http : // localhost : 3000] (http : // localhost : 3000)에서 찾을 수 있습니다.


## Blockchain Explorer
블록 체인 탐색기는 별도의 컨테이너 인 geth-explorer를 통해 제공되는 간단한 node.js 웹 응용 프로그램입니다. 응용 프로그램은 web3 javascript API를 사용하여 RPC 호출을 통해 노드에서 데이터를 가져옵니다. 블록 체인 탐색기는 [http : // localhost : 8080] (http : // localhost : 8080) - geth-explorer에서 찾을 수 있습니다.