

## 프로세스

---

<details>
<summary><strong style="font-size:1.17em">
프로세스가 무엇인가요?
</strong></summary>

```text
프로세스는 실행중인 프로그램의 인스턴스 입니다.
각 프로세스는 하나 이상의 스레드로 구성되어있고,
실행하는 데 필요한 코드,데이터,스택,힙 등의 메모리 공간과
파일, 소켓 같은 시스템 자원들을 포함하고 있습니다. 
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
프로그램과 프로세스, 스레드의 차이에 대해 설명해 주세요.
</strong></summary>

```text
프로그램은 실행파일입니다. 여기에는 코드나 프로세서 명령집합이 
파일형태로 디스크에 저장되어있습니다.

프로그램의 코드가 메모리에 로드되고
프로세서에 의해 실행되면 프로세스가 됩니다. 

메모리 구조 측면에서
프로세스는 다른 프로세스와 완전히 독립된 메모리 공간인 코드,데이터,힙 영역을 가지지만
스레드는 프로세스 내에서 스택 영역만 따로 할당받고
나머지 영역은 다른 스레드와 공유합니다.

또, 프로세스는 서로 독립적이라 IPC같은 별도의 통신 방식이 필요한 반면, 
스레드는 프로세스 내의 자원을 공유하기 때문에 데이터 공유가 쉽습니다.

컨텍스트 스위치 비용은
프로세스의 경우, PCB에 저장된 프로세스의 상태 정보를 모두 교체해야 합니다. 
여기에는 CPU 레지스터 상태, 메모리 관리 정보, 캐시 메모리 등이 포함됩니다.

반면 스레드는 같은 프로세스의 PCB를 공유하므로, CPU 레지스터와 스택 포인터만 교체하면 됩니다. 
메모리 맵이나 캐시는 그대로 유지되어 훨씬 효율적입니다
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
PCB가 무엇인가요?
</strong></summary>

```text
PCB는 각 프로세스의 정보를 담은 구조체입니다. 
거기에는 프로세스 상태,cpu register 정보, 스케줄링 정보,메모리정보,
io정보등이 저장되어있습니다.
그리고 이 PCB는 운영체제가 관리합니다. 
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
그렇다면, 스레드는 PCB를 갖고 있을까요?
</strong></summary>

```text

```

</details>

---







---


<details>
<summary><strong style="font-size:1.17em">뮤택스와 세마포어 차이?</strong></summary>

```text
뮤텍스는 Locking 메커니즘으로 락을 걸은 쓰레드만이 임계 영역을 나갈때 락을 해제할 수 있습니다.
wait와 signal 이라는 원자적 연산을 사용합니다.  

하지만 세마포어는 Signaling 메커니즘으로 락을 걸지 않은 쓰레드도 signal을 사용해 락을 해제할 수 있습니다.
```

</details>



## OS 스케줄링 방식

```text

- FCFS
    - 먼저 들어온 프로세스부터 레디 큐에 올려서 처리한다.
    - 비선점 방식
- SJF
    - Shortest Job First의 약자이고, 즉 최단 작업 우선 스케쥴링이란 뜻으로, 
    평균 대기 시간을 최소화하기위해서 CPU점유 시간(Burst Time)이 가장 적은 프로세스를 먼저 실행시키는 정책이다.
    
    - 특히 비선점 방식을 가지는 정책을 SJF라 한다.
- SRTF
    - 선점형(Preemptive) 스케줄링 
    - 현재 실행 중인 프로세스보다 더 짧은 실행 시간을 가진 프로세스가 도착하면, 실행 중인 프로세스를 중단하고 새로운 프로세스를 실행합니다.
    
- 라운드로빈
    - 선점형 방식으로 모든 프로세스에 동일한 우선순위를 부여하여 공평하게 CPU 시간을 분배합니다.
```

## 페이지 교체 알고리즘

```text
OPT (Optimal)

이상적인 알고리즘으로, 미래의 페이지 참조를 미리 알고 있다고 가정합니다.
앞으로 가장 오랫동안 사용되지 않을 페이지를 교체합니다.
실제로 구현하기는 불가능하지만, 다른 알고리즘의 성능을 평가하는 기준으로 사용됩니다.


FIFO (First In First Out)

가장 먼저 들어온 페이지를 가장 먼저 교체하는 방식입니다.
구현이 간단하지만, 중요한 페이지가 자주 교체될 수 있는 단점이 있습니다.


LRU (Least Recently Used)

가장 오랫동안 사용되지 않은 페이지를 교체합니다.
최근 사용 이력을 바탕으로 미래 사용 가능성을 예측하는 방식입니다.
구현이 복잡하지만 OPT에 근접한 성능을 보입니다.


LFU (Least Frequently Used)

참조 횟수가 가장 적은 페이지를 교체합니다.
장기적인 사용 빈도를 고려하지만, 최근성을 반영하지 못하는 단점이 있습니다.


MFU (Most Frequently Used)

LFU와 반대로, 참조 횟수가 가장 많은 페이지를 교체합니다.
사용 빈도가 높은 페이지는 이미 그 역할을 다했다는 가정에 기반합니다.
실제로는 자주 사용되는 중요한 페이지를 교체할 위험이 있어 잘 사용되지 않습니다.


NUR (Not Used Recently)

LRU의 근사 알고리즘으로, 구현이 더 간단합니다.
각 페이지에 '참조 비트'와 '수정 비트'를 사용합니다.
최근에 사용되지 않은 페이지 중에서 수정되지 않은 페이지를 우선적으로 교체합니다.
```

---

## 동기, 비동기, 블로킹, 논블로킹

---

<details>
<summary><strong style="font-size:1.17em">동기와 비동기, 블로킹과 논블로킹의 차이에 대해 설명해 주세요.</strong></summary>
</details>


---

<details>
<summary><strong style="font-size:1.17em">그렇다면, 동기이면서 논블로킹이고, 비동기이면서 블로킹인 경우는 의미가 있다고 할 수 있나요?</strong></summary>



</details>

---

<details>
<summary><strong style="font-size:1.17em">I/O 멀티플렉싱에 대해 설명해 주세요.</strong></summary>

```text
관심있는 I/O 작업들을 동시에 모니터링하고 
그중에 완료된 I/O 작업들을 한번에 알려줍니다.
```

</details>



