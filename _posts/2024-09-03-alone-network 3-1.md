---
title: "[혼공네] 3-1. LAN을 넘어서는 네트워크 계층"
tags: [study, alone-network]
author: 상 한규
---
- 데이터 링크 계층의 한계
    1. 물리 계층과 데이터 링크 계층만으로 다른 네트워크까지의 도달 경로를 파악하기 어렵다.
    통신을 빠르게 주고받기 위하여 최적의 경로를 결정하는 라우팅 기법을 사용한다. 이 때 물리 계층과 데이터 링크 계층의 장비로는 라우팅이 불가능하며, 라우터라는 장비를 사용한다.
    2. MAC 주소 만으로는 모든 네트워크에 속한 호스트의 위치를 특정하기 어렵다.
    MAC 주소는 수신인의 역할을 하며, 수신지를 알기 위해서 IP 주소가 필요하다. MAC은 물리 주소라고 부르기도 하며, IP 주소는 논리 주소라고 부르기도 한다. 또한 MAC은 일반적으로 NIC마다 할당되는 고정된 주소지만, IP는 호스트에 직접 할당이 가능하다. DHCP 프로토콜을 사용하여 자동으로 할당받거나 사용자가 직접 할당할 수 있고, 한 호스트가 복수의 IP를 가질 수도 있다.
<br><br>
- 인터넷 프로토콜 (Internet Protocol)
    - IPv4, IPv6 두 종류가 있다.
    - IP 주소는 4바이트로 표현할 수 있고, 옥텟으로 표현된다.
    - 기능
        - IP 주소 지정 : IP 주소를 바탕으로 송수신 대상을 지정하는 것
        - IP 단편화 : 전송하고자 하는 패킷의 크기가 MTU보다 클 경우 복수의 패킷으로 나누는 것
        - MTU : 한 번에 전송 가능한 IP 패킷의 최대 크기
    - IPv4
        1. 식별자 : 패킷에 할당된 번호
        2. 플래그 : 총 세 개의 비트로 구성된 필드로, 첫 번째 비트는 항상 0으로 예약된 비트다. 두 번째 비트는 DF로 단편화를 수행하지 말라는 표시를 한다. 마지막 비트는 MF로 단편화된 패킷이 더 있는지를 표시한다.
        3. 단편화 오프셋 : 패킷이 단편화되기 전에 초기 데이터에서 몇 번째로 떨어진 패킷인지 나타내주는 것
        4. TTL : 패킷의 수명. 패킷이 호스트 똔느 라우터에 한 번 전달되는 것을 홉이라고 하는데, 홉마다 TTL은 1 감소한다. 무의미한 패킷이 네트워크 상에 남아있는 것을 방지한다.
        5. 프로토콜 : 상위 계층의 프로토콜이 무엇인지를 나타내는 필드
        6. 송신지 IP주소
        7. 수신지 IP 주소
    - IPv6 → IPv4(4바이트, 2^32)의 주소가 부족하여 한계를 해결하기 위해 등장 (16바이트, 2^128)
        1. 다음 헤더 : 상위 계층의 프로토콜 혹은 확장 헤더를 가리키는 헤더.
        2. 홉 제한 : 패킷의 수명을 나타내는 필드
        3. 송신지 IP 주소
        4. 수신지 IP 주소
<br><br>
- ARP : IP 주소를 통해 MAC 주소를 알아내는 프로토콜. 동일 네트워크 내에 있는 송수신 대상의 IP 주소를 통해 MAC 주소를 알아낼 수 있다.
    - 동작과정
        1. ARP 요청 : 네트워크 내의 모든 호스트에게 브로드캐스트 메시지를 보낸다. IP 주소를 보내고 MAC 주소를 요청한다.
        2. ARP 응답 : 자신의 IP가 아닌 호스트는 무시하고, 이에 맞는 호스트가 유니캐스트 메시지를 보낸다.
        3. ARP 테이블 갱신 : ARP 테이블을 갱신 이는 일정 시간이 지나거나 임의로 삭제할 수 있다.

### IP 단편화를 피하는 방법

IP 단편화는 되도록 하지 않는 것이 좋다. 단편화가 많아질수록 패킷의 헤더들이 많아지고, 불필요한 트래픽 증가와 대역폭 낭비로 이어질 수 있다. 또한 이를 합치는 과정에서 부하와 성능 저하가 생길 수도 있다. 

이러한 문제를 피하기 위해서 처리 가능한 MTU 크기를 고려해야 한다. IP 단편화 없이 주고 받을 수 있는 최대 크기, 즉 경로 MTU만큼만 전송하면 된다. 이러한 경로 MTU를 구하고 단편화를 피하는 기술을 경로 MTU 발견 이라고 한다.

문제 1. ARP의 동작 과정을 세가지로 나누어 서술하시오

→ 1. ARP 요청. 2. ARP 응답. 3. ARP 테이블 갱신

문제 2. IP 단편화를 피하는 방법 은 __ MTU 라고 한다. 또한 이러한 기술을 __ MTU 발견이라고 한다. 

→ 경로