# OSI 계층 모델
OSI 7계층 모델은 `Layered Architecture`로써 **네트워크 프로토콜이 통신하는 구조를 7계층으로 나눈 참조 모델**입니다.

반드시 지켜야하는 것은 아니지만 안지키면 다른 네트워크와 통신을 하는 것을 보장할 수 없습니다.

현재 인터넷은 사실 `OSI 7계층 참조 모델`이 아닌 `TCP/IP Updated Model`을 사용하고 있습니다.

<img src="https://user-images.githubusercontent.com/53790137/151368206-e55eeac3-6243-469f-810e-24d625a04e69.png" width="400" height="300">

이름은 다르지만 계층화된 참조 모델로서 `Encapsulation` 과 `Decapsulation`을 통해 통신한다는 것은 같습니다.. 

- **Encapsulation**: 데이터를 전송하기 위해 상위 계층에서 하위 계층으로 내려오면서 **인코딩을 통해 데이터에 프로토콜 헤더를 붙여가며 캡슐화**하는 것.
- **Decapsulation**: 데이터를 수신하여 원하는 헤더의 정보를 읽기 위해 하위 계층에서 상위 계층으로 올라가면서 **디코딩을 통해 헤더를 떼어내어 읽는 것**.

## 1계층(Physical Layer)
1계층은 물리적인 연결로 컴퓨터나 **통신 장비가 서로 데이터를 주고 받을 수 있게 해주는 모듈**로써, `Encasulation`에서는 비트 데이터를 전기 신호로 바꾸어 회선으로 보내고 `Decasulation`에서는 전기 신호를 비트 데이터로 바꾸어 읽는 계층입니다. 

프로토콜의 데이터 단위는 `Bit`이고, 하드웨어로 구현되어 있습니다. 대표 장비로는 우리 컴퓨터의 **PHY칩, 리피터, 더미 허브**가 있습니다.

## 2계층 (Data Link Layer)
2계층은 **물리적으로 연결된 같은 네트워크(LAN)에 있는 여러 대의 통신 장비들이 데이터를 주고 받기 위해서 필요한 모듈**입니다.

`MAC`주소를 이용하여 통신하며 **목적지 MAC주소가 없는 프레임은 폐기(오류 제어)**합니다. 

프로토콜의 데이터 단위가 `Frame`이며, `Encapsulation`에서는 데이터에 2계층 헤더를 붙여 1계층으로 보내고 `Decasulation`에서는 디코딩하여 2계층 헤더 정보를 읽습니다. 

대표 장비로는 **랜카드, 브리지, 스위치**가 있고 **표준으로는 MAC과 LLC**가 있습니다. 

LAN에서 데이터링크 계층은 **LLC계층과 MAC 계층으로 분리**됩니다.

- **LLC 계층**
	- 데이터 링크 계층에서 상위에 있다.
	- 상위 계층에서 패킷을 가져오고 데이터를 MAC 계층으로 전달한다.
	- 소프트웨어로 구현되어 있다. (ex. NIC 네트워크 드라이버)
		- NIC 드라이버는 NIC 하드웨어와 직접 상호 작용하고 MAC 계층과 통신 장비 간에 데이터를 전달하는 소프트웨어 프로그램이다. 

 - **MAC계층**
 	- 데이터 링크 계층에서 하위에 있다. 
 	- MAC 계층은 하드웨어로 구현된다. (ex. 스위치)
 	- Encapsulation과 Decapsulation을 합니다.(프레임 구분, 주소 지정, 오류 감지)
 		- **프레임 구분** : 송신 노드와 수신 노드 간의 비트 수준 동기화 제공. 새 프레임의 시작에 대해 수신 노드에 신호
 		- **주소 지정** : 프레임에 이더넷 헤더 추가.(MAC 주소)
 		- **오류 감지** : 모든 프레임에는 프레임 내용에 대한 `Cycle Redundancy Check (CRC: 순환 중복 검사)`가 있는 트레일러가 있습니다. 이 CRC 합을 계산하고 프레임의 합과 비교하여 오류를 체크합니다.
 	- MAC(Media Access Control) 기능을 합니다. (미디어 액세스를 제어, 미디어 복구)

## 3계층 (Network Layer)
3계층은 **서로 다른 네트워크 간의 논리 주소인 `IP 주소`를 이용해서 길을 찾고(Routing) 다음의 라우터에게 데이터를 넘겨주는(forwarding) 모듈**입니다. 즉 목적지에 빠르게 도착하도록 해주는 계층입니다. 

- **Routing**: OSPF나 IGRP와 같은 Routing protocol을 사용하여 최대한 데이터를 빠르게 보낼 최적의 경로를 찾아 라우팅 테이블(또는 포워딩 테이블)을 업데이트, 유지하는 것을 의미.
- **Forwarding**: 패킷의 목적 IP와 포워딩 테이블을 참고하여 다음 라우터에게 패킷을 보내는 행위를 의미.

프로토콜의 데이터 단위는 `Packet`이며, `Enacapsulation`에서는 데이터에 3계층 헤더(IP 주소)를 붙여 2계층으로 보내고 `Decapsulation`에서는 디코딩하여 3계층 헤더 정보를 읽습니다. 

대표 장비는 **라우터**가 있고, **표준으로는 IP**가 있습니다. 

물론 우리의 컴퓨터에도 있는데 **운영체제 커널에 소프트웨어로 구현**되어 있습니다. CMD를 열어 `route print`를 입력하면 저장되어 있는 라우팅 테이블을 보여줍니다. 

3계층이 필요한 이유는 굉장히 거대한 인터넷 안에서 빠르게 목적지를 찾기 위해서는 지역 정보가 들어있는 계층형 주소인 IP주소가 있어야 필터링이 가능하기 때문입니다. 

## 4계층 (Transport Layer)
4계층은 **`Port`를 붙여 최종 도착지 컴퓨터의 프로세스에게 데이터를 도달하게 하는 모듈**입니다.

프로토콜 데이터 단위가 `Segment`이며, `Encapsulation`에서는 데이터에 4계층 헤더(Port)를 붙여 3계층으로 보내고 `Decapsulation`에서는 디코딩하여 4계층 헤더 정보를 읽습니다.

주 기능으로는 데이터를 Segment로 나누거나 재조립하는 기능(다중화)과 주소 설정, 오류 제어, 흐름 제어를 통해 종단 시스템(ent-to-end) 간에 논리적 안정과 균일한 데이터 전송 서비스를 제공합니다.

대표 장비는 **Gateway, L4 스위치**가 있고, **표준으로는 TCP, UDP**가 있습니다.

**Gateway**: 게이트웨이는 사실 개념적인 내용으로써, 서로 다른 통신망, 프로토콜을 사용하는 네트워크 간의 통신을 가능하게 해주는 출입문 역할을  한다. 역할을 수행만 할 수 있다면 어떤 장비나 소프트웨어도 게이트웨이가 될 수 있다. 라우터도 게이트웨이로 많이 사용된다.

## 5계층 (Application Layer)
5계층은 **사용자인 우리가 네트워크 자원에 접근할 수 있도록 해주는 모듈**입니다. 

프로토콜 데이터 단위가 `Message`이며 **대표적으로 HTTP, HTTPS, FTP 등**이 있습니다. 

> **우리는 프로토콜을 만들 수 있을까?**

우리는 운영체제의 Transport layer에서 제공하는 API를 활용해서 통신 가능한 프로그램을 만들 수 있습니다. 

이것을 TCP/IP 소켓 프로그래밍이라고 하는데요, 누구나 자신만의 Application layer의 인코더와 디코더, 즉 프로토콜을 만들어 사용할 수 있습니다. 
	
# 역할 정리
- **1, 2계층(Physical, Data Link Layer)** : 물리적으로 연결된 같은 네트워크 안에서의 통신을 가능하게 해줍니다.
- **3계층(Network layer)** : 패킷을 목적지 부근까지 전달할 수 있게 해주며, 인터넷을 사용할 수 있게 해주는 계층입니다. 
- **4계층(Transport layer)** : 두 프로세스 간의 안정적인 메시지 전달을 담당하는 계층입니다.
- **5계층(Application layer)** : 우리가 네트워크 자원에 접근할 수 있도록 해주는 계층입니다. 
