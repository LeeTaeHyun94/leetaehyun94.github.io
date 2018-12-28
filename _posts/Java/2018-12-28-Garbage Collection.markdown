---
layout: post
title:  "Garbage Collection"
date:   2018-12-28 23:30:00
categories: Java
comments: true
---
Java는 프로그램 코드 내부에서 메모리를 명시적으로 직접 해제하지 않는다. 때문에 Garbage Collector가 더 이상 필요없는 사용되지 않는 객체를 찾아 지우는 작업을 한다.

stop-the-world 이후에 Garbage Collection 작업을 완료한다. 때문에 Java를 이용해 개발하게 된다면 프로그램의 성능을 높이기 위해서는 직접 Java의 Garbage Collection 상황을 모니터링해 튜닝이 필요하다.

- stop-the-world : JVM이 애플리케이션을 실행 중지하는 것을 말한다. Garbage Collection을 실행하는 쓰레드 외에 나머지 쓰레드는 모두 작업을 멈추게 된다.
- Garbage Collector가 더 이상 필요없는 객체를 찾는 알고리즘
    - Young Generation 영역 : 새롭게 생성한 객체의 대부분이 이 영역에 위치한다.
        - 대부분의 객체가 금방 접근 불가 상태가 되기 때문에 매우 많은 객체가 이 영역에 생성되었다가 사라진다.
        - 이 영역에서 객체가 사라질 때 Minor GC가 발생한다고 한다.
        - Eden 영역과 2개의 Survivor 영역으로 나뉜다.
        - 새로 생성한 대부분의 객체는 Eden 영역에 위치
        - Eden 영역에서 GC가 한 번 발생한 후 살아남은 객체는 Survivor 영역 중 하나로 이동
        - Eden 영역에서 GC가 발생하면 살아남아 있는 객체가 존재하는 Survivor영역으로 객체가 계속 쌓인다.
        - 하나의 Survivor영역이 가득 차게 되면 그 중에서 살아남은 객체를 다른 Survivor 영역으로 이동
        - 가득 차 있던 Survivor 영역은 빈 상태가 된다.
        - 위 과정을 반복하다가 계속해서 살아남아 있는 객체는 Old 영역으로 이동된다.
        - Survivor 영역 중 하나는 반드시 빈 상태여야 한다. 만약에 그렇지 않다면 시스템 상태가 비정상이라는 것
    - Old Generation 영역 : 접근 불가능 상태로 되지 않아 Young 영역에서 살아남은 객체가 이 영역으로 복사된다.
        - 대부분 Young 영역보다 크게 할당하며, 크기가 큰 만큼 Young 영역보다 GC는 적게 발생한다.
        - 이 영역에서 객체가 사라질 때 Major GC가 발생한다고 한다.
        - Old 영역의 기본적으로 데이터가 가득 차면 GC를 실행한다.
        - JDK 7 기준 5가지의 GC 방식이 있다.
            - Serial GC
                - Old 영역의 GC는 mark-sweep-compact 알고리즘을 사용한다.
                    - Old 영역의 살아 있는 객체를 식별(Mark)
                    - 힙의 앞 부분부터 확인하여 살아 있는 것만 남긴다.(Sweep)
                    - 각 객체들이 연속되게 쌓이도록 힙의 가장 앞 부분부터 채워서 객체가 있는 부분과 없는 부분으로 나눈다.(Compaction)
                - 메모리가 적고 싱글 코어일 때 적합한 방식
            - Parallel GC
                - 기본적인 알고리즘은 Serial GC와 같다.
                - GC를 처리할 때 다수의 스레드를 이용하기 때문에 Serial GC보다 빠르게 처리할 수 있다.
                - 메모리가 충분하고 코어의 개수가 많을 때 유리하다.
                - Throughput GC라고도 한다.
                - ![Serial GC & Parallel GC](./../../assets/Java/4.PNG)
            - Parallel Old GC
                - JDK 5 update 6부터 제공한 GC 방식
                - Parallel GC와 Old 영역의 GC 알고리즘만 다르다.
                - Mark-Summary-Compaction 알고리즘을 사용 : 앞서 GC를 수행한 영역에 대해서 별도로 살아 있는 객체를 식별(Summary)
            - Concurrent Mark & Sweep GC
                - Initial Mark 단계 : ClassLoader에서 가장 가까운 객체 중 살아 있는 객체만 찾는다.
                - Concurrent Mark 단계 : 살아있음을 확인한 객체에서 참조하고 있는 객체들을 따라가면서 확인, 다른 스레드가 실행 중인 상태에서 동시에 진행된다.
                - Remark 단계 : Concurrent Mark 단계에서 새로 추가되거나 참조가 끊긴 객체를 확인
                - Concurrent Sweep 단계 : 쓰레기 정리, 다른 스레드가 실행 중인 상태에서 동시 진행
                - stop-the-world 시간(멈추는 시간)이 매우 짧다.
                - 애플리케이션의 응답 속도가 매우 중요할 때 사용하며, Low Latency GC라고도 부른다.
                - 다른 GC 방식보다 메모리와 CPU를 많이 사용한다.
                - Compaction 단계가 기본적으로 제공되지 않기 떄문에 조각난 메모리가 많아 Compaction 작업 시에 stop-the-world 시간이 다른 GC 방식보다 길기 때문에 Compaction 작업에 대한 모니터링이 필요하다.
                - ![Serial Mark-Sweep-Compact Collector & Concurrent Mark-Sweep Collector](./../../assets/Java/5.PNG)
            - Garbage First(G1) GC
                - 바둑판의 각 영역에 객체를 할당하고 GC를 실행한다.
                - 해당 영역이 꽉 차면 다른 영역에서 객체를 할당하고 GC를 실행한다.
                - 다른 방식에 적용된 Young, Old 영역의 개념이 없다.
                - 이전의 GC 방식들보다 빠르다.
                - ![G1 GC](./../../assets/Java/6.PNG)
    - 영역별 데이터 흐름
        - ![GC Data Flow](./../../assets/Java/1.PNG)
        - ![GC Data Flow(Young Generation -> Old Generation)](./../../assets/Java/3.PNG)
    - Permanent Generation 영역 : Method Area라고도 한다. 객체나 억류(intern)된 문자열 정보를 저장하는 곳
        - 이 영역에서 GC가 발생해도 Major GC의 횟수에 포함된다.
    - Old 영역의 객체가 Young 영역의 객체를 참조하는 경우
        - Old 영역에는 512 byte의 덩어리(chunk)로 되어 있는 card table이 존재한다.
        - 이 Card table을 통해 Old 영역의 객체가 Young 영역의 객체를 참조할 때마다 정보를 표시한다.
        - Young 영역의 GC를 실행할 때에는 Old 영역에 있는 모든 객체의 참조를 확인하는 것이 아니라 이 Card table만 탐색해서 GC 대상인지 식별한다.
        - ![Card Table](./../../assets/Java/2.PNG)
        - Card table은 Write Barrier를 사용하여 관리한다.
            - Write Barrier : Minor GC를 빠르게 할 수 있도록 하는 장치
                - 약간의 오버헤드는 발생하지만 전반적인 GC 시간은 감소


