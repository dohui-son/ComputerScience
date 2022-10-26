# 1\. MA 모놀리틱 아키텍처 Monolithic Artchitecture

---

- 마이크로 서비스 아키텍쳐(MSA)에 반대되는 개념으로, **애플리케이션 모든 구성 요소가 한 프로젝트에 통합되어 있는 형태**를 말함.
- 전체 어플리케이션이 하나로 되어있어 배포 및 테스트도 하나의 애플리케이션만 하면 되기에 개발 및 환경 설정이 단순함.
- 각 컴포넌트들이 함수로 호출 되기 때문에 성능 제약이 덜하고 운영이 용이.
- 작은 볼륨의 시스템 개발시 유용.
- 서비스 간 호출이 하나의 프로세스 내에서 이루어지기 때문에 속도가 상대적으로 빠를 수도 있음.

[##_Image|kage@2mjDz/btrPsBDw08T/1hgs5Y6HBy5UGA8cx5GZ21/img.jpg|CDM|1.3|{"originWidth":828,"originHeight":318,"style":"alignCenter"}_##]

출처 : [https://medium.com/koderlabs/introduction-to-monolithic-architecture-and-microservices-architecture-b211a5955c63](https://medium.com/koderlabs/introduction-to-monolithic-architecture-and-microservices-architecture-b211a5955c63)

### 장점

- 단순한 아키텍처 구조로 초기 개발에 용이하다.
- 배포가 간단하다.
- End-to-End 테스트가 용이하다.
- 확장이 쉬움(로드 밸런스를 이용하여 로드 부하를 나눠가지는 방식으로 진행)

### 단점

- 빌드 및 배포 시간 증가 : 프로젝트 규모가 커질수록 애플리케이션 구동 지연이 늘어나고 빌드 및 배포 시간이 길어진다.
- 전체 빌드 및 배포의 불가결함 : 구조적 결합도가 높음으로 단순 수정 사항이 있어도 전체를 빌드하고 배포해야 한다.
- 유지보수의 어려움 : 전체 코드가 총합되어 있기에 코드 이해도가 떨어지며 유지보수가 어렵다.
- 장애 전파 : 하나의 서비스가 모든 서비스에 영향을 줌.  
  ( 버그가 전파 및 확산될 수 있다. 이벤트 서버에 트래픽이 몰려 해당 서버가 죽으면 모든 서비스가 마비됨. )
- 선택적 확장의 어려움 : 전체 애플리케이션 확장은 쉽지만, 부하 분산을 위해 각 컴포넌트를 선택적 확장이 어렵고 프로젝트 전체를 확장해야 함.

# 2\. MSA 마이크로 서비스 아키텍처 Micro Service Artchitecture

---

- **_하나의 큰 애플리케이션을 여러 작은 애플리케이션으로 쪼개어 변경 및 조합이 가능한 형태를 말함._**
- 각 컴포넌트는 서비스 형태로 구현되고 API를 이용하여 타 서비스와 통신하게 됨.
- 각 서비스는 독립된 서버로 타 컴포넌트와 의존성이 없어 독립 배포.  
  [##_Image|kage@7uPTC/btrPtIaT0j2/AJFEBmkj16ufxJcOOe1g4k/img.png|CDM|1.3|{"originWidth":539,"originHeight":370,"style":"alignCenter"}_##]  
  출처 : [https://microservices.io/](https://microservices.io/)

### 장점

- 독립성 확보 : 독립적인 개별 확장 ( ex. 온라인 쇼핑몰에서 주문 서버만 트래픽 증가한다면 해당 서버만 확장해주면 됨. )
- 장애 격리 : 각 서비스가 독립적이고 타 컴포넌트 의존성이 떨어지기에 버그가 전파 확률이 떨어짐. 서비스 간 장애 격리가 비교적 쉬움.
- 유연성 확장 : 여러 작은 애플리케이션으로 쪼개어 개발되었기에 변경 및 조합이 용이함.
- 적시 배포 : 일부 수정이 있어도 전체를 다시 재배포해야 하는 MA에 비해 독립 배포가 가능함으로 적시에 배포를 할 수 있음.

### 단점

- 서비스 간 호출을 API통신을 이용하기에 비교적 속도가 느림.
- 통신에 사용하기 위해 값을 데이터 모델로 변환시켜주는 오버헤드 발생 가능.

**_REFERENCE_**  
[https://blog.lgcns.com/2981?category=515093](https://blog.lgcns.com/2981?category=515093)  
[https://velog.io/@tedigom/MSA-제대로-이해하기-1-MSA의-기본-개념-3sk28yrv0e](https://velog.io/@tedigom/MSA-%EC%A0%9C%EB%8C%80%EB%A1%9C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-1-MSA%EC%9D%98-%EA%B8%B0%EB%B3%B8-%EA%B0%9C%EB%85%90-3sk28yrv0e)  
[https://levelup.gitconnected.com/the-advantages-of-microservices-vs-monolithic-architectures-94ce25ae3fd](https://levelup.gitconnected.com/the-advantages-of-microservices-vs-monolithic-architectures-94ce25ae3fd)  
[https://velog.io/@tedigom/MSA-제대로-이해하기-2-MSA-Outer-Architecure](https://velog.io/@tedigom/MSA-%EC%A0%9C%EB%8C%80%EB%A1%9C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-2-MSA-Outer-Architecure)  
[https://www.samsungsds.com/kr/insights/msa.html](https://www.samsungsds.com/kr/insights/msa.html)  
[https://www.comworld.co.kr/news/articleView.html?idxno=49710](https://www.comworld.co.kr/news/articleView.html?idxno=49710)  
[https://steady-coding.tistory.com/595](https://steady-coding.tistory.com/595)
