# Protocol(프로토콜)

## ARP 정의

- 논리적 네트워크 주소인 IP를 물리적 네트워크 주소인 MAC주소로 변환 시켜주는 프로토콜



## ARP 헤더

![img](Protocol - 복사본.assets/image1.bmp)

- Hardware Type : 네트워크 유형에 대해서 표시 되어 있습니다.

  이더넷(Ethernet)환경의 경우 값이 0x0001로 설정됩니다.

- Protocol Type : 프로토콜에 대해 표시 되어 있으며 IP 버전에 따라 달라집니다. 

  IPv4 경우 0x0800

- Hardware Length : 말그대로 하드웨어 주소 길이를 정의합니다. 

  이더넷(Ethernet)의 경우 6byte

- Protocol Length : 프로토콜의 길이를 정의합니다. IPv4의 경우 4byte

- Operation : 패킷의 유형, 요청의 경우 1 응답의 경우 2

- Sender Hardware Address : 발신자의 MAC주소

- Sender Protocol Address : 발신자의 IP주소

- Target Hardware Address : 목적지 MAC주소

- Target Hardware Address : 목적지 IP주소



## ARP 실행방식

- 질의와 응답으로 답하게 되는 방식을 가지고 있습니다. 



- Ex)

  처음 네트워크에 연결되었을때 라우터로부터 IP주소를 발급 받고 서로 MAC 주소를 교환하면서 기기의 정보를 등록.

  상대의 MAC 주소를 통해 패킷을 보내기 위해서는 IP주소 이외에도 MAC주소가 필요. 

  

  만약 'A' PC와 'B' PC가 있다고 가정.

  - 'A' PC = IP : 192.168.1.2 MAC : aa:bb:cc:dd:ee:ff

  - 'B' PC = IP : 192.168.1.3 MAC : aa:bb:cc:dd:ef:00

    

  1. 라우터는 'A', 'B' 두 PC에 각각  192.168.1.2와 192.168.1.3 IP 주소를 배정.

  2. 두 PC는 각각 고유의 MAC 주소를 가지고 있지만 아직 서로의 MAC 주소를 모르는 상태.
  3. 'A' PC가 'B' PC에게 파일을 보내야하는 상황이 되면 MAC주소가 필요.
  4. 'B'의 IP는 라우터에서 알려줄수 있지만, MAC주소는 알려줄수 없기 때문에 질의.
  5. 'A' PC는 'B' PC의 논리적 주소인 IP를 알고 있기에 MAC주소를 알게끔 브로드캐스트 통신으로 질의. 
  6. 헤더 형태로 포맷을 하여 모든 통신 기기에 질의.
  7. 모든 기기에 질의를 하고 질의를 받은 네트워크는 자신이 MAC주소를 입력한뒤 상대에게 다시 reply 패킷을 보냄. -> ARP통신방식
  8. 'A' PC의 MAC 주소 테이블에는 'B' PC의 IP주소와 MAC주소가 입력되고 'B' PC에게 패킷을 보낼 수 있음.

  

## ARP 요약

- 자신이 상대의 MAC주소를 모를때 IP주소를 통해 알기 위해서 패킷을 만듬.

- 자신의 IP와 MAC주소를 기입하고 브로드캐스트로 해당 IP주소를 가지고 있는 PC를 질의

-  질의를 받은 PC는 자신의 IP와 일치할 경우 MAC주소를 입력하여 ARP reply 패킷을 보냄.
