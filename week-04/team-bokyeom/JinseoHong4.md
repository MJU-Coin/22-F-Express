# section 7

# MVC 패턴

### 디자인 패턴

소프트웨어의 개발 방법을 공식화 한 것.

소수의 뛰어난 엔지니어가 해결한 문제를 다수의 엔지니어들이 처리 할 수 있도록 한 규칙. 구현자들 간의 커뮤니케이션 효율성 높임.

### MVC패턴이란

MVC(모델 - 뷰 - 컨트롤러) 패턴은 UI, 데이터 제어, 논리 제어를 구현하는데 사용되는 소프트웨어 디자인 패턴.

어플리케이션을 세가지의 역할로 구분한 개발 방법론

사용자가 컨트롤러 조작 → 컨트롤러가 모델을 통해 데이터 가져옴 → 뷰를 통해 사용자에게 전달.

SW의 비즈니스 로직과 화면을 구분하는데 중점을 둠 → 업무 분리, 향상된 관리.

### Web 에서의 MVC

1. 사용자가 웹사이트 접속 (Uses)
2. 컨트롤러는 요청된 페이지를 서비스 하기 위해 모델 호출(Manipulates)
3. 모델은 DB나 파일 같은 데이터를 제어한 후 결과 리턴
4. 컨트롤러는 모델이 리턴한 결과 뷰에 반영(Updates)
5. 데이터가 반영된 뷰는 사용자에게 보여짐.(Sees)

### 1. 모델: 데이터와 비즈니스 로직 관리

모델은 앱이 포함해야할 데이터 정의.

데이터 변화 → 뷰, 컨트롤러에 알림

뷰는 최신의 결과를 보여줌.

컨트롤러는 모델 변화에 따라 명령도 변화시킬 수 있음.

**규칙**

- 사용자가 편집하길 원하는 모든 데이터를 가지고 있어야함
- 뷰, 컨트롤러에 대해 어떤 정보도 알지 말아야 함
- 변경이 일어나면, 변경을 알려줄 처리 방법을 구현해야함.

### 2. 뷰: 레이아웃, 화면 처리

MVC에서 모델은 여러개의 뷰를 가질 수 있음

앱의 데이터를 보여주는 방식 정의

표시할 데이터를 모델로부터 받음

**규칙**

- 모델이 가지고 있는 정보를 따로 저장하면 안됨.
- 다른 구성요소를 몰라야 함.
- 변결될 때 통지할 처리 방법 구현.

### 3. 컨트롤러: 명령을 모델과 뷰 부분으로 라우팅.

MVC의 뷰는 여러개의 컨트롤러를 가지고 있음.

앱에서 사용자의 입력에 대한 응답으로 모델과 뷰를 업데이트 하는 로직 포함.

모델에 명령을 보내서 모델의 상태를 변경하거나 뷰에 명령을 보내 모델의 표시 방법을 바꿀 수 있음.

**규칙**

- 모델이나 뷰에 대해 알고 있어야 함
- 모델이나 뷰의 변경을 모니터링 해야함

### MVC 패턴을 사용하는 이유

유지 보수의 편리성.

기존에 유지보수 시 높아지던 기능간의 결합도 → 사소한 변경도 다른 비즈니스 로직에 영향 → 버그 유발 가능

UI 시스템의 핵심 컴포넌트를 세가지로 나누고 자신의 역할만 수행하고 넘겨주는 방식으로 시스템 결합도를 낮춤.

유지보수 시에도 특정 컴포넌트만 수정 → 쉬운 시스템 변경 가능.

### 한계

대규모 프로그램의 경우 다수의 뷰와 모델이 컨트롤러에 연결 → 컨트롤러가 불필요하게 커지는 현상 발생

복잡한 화면을 구성하는 경우도 동일한 현상 발생.

‘Massive-View-Controller’ 라고 함.
