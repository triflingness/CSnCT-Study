# 데브옵스(DevOps)
> 개발 방법론 중 하나로 소프트웨어의 개발(Development)과 운영(Operations)의 합성어

애플리케이션과 서비스를 **빠른 속도로 제공**할 수 있도록 **조직의 역량을 향상**시키는 문화 철학, 방식 및 도구의 조합   
**시스템 개발자와 운영을 담당하는 정보기술 전문가 사이**의 소통, 협업, 통합 및 자동화를 강조하는 소프트웨어 개발 방법론

## 목적
기존의 소프트웨어 개발 및 인프라 관리 프로세스를 잘 사용하는 조직보다 **제품을 더 빠르게 혁신하고 개선할 수 있음**

## 장점
1. **속도**   
    고객을 위해 더 빠르게 혁신하고, 시장 변화에 더 잘 적응하고, 좀 더 효율적으로 비즈니스 성과 창출 가능   
    마이크로 서비스와 지속적 전달을 사용하면 팀에서 서비스를 주도적으로 운영하여 업데이트를 좀 더 빠르게 릴리즈할 수 있음   
    
2. **신속한 제공**   
    릴리즈의 빈도와 속도를 개선하여 더 빠르게 혁신하고 개선 가능   
    지속적 통합과 지속적 전달은 빌드에서 배포까지 소프트웨서 릴리즈 프로세스를 자동화하는 방식   
    
3. **안정성**   
    최종 사용자에게 지속적으로 긍정적인 경험을 제공하는 한편 더욱 빠르게 안정적으로 제공할 수 있도록 애플리케이션 업데이트와 인프라 변경의 품질 보장   
    지속적 통합 및 지속적 전달과 같은 방식을 사용하여 각 변경 사항이 제대로 작동하며 안전한지 테스트   
    모니터링과 로깅 방식을 통해 실시간으로 성능에 대한 정보 얻을 수 있음   
    
4. **확장**   
    규모에 따라 인프라와 개발 프로세스 운영 및 관리   
    자동화와 일관성이 지원되므로 위험을 줄이면서 복잡한 시스템 또는 변화하는 시스템을 효율적으로 관리 가능   
    코드형 인프라를 사용하면 개발, 테스트 및 프로덕션 환경을 반복 가능하고 좀 거 효율적인 방식으로 관리 가능   
    
5. **협업 강화**   
    개발자와 운영팀은 긴말하게 협력하고, 많은 책임을 공유하며, 워크플로를 결합   
    비효율성을 줄이고 시간 절약
    
6. **보안**   
    자동화된 규정 준수 정책, 세분화된 제어 및 구성 관리 기술을 사용함으로써 보안을 그대로 유지하면서 DevOps 모델 도입 가능   
    코드형 인프라와 코드형 정책을 사용하면 규모에 따라 규정 준수를 정의하고 추적 가능
    
## 방식
1. **지속적 통합 CI**   
    자동화된 빌드 및 테스트가 수행된 후, 개발자가 코드 변경 사항을 중앙 리포지토리에 정기적으로 병합하는 방식   
    버그를 신속하게 찾아 해결하고, 소프트웨어 품질을 개선하고, 새로운 소프트웨어 업데이트를 검증 및 릴리즈하는 데 걸리는 시간을 단축하는 것이 핵심 목표
    
2. **지속적 전달 CD**   
    프로덕션에 릴리즈하기 위한 코드 변경이 자동으로 빌드, 테스트 및 준비되는 소프트웨어 개발 방식   
    빌드 단계 이후의 모든 코드 변경 사항을 테스트 환경 및 프로덕션 환경에 배포함으로써 지속적 통합을 확장   
    개발자는 언제나 즉시 배포할 수 있고 표준화된 테스트 프로세스를 통과한 빌드 아티팩트를 보유하게 됨
    
3. 마이크로 서비스   
    단일 애플리케이션을 작은 서비스의 집합으로 구축하는 설계 접근 방식   
    각 서비스는 자체 프로세스에서 실행되고 주로 HTTP기반 API라는 간편한 메커니즘을 사용하는 잘 정의된 인터페이스를 통해 다른 서비스와 통신
    
4. 코드형 인프라   
    버전 관리 및 지속적 통합과 같은 코드와 소프트웨어 기술을 사용하여 인프라를 프로비저닝하고 관리하는 방식
    
5. 모니터링 및 로그   
    지표와 로그를 모니터링하여 애플리케이션 및 인프라 성능이 제품의 최종 사용자 경험에 어떤 영향을 미치는지 확인
    
6. 커뮤니케이션 및 협업   
    개발 및 운영의 워크플로와 책임을 물리적으로 합침으로써 협엽이 이루어짐
<br/>

# 데브옵스 엔지니어
- 프로그래머, 시스템 관리자, DBA 등 모든 역할을 연결하는 과정을 돕는 인력
- 데브옵스 툴에 대한 이해와 여러 프로그래밍 언어에 관한 지식을 기반으로 지속적 전달과 지속적 통합 워크플로우 도입
- **개발과 운영 모두에서 충분한 지식과 경험을 보유**하고 어떻게 함께 작업할 수 있는지를 이해하고 팀원들과 서로 소통하는 사람

## 데브옵스 엔지니어 스킬
- 기초: 리눅스 관리, 파이썬, AWS 또는 다른 클라우드 플랫폼
- 구성: 테라폼(Terraform) 또는 앤서블(Ansible)
- 버전 관리: 깃(Git), 깃허브(GitHub)
- 패키징 : 도커(Docker)
- 배포 : 젠킨스(Jenkins)
- 실행 : 아마존 ECS, 쿠버네티스
- 모니터링 : ELK 스택

💡 모든 플랫폼과 툴을 마스터하는 것보다 최소한 어떻게 상호 연계해 작동할 수 있는지 알아야 함

## 데브옵스 엔지니어의 역할과 책임
- 서버 측 기능에 대한 사양 및 문서 작성
- CI/CD 관리
- CI/CD 스크립트 작성
- 성능 평가 및 모니터링
- IT 인프라 유지보수 및 관리(H/W, S/W, 네트워크, 스토리지, 가상 및 원격 자산, 클라우드 데이터 스토리지 포괄)

##### 참고
- [https://aws.amazon.com/ko/devops/what-is-devops/](https://aws.amazon.com/ko/devops/what-is-devops/)   
- [https://www.itworld.co.kr/news/118329](https://www.itworld.co.kr/news/118329)
