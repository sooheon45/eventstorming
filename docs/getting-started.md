
## 소개

[eventstorming2code.io](http://eventstorming2code.io) 는 온라인 Event Storming 도구로서, 이벤트 기반 마이크로서비스 (Microservices Native) 를 결과물 코드로 생성해 줍니다!

> ![](.//media/image2.png)
> <p align="center"> 그림 1 EventStorming2Code 도구 화면 (예시) </p>

이벤트스토밍(Event Storming)은 Event와 BrainStorming의 합성어로서, 이벤트 기반 시스템의 설계와 개발을 빠르게할 수 있는 기법이다. 기존의 UML, BPMN 등의 이해도와 전무성을 갖추지 않더라도 현업, 업무전문가, 도메인전문가 들이 모여 화이트보드 벽면에 주요 이벤트(Event)를 중심으로 업무들간의 상호 연관성을 스티키 노트(Sticker)를 가지고 협업해 나간다.

이벤트를 유발시키는 행위(사용자의 의사결정)와 해당 이벤트에 연이어 반응하는 액션들을 1)모든 이해 관계자들이, 2)짧은 시간 내에, 3)시각적으로 모델링 한다. 궁극적으로 마이크로서비스를 여러 개로  쪼개는데 활용 가능하다.

EventStorming2Code는 이러한 오프라인 이벤트스토밍이 공간적인 제약과, 화이트보드 벽면에 부착된 스티커가 물리적 요인으로 쉽게 떨어질 수 있다는 점을 보완하여 고안된 온라인 도구이다.

또한, 결과 모델을 단위 마이크로서비스 코드, 클라우드 환경에 필요한 도커 파일과 CI/CD 배포 파이프라인(Pipeline) 등 자동화된 환경 구성을 생성해 준다.
이러한 템플릿을 여러분의 선호하는 언어와 플랫폼에 맞도록 커스터마이징 할 수도 있다. 

--- 

### 주요 Features

  - **Web-based Event Storming environment**
    
      - 6 types of Event Sticker  
        (Event, Policy, Command, Aggregate, External System, Read Model)
    
      - Bounded Context and Context Mapping (Relation between
        Microservices)
    
      - English word suggestion
    

  - **Code Generation**
    
      - MSA Implementation Source Codes (Default: Spring-boot)
    
      - Dockerfile
    
      - Pipeline YAML file for CI/CD DevOps
    
      - Helm Chart for Kubernetes Deployment

  - **Custom Templates for Microservice’s Polyglot language**
    
      - Template customizing support (Any language is available)
    
      - Local and remote(Github) template add-in support


---

### 도구의 배경과 목적

#### EDA(Event Driven Architecture) 기반 3세대 MSA의 유행

모노리식 아키텍처는 큰 배포 단위 속에 상호 모듈들의 의존도가 높을 뿐만 아니라 단일 DB를 사용함으로 인해, 사소한 개선 사항의 적용에도 표준 가이드라인 준수, 복잡한 결재 라인을 통한 승인 획득 등 지속적인 딜리버리 절차에 더 많은 시간을 요구하고 있는게 현실이다. 

더욱이, 치열한 경쟁 시장에서 살아남기 위해서는 고객이 실제 우리 제품에 대해 관심이 있는지를 빠른 시장 출시를 통해 파악한 후, 관심과 호응도가 높을 시, 제대로 구현하는 “Fail Fast”, “Fail Cheap”의 에자일한 접근 전략이 필요하다.

이러한 대안으로 제시된 기존 SOA(Service Oriented Architecture)에서는 생산성을 극대화하기 위해 하나의 정해진 데이터베이스, 잘 짜여진 API와 스키마를 준수하면서 공통 서비스를 도출하고 이를 재사용하면서 이루려 했다. 그러나 빠르고 기민하게 요구사항을 받아들이고 반영해야 하는 비즈니스 라이프사이클 상에서 표준화(Standardization)는 오히려 팀별 자발적 생산성을 저해하는 커다란 걸림돌이 되고 있다.

그래서 등장한 것이 마이크로서비스 아키텍처이다. 마이크로서비스는 서비스를 함축적 (Implementation Hiding)으로 제공하자는 측면에서 SOA 사상과 유사하나, 서비스 레벨 뿐만 아니라 데이터베이스 레벨까지 철저하게 분리하자는 것이 SOA와 크게 구분되는 점이다. 

초기의 마이크로서비스는 서비스의 자율성과 독립성, 서비스에 최적화된 저장소(Polyglot Persistence) 선택이 가능한 아키텍처로 고안되었으나, 서비스간 호출 시, 동기식 API 방식 (Requeste & Response)을 주로 사용함으로 인해 타임 커플링(Time Coupling)이라는 약점이 존재했다. 

타임 커플링된 서비스들은 서비스 블로킹(Blocking) 우려와 한 서비스에서 발생한 장애가 타 서비스로 전파될 수 있는 구조로 인해 웹 스케일 기반 시스템에서는 치명적인 단점이 있어, 이를 회로 차단(Circuit Breaking) 등의 방법으로 극복하려 하였다.
 

> ![](.//media/image3.png)
> <p align="center"> 그림 2 1세대 마이크로서비스 아키텍처 예시</p>

 이를 보완한 것이, 최근 각광받고 있는 이벤트 기반(EDA)의 3세대 MSA로, 도메인에서 발생하는 이벤트를 큐를 통하여 브로드캐스팅(BroadCasting)하는 마이크로서비스간 Pub/Sub을 통해 상호 커뮤니케이션하는 아키텍처를 따른다.

> ![](.//media/image4.png)
> <p align="center"> 그림 3 EDA기반 3세대 마이크로서비스 아키텍처 예시 </p>


 예를 들어, 주문이 발생하였을 때, 직접 배송팀에다 ‘’배송을 준비하세요.’라고 지시하는 것은 주문팀의 입장에서는 그다지 중요한 것이 아니다. 주문팀은 배송팀이 배송을 하던 말던 관심이 없다는 것이다.

REST방식(직접 호출)으로 서로 통신할 경우, 요청자는 다음 액션을 수행하기 위해 응답이 도착할 때까지 기다려야 하는 블로킹(Blocking) 즉, 타임 커플링이 일어난다. 

만약, 주문팀이 발생한 사실에 대해 비동기 기반 큐(single Source Of Truth)에 “주문이 발생하였습니다.” 라고 신고만 하고, 이어지는 액션을 배송팀이 알아서 수행해도 된다. 이처럼 “발생한 사실을 신고”하고, "신고된 사실을 구독"하는 패턴의 아키텍처를 이벤트 드리븐(Event Driven) (또는, 화이트보드 패턴)이라고 한다. 

그렇게 되면 1세대 MSA에서는 배송팀의 비즈니스 프로세스가 주문팀이 호출해 실행되던 방식이, 3세대 MSA에선 배송팀이 직접 이벤트에 반응하여 실행하는 방식으로 실행 주체가 바뀌게 된다.

 신설된 마케팅팀 또한, 주문팀의 주문 발생으로 수행해야 할 비즈니스 프로세스가 있다면, 단순하게 주문팀의 “주문이 발송하였습니다.” 라는 이벤트에 대해 마케팅팀도 반응하여 수행하면 된다는 것이다. 

본 도구는 이러한 생소할 수 있는 EDA기반 MSA를 쉽게 도출하고 개발하기 위한 지원도구이다.
 
 #### 이벤트스토밍 애자일 기법의 유행
 
 이벤트 기반 3세대MSA 구축에 필요한 이벤트스토밍은 현업, 업무 전문가, 도메인 전문가들이 업무들 간의 상호 연관성을 분석하고 설계하기 위한 협업 공간을 필요로 한다. 

서비스 규모에 비례하여 더 크고 넓은 협업 공간과 이벤트스토밍이 종료되는 시점까지 해당 공간을 점유하고 있어야 한다.

> ![](.//media/evtstrm.jpg)
> <p align="left"> 이미지 출처 : Pivotal_Methodology 이벤트스토밍 예시</p>

그러나, EventStorming2Code(이하, ES2Cd) 도구를 사용하게 되면, 현업, 도메인 전문가, 시스템 개발자의 협업이 도구가 제공하는 브라우저 기반 전자적 화이트보드 상에서 가능하므로 시공간적 제약이 없어진다.

또한, 이벤트스토밍이 매일 2시간씩 2~3주 동안 수행되더라도 스티키 노트의 분실이나, 훼손의 우려가 없으며, 결과물 또한 전자적으로 자동 관리된다는 장점이 있다.

#### MSA 코드 자동 생성

오프라인 이벤트스토밍 환경에선 이벤트스토밍 결과 모델을 참조하여 개발자가 수작업으로 코딩해야 한다. 코딩은 전적으로 팀내 개발자의 몫으로, 스티커 분량 만큼 개발 대상도 늘어난다. 더욱이 개발자가 이벤트 기반 MSA 코딩에 익숙하지 않을 경우, 어떻게 시작해야 하는지에 대한 러닝 커브로 인해 얘기치 않은 병목 구간이 될 수도 있다.

웹 스케일 기반 서비스일 경우, 서비스 구현에 최적화된 언어(Language)를 사용하는 것이 서버 사이드 퍼포먼스를 높여 사용자의 응답시간(Respose Time)을 줄이는 점에서 유리하다.

ES2Cd 도구는 이벤트스토밍 결과에 대해 개발자가 설정한 폴리글랏 언어로 MSA 소스 코드를 자동으로 생성하여 준다. 도구를 통해 수행된 결과는 순공학(Forward Engineering) 코드 생성 모듈을 통해 MSA 소스코드로 생성되며, 사용자 정의 가능한 확장 템플릿을 통해, 각 MSA마다 서비스에 최적화된 언어를 적용할 수 있도록 지원한다.

또한, 워크로드 분산 엔진(Workload Distribution Engine) 기반의 클라우드 배포를 위한 Dockerfile과 CI/CD 파이프라인, 컨테이너 Runtime 환경에서 MSA를 쉽게 생성할 수 있도록  Helm Chart 스크립트까지도 자동으로 생성해 준다. 

이처럼 본 도구를 사용하게 되면, MSA 소스코드는 물론, DevOps 담당자가 클라우드 운영에 필요한 메타 정보(Configuration)를 수작업으로 작성해야 하는 번거로움을 줄일 수 있다.


#### Polyglot MSA를 위한 User-defined 템플릿

과거 모노리식 어플리케이션은 간단한 경우, 어플리케이션 서버와 DB서버 두개만 관리하면 되지만, MSA에서는 기본적으로 한 서버에
하나의 서비스만 실행되므로, 서비스 수만큼의 이기종 인스턴스 서버와 각 서비스에 최적화된 데이터베이스 적용이 가능하다. 즉 모든
서비스마다 반드시 동일한 개발 언어, 동일한 프레임워크로 구성될 필요가 없는 것이다.

예를 들어 TPS(시간당 트랜잭션)가 높고, 읽기 작업이 많은 MSA서비스는 Node, Redis 기반으로 구현하고, 트랜잭션 및
안정성이 중요한 MSA 서비스에는 Spring, RDB를 적용할 수 있는데 이를 ‘Polyglot Architecture(폴리글랏
아키텍처)’ 라고 한다.

ES2Cd 도구는 이러한 폴리글랏 아키텍처를 지원하기 위해 팀플릿 기반 MSA 코드 생성을 지원한다. ES2Cd의 커스텀 템플릿
기능을 활용하여 기본 제공 템플릿 외에 개발자가 템플릿을 추가하여 EventStorming결과가 원하는 템플릿에 맞추어 코드가
생성될 수 있도록 한다.

커스텀 템플릿의 자세한 내용은 [4.3 커스텀 템플릿 (Custom Template)](/EventStorming2Code?id=커스텀-템플릿-custom-template)</span>에서 설명한다.

---

### 도입 효과

ES2Cd 도구는 이벤트스토밍(EventStorming)이라는 DDD 구현 방법론이 가지는 장점들을 그대로 가지면서 이벤트스토밍에
필요한 충분한 공간적인 요소가 요구되지 않고, 벽면에 부착되는 다양한 스티커 노트들의 분실 및 훼손의 우려가
없다.

| **구 분**           | **오프라인 EventStorming**        | **ES2Cd**              |
| ----------------- | ----------------------------- | ---------------------- |
| Support Phase | 분석, 설계                        | 분석, 설계, 개발, 운영         |
| 시공간적 제약           | 충분한 화이트보드 공간 필요               | 제약 없음                  |
| MSA 코드 구현         | MSA 구현 스킬을 보유한 개발자에 의한 수작업 개발 | 도구에서 초기 소스코드 자동생성      |
| Ployglot MSA      | 팀별 자체 구현                      | 사용자정의 확장 템플릿으로 자동생성 지원 |
| DevOps 지원         | 없음                            | CI/CD 파이프라인 자동생성       |
| 결과물 관리 용이성        | 분실 및 훼손 우려 높음                 | 결과물 버전관리 및 전자적 보관      |

<p align="center"> 표 2 이벤트스토밍 도구 도입효과 </p>

오프라인 이벤트스토밍으로 DDD기반 도메인 분석 및 설계가 가능하지만, ES2Cd는 분석에서부터 운영에 이르는 MSA 전 주기를
지원한다. 기존 MSA 스킬을 보유한 개발자가 직접 수작업으로 개발하던 소스코드는 도구에서 초기 소스코드를 자동으로 생성해
주며, 오프라인 이벤트스토밍에서는 불가능한 결과물 버전관리와 수행 결과물의 전자적 보관은 소프트웨어 기반의 이벤트스토밍
툴인 ES2Cd가 제공하는 당연한 이점이다.

---

### 실행 환경

<table>
<thead>
<tr class="header">
<th>구분</th>
<th>내  용</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>지원 OS</td>
<td>Windows, Linux, Mac OS 지원</td>
</tr>
<tr class="even">
<td>지원 Cloud</td>
<td><p>All Cloud Platform 지원</p>
<p>(AWS, GCP, MS Azure, IBM/Oracle Cloud, OpenShift)</p></td>
</tr>
<tr class="odd">
<td>서비스 유형</td>
<td>On-Premise, or SaaS</td>
</tr>
<tr class="even">
<td>필요 사양</td>
<td>Memory 512MB 이상</td>
</tr>
<tr class="odd">
<td>지원 Browser</td>
<td>크로스 브라우저 지원 (IE, Edge 등 MS계열 제외)</td>
</tr>
<tr class="even">
<td>설치 모듈</td>
<td>없음</td>
</tr>
</tbody>
</table>
<p align="center"> 표 3 EventStorming2Code 실행 환경 </p>


