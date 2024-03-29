---
title: 기술 탐구 1. 블록체인과 비트코인, 어떻게 돈이 될까?
tags: [tech, block-chain]
author: 상 한규
---
# 블록체인의 이해, 비트코인을 버는 방법

이번 포스트에서는 공부한 지식을 기반으로 블록체인과 비트코인에 대해 알아보고자 한다. 

기술 탐구 중심이며, 공부한 바를 기반으로 작성하였으므로, 정확한 정보가 아닐 수 있다.

## 목차

1. [개요](#개요)

2. [블록체인과 블록](#블록체인과-블록)

    2-1. [해시(Hash)란?](#해시(hash)란)
    
    2-2. [블록의 구성](#블록의-구성)

    2-3. [블록체인의 특성](#블록체인의-특성)

3. [어떻게 블록체인으로 돈을 벌까?](#어떻게-블록체인으로-돈을-벌까)

    3-1. [채굴자의 역할](#채굴자의-역할)
    
    3-2. [작업증명의 방식](#작업증명의-방식)
    
    3-3. [네트워크의 질문](#네트워크의-질문)

    3-4. [채굴의 가능성](#채굴의-가능성)
## 개요
누구나 정보를 열람할 수 있지만, 그 누구도 정보를 수정할 수 없는 기술이 있다. 그렇기에 보안 측면에서 상당히 매력적이며, 심지어 가상 화폐로도 사용하고자하는 의견도 나온다. 바로 블록체인이다. 그렇다면 블록체인이란 어떤 기술일까?

<br>

![screenshot](/assets/images/posts/blockchain 1/1.png)

<figcaption style="text-align:center; font-size:15px; color:#808080">
블록체인과 레고블록
</figcaption>

## 블록체인과 블록
블록체인이란 마치 사슬과 같이 블록들이 모여있는 형태를 이야기한다. 쉽게 생각해보자. 블록을 레고의 한 블록이라고 생각하고, 블록체인은 레고 블록을 일렬로 위를 향하게 쭉 쌓은 것이라고 생각하면 편하다. 여기서 블록은 어떤 정보를 가지고 있는 것이며, 그리하여 블록체인은 데이터가 서로 묶여있는 데이터베이스가 되는 것이다. 즉, 현재 블록에서는 사슬처럼 연결되어 있는 이전블록의 정보를 가지고 있어야하며, 그러한 블록들은 서로 연관성을 가져, 하나의 블록의 정보가 바뀌면 모든 정보가 바뀌는 것이다. 만약 누가 임의로 레고 블록와 다른 블록이 접합되어 있는 구멍의 형태나 볼록 튀어나와있는 (구멍에 끼우는) 형태를 바꾸려고 한다면, 일렬로 쌓인 모든 레고 블록이 변해야 할 것이다. 여기서 알 수 있듯이 블록은 이전 블록와 연결되기 위해 어떠한 정보가 필요하며, 블록 자체의 정보도 필요하다. 그러한 정보가 무엇인지 알기 위해서는 '해시'('hash')라는 것에 대하여 알고 넘어가야 한다.

<br>

![screenshot](/assets/images/posts/blockchain 1/2.png)

<figcaption style="text-align:center; font-size:15px; color:#808080">
해시 함수
</figcaption>

## 해시(Hash)란?
해시란 어떠한 규칙에 의하여 하나의 정보를 다른 형태로 변경해주는 것을 뜻한다. 예를 들어, 'I am groot'라는 문장을 해시로 표현하면 '1002948a27189f9c3'등으로 나타낼 수 있다는 것이다. 단, 'I am grooz'라는 문장을 해시로 표현하면 완전히 다른 값으로 나타난다. groot에서 grooz로 한 단어가 변했지만 결과는 완전히 다른 것이다. 하지만 항상 같은 문장에서는 같은 해시로 표현되며, 이를 '결정론적'이라고 한다.

그렇다고, 해시로 표현된 것을 원래 문장으로 되돌릴 수 없다. 즉, '1002948a27189f9c3'를 넣는다고 해서 'I am groot'가 나오는 것이 아니다. 이를 '일방향'적 함수라고 하며, 이렇게 결정론적이며 일방향적인 함수를 갖는 것이 해시의 특징이다. 

## 블록의 구성
다시 블록으로 돌아가자. 블록은 자신의 정보를 해시로 가지고 있다. 즉, 외부에서 이 해시를 볼 순 있어도, 원래의 뜻이 무엇인지는 확인이 불가능하다는 것이다. 이러한 점에서 블록체인은 뛰어난 보안을 선보인다. 또한, 앞서 자신의 블록에서는 이전의 블록과 연결되는 (구멍과 같은) 무언가가 필요하다고 이야기하였다. 이러한 (구멍과 같은) 연결고리는 자신의 정보 안에 있다. 자신의 해시를 구성할 때, 블록은 이전 블록의 해시와 자신의 데이터를 결합하여 만든다. 즉, 자신의 해시에는 이전 블록의 해시 + 자신 블록의 데이터 해시로 구성되어 있는 것이다. 데이터의 경우 현실에서 사용되는 바를 예로 들면 금융권에서 누가 얼마의 돈을 누구에게 보냈는가 등의 거래내역이 포함된다. 여기서 내 데이터의 해시와 이전 해시 말고도 하나가 더 추가 되는데, 이름은 'nonce'로, 이후에 다루도록 하겠다. 이렇듯 모든 정보가 해시로 되어있어, 외부에서는 데이터의 원본은 가늠하기 어렵다. 

## 블록체인의 특성
그렇다면 이러한 기술은 어떤 점에서 보안이 뛰어나며, 사람들이 왜 신뢰를 하는 것일까? 정보들이 해시로 되어있어 외부에서 원본을 확인하기 어렵다고 하지만, 이를 제거 혹은 변경하는 등의 악용 방법은 상당히 다양하다. 여기서 블록체인의 특성을 더 살펴본다면 왜 악용이 매우 어려우며, 사람들이 신뢰하는지를 알 수 있다. 블록체인은 크게 두 가지 특성이 있다. 1. Append만 가능하며, 2. Decentralizaiton이라는 것이다. 1번의 경우 블록이 추가만 가능하다는 것이다. 블록체인으로 형성된 블록의 경우 제거할 수 없으며, 새로운 블록 추가만 가능하다. 그리하여 수정에 민감한 것들, 예를 들면 자격증이나 신분증 등의 정보들에 블록체인 기술을 적용할 수 있다는 것이다. 2번의 경우 탈중앙화이다. 탈중앙화란, 블록체인 데이터를 하나의 컴퓨터에서만 관리하는 것이 아니라 모든 컴퓨터가 관리할 수 있다는 것이다. 즉, 모든 컴퓨터가 중앙컴퓨터의 역할을 수행할 수 있다. 이는 모든 컴퓨터가 동일한 블록체인 데이터베이스 사본을 가지고 있다는 것이다. 이를 통해 어떤 정보가 진실인지 거짓인지 검증이 용이하다. 하나의 컴퓨터에서 거짓된 정보를 전달해도, 다른 컴퓨터들이 대부분 진실된 정보를 가지고 있으므로 거짓된 정보를 검증하기 쉽다. 그리하여 블록체인은 보안이 매우 뛰어나며 신뢰성이 높은 기술이다.

<br>

![screenshot](/assets/images/posts/blockchain 1/3.jpg)

<figcaption style="text-align:center; font-size:15px; color:#808080">
블록체인 채굴 / “中 비트코인 채굴자들, 전세계 해시율 66% 차지하고 있다 - 비트와이드”[웹사이트], (2021.07.05), https://www.bitwide.co.kr/news/news_view.php?uData=ZXhlTW9kZSUzRHZpZXclMjZpZHglM0QyMTAz.
</figcaption>


## 어떻게 블록체인으로 돈을 벌까?
블록체인은 외부에서 정보를 확인하기 어렵다고 설명하였다. 또한, 블록체인은 블록들이 사슬과 같은 형태로 묶인 데이터베이스라고 이야기하였다. 단, 정보를 확인할 수 있고, 블록을 사슬과 같은 형태로 묶어줄 수 있는 자가 존재한다. 이는 우리가 흔히 부르는 '채굴자'다. 

## 채굴자의 역할
채굴자는 블록체인에 들어오는 데이터를 확인하고, 블록에 데이터를 넣어서 블록체인에 보내주는 역할을 하는 사람들을 일컫는다. 즉, 채굴자들에 의해서 블록이 생성되며, 블록체인이 형성된다고 해도 과언이 아니다. 이렇게 데이터를 확인하고 블록체인에 넣어주는 것을 '작업증명'이라고 부르며, 채굴자는 작업증명을 하는 역할이다. 돈은 채굴자들이 작업증명을 하면서 발생하게 된다. 사실 돈이라고 부르기보단, 비트코인 즉, 가상화폐라고 부르는 것이 더 정확하다. 하지만, 이는 가상화폐 거래소에서 화폐와 비슷하게 쓰이므로 돈이라고 불러도 무방할 것이다. 작업증명을 통해 돈을 벌 수 있고, 이러한 행위를 하는 자를 채굴자라고 부르는데, 여기서 채굴자는 앞서 설명한 탈중앙화 특성으로 인해 모든 컴퓨터가 채굴자로 직업을 가질 수 있다. '그러면 모두 채굴을 하지, 왜 그렇지 않는가?'라는 질문을 던질 수 있는데, 이에 대한 답으로는 '채굴은 매우 힘들기 때문'이라고 답할 수 있다. 자, 그럼 가상화폐가 생성되는 원리 및 방식을 조금 더 자세히 알아보자.

<br>

![screenshot](/assets/images/posts/blockchain 1/4.jpg)

<figcaption style="text-align:center; font-size:15px; color:#808080">
작업방식 / “What is Proof-of-Work”[웹사이트], (2021.07.05), https://www.ledger.com/academy/blockchain/what-is-proof-of-work.
</figcaption>
## 작업증명의 방식
작업증명은 다음과 같은 방식으로 이루어진다. 

1. 네트워크가 채굴자에게 질문을 던짐.
2. 채굴자가 질문에 대하여 답을 함.
3. 네트워크가 답안 확인 후 블록체인 생성을 허용.
4. 채굴자가 블록체인 생성 후 네트워크에 올림.

방식의 경우 상당히 단순하다. 채굴자가 네트워크의 질문에 답하고 블록체인을 만드는 것으로 끝이 난다. 여기서 채굴자가 네트워크의 질문에 정답을 제출하고, 블록체인을 생성하여 네트워크에 올릴 때 가상화폐 즉, 'coin transaction'이 발생한다. 이것이 비트코인으로 불리는 것이며, 이를 통해 비트코인은 기존에 있는 것이 아닌, 생성된 것임을 알 수 있다. 이러한 비트코인은 처음에는 50개씩 생성이 되었으나, 4년마다 반감기를 가져, 현재는 6.25개씩 생성이 된다. 이렇게 반감기가 지날 때 마다 비트코인이 희귀해지며, 그 값이 높아질 수 있음을 예측할 수 있다. 그렇다고 비트코인을 무한으로 생성할 수 있는가? 그것도 거짓이다. 비트코인의 경우 2100만개로 한정되어 있기 때문이다. 그렇기에 비트코인이 가상화폐로서의 가치를 갖는다. 금과 비슷한 맥락으로 한정된 수량이고, 캐면 캘수록 나오는 확률이 더 적어져, 희귀성이 높아지기 때문이다. 

## 네트워크의 질문
그럼 네트워크는 채굴자에게 어떤 질문을 던지고, 왜 채굴이 힘든지 알아보자. 채굴자는 그 블록을 구성해야하는 데이터를 알고 있다고 이야기하였다. 그렇다면 채굴자의 역할은 데이터와 이전 블록의 해시를 결합하여 현재 블록의 해시를 만들어야한다. 이 과정에서 네트워크의 질문이 등장한다. 앞서 해시에 대한 설명을 할 때, 하나의 데이터에서 하나의 해시가 나타난다(결정론적)고 하였다. 단, 'nonce'를 조정하면 이를 다른 해시로 변경이 가능하다. 즉 'I am groot'에서 nonce가 0인 해시와 1인 해시는 다른 값으로 나타난다. 이 때 nonce는 간단히 정수라고 생각해보자. 또한 해시가 16진수로 나타난다고 가정해보자. 그렇다면 해시에서 나타날 수 있는 결과는 0부터 f까지 가능하다. 여기서 네트워크가 질문을 한다. '해시를 만들어주세요. 단, 처음 시작하는 값이 0000(0이 네개)인 해시를 만들어주세요.'라고 질문을 한다. 여기서 0의 개수가 곧 난이도를 나타낸다. 그렇다면 채굴자는 이전 해시와 현재 데이터를 결합한 값을 해시로 나타내는 과정에서 0이 4개인 해시를 만들어내야하며, 이는 nonce의 값을 변경해주며 찾게 된다. 무작위로 형성되는 해시 값에서 0이 4개인 값을 찾는 데에는 매우 오랜 시간이 걸릴 것이다. 또한 nonce 값의 한계가 없다면, 여타 알고리즘을 대입하여 찾는 것보다 0부터 1씩 증가하여 찾는 부르트포스 알고리즘이 그나마 효율적이므로 매우 비효율적인 알고리즘을 대입하여 채굴해야 할 것이다. 현재 비트코인은 19개의 0으로 시작하는 것으로 질문을 한다고 한다. 그렇기에 비트코인을 채굴하는 것은 상당히 난이도가 높은 작업이며, 흡사 노가다의 형태를 띠기 때문에 시간에 비례한 보상을 기대하기도 어렵다. 이에 더하여 네트워크 측에서 현재 10분마다 새로운 블록을 생성하여 질문하기 때문에, 10분 안에 질문에 답을 해야한다는 점도 채굴의 난이도를 높인다. 

## 채굴의 가능성
그렇다면 채굴은 매우 비효율적이며, 하면 시간만 낭비하는 행위인가? 꼭 그렇지는 않다. 이는 최근 그래픽카드의 가격이 상당히 높아진 것에서 찾을 수 있다. 이 포스트는 그래픽카드에 대해 다루는 것이 아니므로, 채굴에 성능이 좋은 그래픽카드를 최근에 나오는 그래픽카드라고만 덧대어 이야기하자면, 최근의 그래픽카드들은 nonce를 1초에 6천만개까지 계산한다고 한다. 네트워크에서 생성되는 블록의 주기가 10분임을 감안하면 꽤 채굴을 할만한 것이다. 그리하여 최근들어 블록체인이라는 기술이 대두가 되고, 그래픽카드의 성능이 높아짐에 따라 채굴자가 늘어났고, 채굴도 꽤 할만한 것이다. 다만, 채굴을 하는 환경에 따른 제약 및 조건, 혹은 국가의 개입 등을 고려한다면 채굴자가 채굴을 하는 것에 있어서 신중해야한다. 이하 막론하고, 이 포스트는 기술에 대하여 다루므로, 블록체인의 기술 및 그 기술이 돈이 되는 이유까지 다루었다. 그리고 이를 마지막으로 포스팅을 마치고자 한다.
