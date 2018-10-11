# react-native: 웹 개발자가 한달만에 앱 출시하기
# 사례
* 페이스북
* 인스타그램
* 디스코드
* 케이크
앱개발자 1명
안드로이드 & iOS 개발기간 1달
매달 정기 업데이트

선택의결과
1. 투입한 개발 리소스 down = 최종 결과물의 퀄리티 up
2. 플랫폼간 공유 코드

# react-native 완벽한 이해 
React Component -> React Native -> Bridge -> Android, iOS

# Threading Structure
Bridge 특징 (1) : Asynchronous
Native 비동기 호출: 완료 시점ㄲ자ㅣ 자바스크립트 처리 진행
2: Serializable
직렬화된 메시지 교환: 간결해진 구조 대신 성능 저하 발생
3: Batched
Native 호출마다 직렬화와 역직렬화의 과정에서 부하 발생
큐에 넣어 5ms
MessageQueue 모니터링 방법 spy

Native -> Bridge -> javascript

UIManager, Networking
네이티브의 네트워크 요청 처리시 메시지큐 로그
브릿지와의 통신 최소화해야함

발전방향
1. New Threading model
2. New async rendering capabilities
3. Faster and more lightweight bridge

노하우 팁
프로덕션 레벨 프로젝트라며 ㅇ엑스포는 사용하지마세요
시작만 쉽고 모든게 어려워짐
기본으로 제공하는 기능이 많지만 앱이 너무커짐
추가적인 네이티브 모듈을 설치할 수 없다

속편하게 처음부터 빌드방식으로 시작하세요

효율적인 작업 순서

기본적인 작업 (레이아웃 , 데이터 연동) -> 복잡한 애니메이션 & 인터랙션 확인 -> ios에 특화된 ux 작업

* bable-plugin-root-important 적용
* import someexample from ‘~/some/examp.e/'


Optional Chaining (0.56 가능)
옵셔널 체이닝 오퍼레이터 널세이프티 코딩가능

lock dependencies 버전고정

npm install —save —save-exact react-native0sdk


Flow는 처음부터 꼭 사용하세요! 
(타입스크립트 안사용하는 이유?)

flow적용시 발생하는 문제해결

컴파일된 번들 파일 확인

npm -g install js-beatify
내가 짠 코드가 babel로 어떻게 변환되는지 확인해보는것도의미있다

# 성능을 고려한 정적 이미지 사용

javascript 패키져가 동작하는 방식 ->번들파일 생성 ->모듈id로 치환

<Image source ={{uri: ‘my_icon’}} style={{}}}

 기존 네이티브 개발방식으로 추가
사이즈 반드시 입력


성능을 고려한 리모트 이미지 사용

SDWebImage Glide 라이브러리 사용으로 문제점 개선

react-native-image

내장 이미지컴포너ㅌ읨 누제

플리커링

캐시미시스
로우 펄포먼스



자바스크립트 코어의 동작 오류

리모트 디버그 모드는 크롬의 브이팔 엔진 사용
자바스크립트코어엔진은 데이터 처리에 문제가 많음 (moment.js 라이브러리 사용)

안드로이드느느 자바스크립트코어 오래된 버전 사용중
플랫폼 간에도 다르게 동작할 수 있어요.

플랫폼 별 컴포넌트 스타일링
재정의 방식으로 스타일 정의
atom-react-native-style 

안드로이드텍스트 위 아래 패딩 제거
includeFontPadding 스타일 속성 끄기
ios와 동일하게

공용 Text 컴포넌트 사용하기

터치영역확장하기
힙슬롭으로 최소한 44dp의 터치영역으로 보장해주세요
hitslop={{}}

놓치기 쉬운 최초화ㅏ면 렌더링
render() 함수가 최초에 한번실행된다는걸 잊기쉽자
출력여부 상태값으로 불필요한 초기렌더링제거! (로딩뷰)

화면에 보이지않지만 동작하는코드

타이머/이벤트 리스너 사용 시 꼭 제거해주세요.
끄지않으면 백그라운드에서 계속발생함

개발자도구
perf monitor  프로세스 메모리 jsc views ui js 개발자도구

xcode: view hierarchy debugger 
android: studio: profiler

60fps 보장하기
자연스러운 애니메이션
requestAnimationFrame 함수 실행
-> 값계산후 view.setnativeprops 함수 실행
-> bridge로 전달
-> ui 업데이트
useNativeDriver: true로 ㅅ속성 주면

메인쓰레드에서 프레임마다 실행
-> 계산된값으로 직접 View 업데이트 호출
-> UI 업데이트


무거운 코드의 올바른 실행 시점
애니메이션과 인터랙션이 끄난 후로 실행 지연
반복되는 애니메이션이 있다면 등록한 코드가 실행되지 않거나 실행시점문제발생

다음프레임으로 실행지연
현재 프레임의 다른 실행을 보장해서 앱반응성 개선

faltlist 성능개선
getitemLayout  속성사용
높이가 고정된 구성이라면 레이아웃의 크기를 매번계산하지않아서 성능개선

효율적인 레퍼런스 사용
1. string refs
2. callback refs
3. React.createRef() (tofhtodrla)

구글플레ㅣㅇ 타겟 api 26 정책 대응

안드로이드 apk  chlwjrghk
1. split apk
2. 
def enableSeparateBuidl =true
2. 프로가드 적용
쉬링크 리소스 옵션 사용금지

babel-pligin tranform remove console


불필요한 localized reosoucr 제거

앱크기에대한 걱정은 노

네비게이션 모듈 선택
react-navigation
react-native-navigation (네이티브 구현체 버전2개발중)

복잡한 애니메이션은 Lottie
디자이너한테 복잡한 애니메이션도 다 된다고 자신있게 말하세요





















































