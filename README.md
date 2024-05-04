# 🙌 Kafka를 활용한 ws서버의 zero-downTime-deploy 구현하기

## 🛠 사용한 Tool

## Kafka

Pub/Sub을 도입하여, 사용가능한 서버를 Event방식으로 처리하기 위해 도입

zookeeper의 앙상블은 사용하지 않으면, Kafka의 설정값은 내부 `kafka-setting` 참고

## MySQL

서버가 사용유무에 대한 상태를 위해, Controller Tower Server가 시작 될 떄에 기본 값을 MySQL의 DB를 참조하여 시작이 된다.

이 후, 추가적인 이벤트에 대해서 Kafka의 이벤트를 Subcribe하면서 동작하게 된다.

## 🙋‍♀️ DB Schema

## 🙋‍♀️ 서버 Diagram

1. FE에서 사용가능한 ws 서버리스트들을 관리하고, 해당 ws 서버리스틀을 기반으로 ws 연결을 진행

2. FE에서 ws 서버와 통신을 하면서, Connection을 유지하며 처리

3. Kafka를 통해서 ws 서버가 올라오고, 내려가는 이벤트를 탐지하여, Tower Server에서 사용가능한 리스트를 수정

4. FE에서 ws 요청에 대해, 실패하는경우, Tower Server에서 내려가는 사용가능한 서버들 중에 retry하면서 Connection을 새로 생성하여 처리
