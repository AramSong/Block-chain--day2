180803

### 지갑

개인키를 담는 곳. 구조화된 파일이나 간단한 데이터베이스 형태로 구현. 비트코인 지갑은 비트코인이 아닌 키를 담고 있다. 각 사용자들은 키가 들어 있는 지갑을 보유하고 있다. 지갑에는 개인/공개키 쌍이 담겨 있다. 사용자들은 키를 이용해서 거래에 서명함으로써 자신들이 거래 출력값(비트코인)을 소유하고 있음을 입증한다.

* 비결정적(무작위)지갑

무작위로 생성된 개인키를 모아 놓는 장소. 관리하거나 백업, 데이터를 불러오기 너무 복잡함. 무작위로 뽑은 키들의 단점은 한번 생성된 후 에는 전부 복사본을 보관해야하 함. 이는 지갑이 자주 백업되야한다. 

* 결정적(종자)지갑

일방 해시 함수를 이용해서 공통 종자(common seed)에서 얻은 개인키들이 담겨 있다. 결정적 지갑 내에서는 seed만 있으면 추출키 전부를 복원할 수 있기 때문에 특정 시기에 백업을 한 번만 해도 된다. 또한 export와 import도 종자만 있으면 가능하기 때문에 다른 종류의 지갑 사이에서도 사용자들의 키 전부가 쉽게 이동할 수 있다.

* 연상기호 코드워드

결정적 지갑을 얻기 위해 종자로 이용한 난수를 표현하는(인코딩하는) 영어 단어열이다. 

* HD지갑 :(Hardened Derivation)단절유도법 이라고 불리는 대안 유도 함수를 사용해서 부모 공개키와 자식 체인코드 간 관계를 끊어버린다. 단절 유도 함수는 부모 공개키를 사용하지 않고 부모 개인키를 사용해서 자식 체인 코드를 만든다.

* BIP0044

  m / purpose' / coin_type'/ account' / change / address_index

   * `purpose` : 첫번째 단계.항상 44로 맞추어져있다.

   * `coin_type` : 두번째 단계.암호화폐 동전의 유형 명시

  * `account` : 세번째 단계.사용자들이 회계나 조직적인 용도 때문에 자신들의 지갑을 논리적인 하위 계좌로 세분화할 수 있돌고 해줌.

  * `change` : 네번째 단계.HD지갑이 두 개의 서브트리를 보유하고 있다. 하나는 수신 주소를 생성하기 위한 것. 하나는 잔액 주소를 생성하기 위한것. 세번째 단계가 단절 유도법을 사용하는 반면 네번째 단계에서는 정규 유도법을 사용한다.이를 통해 트리의 네번째 단계가 보안이 약한 환경에서 확장 공개키용 데이터를 전송할 수 있다.

  * `address_index` : 네번쨰 단계의 자식으로써 HD지갑으로 사용가능한 주소를 얻은 후 마지막 단계다.

     

* BIP0038 (암호화된 개인키)

개인키를 안전하게 백업매체에 저장하고 지갑 간 전송을 시행하며 노출될 수 있는 어떠한 조건에서도 비밀이 유지될 수 있도록 하기 위해서 패스프레이즈를 이용해 개인키를 암호화하고 Base58Check로 개인키를 인코딩하는 데 필요한 공동 표준을 제안한다.

### 거래

비트코인 시스템 내에 있는 참가자들 간 가치를 전송하는 행위를 인코딩한 데이터 구조. 각 거래는 전 세계적인 복식부기 장부에 들어있는 공개된 항목이다.

* 거래의 수명주기 

거래가 생성되는 단계부터 시작한다.

1. 생성된 거래에서 해당 거래가 참조하는 금액을 소비하기 위해서는 승인을 의미하는 서명을 한 건 이상 받아야 한다. 
2. 비트코인 네트워크 상에 해당 거래를 알리면, 각 네트워크 노드(참가자)가 해당 거래를 검증하고 네트워크 내에 있는 노드 전부에게 해당 거래가 도착할 때까지 거래를 계속 전파한다.
3. 해당 거래가 채굴 노드에 의해서 검증된 후 블록체인에 기록되어 있는 거래들로 구성된 블록내에 포함된다.
4. 생성되는 블록들에 의해 승인을 받고 나면 해당 거래는 비트코인 장부에 영구적으로 기록되며 모든 참가자들에게 유효하다고 인정받는다.
5. 해당 거래를 통해 새로운 소유주에게 할당된 돈은 새로운 거래소에서 소비가능
6. 이를 통해 소유권 사슬이 연장되고 거래의 수명주기가 다시 시작.

