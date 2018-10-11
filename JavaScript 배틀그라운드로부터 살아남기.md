자바스크립트 탄생배경
다이내믹한 웹을 만들고자하는 비전
새롭게 개발된 이유
자바스럽게 보여야함과 자바를 돋보이게하는 마케팅적측면

모카 -> 라이브스크립트 -> 자바스크립트
es6 : 2015.06

파생버전
JScript, ActionScript (ES4에 기반)
AJAX
JSON

* Server-side
* node
requirejs, commonjs

# PM
npm, bower

프레임워크의 등장
브라우저 (에버그린 브라우저)

vanilla is not common
프레임워크 + 툴체인 (트랜스파일러, 번들링)
실작업 코드는 브라우저에서 직접적인 실행 어려움

프레임워크 + 개발도구
npm 패키지를 사용, ‘조립’
개발방식의 진화

Library -> Framework
직접적인 dom 핸들링 필요성 감소
dom api native 지원향상
컴포넌트단위의 ㅣㄱ능에 집중 dom은 프레임워크에 맡김 프레임워크에따라

트랜스파일링 에라

babel(6to5)

2018년 동향
버전 구분 중요성 감소
ES8
async/await
shared memory and atomics
es9
regexp imporvemnet

es10 catch ㅔㅁㄱㅁ

웹어셈블리
프로그래밍언어를 컴파일해 어느 브라우저에서나 빠르게 실행되는 바이너리로 바꾸는 기술
정적타입시스템
부족한영역 loose typing 을 채워줌

react.js
vue.js
typescript로 작성예정
angular
webcomponents
polymer

npm vs yarn
npm이 요즘은 더빠름

번들러/빌드 도구
webpack (configpack)
0CJS
configuration headache
parcel
무설정 번들링 지향

모바일 애플리케이션
JS to Native

* NativeScript
    * Angular friendly
* React Native

데스크톱 애플리케이션
* ELECTRON (NW.js 기반)
* NW.js

ServiceWorker (오프라인캐싱)

PWA
* workbox
* hnpwa
* pwa starter kit
* pwa-helpers

WebXR Device API
immersive web: 웹에서 몰입 환경 구현을 위한 신기술 모음

자바스크립트는 어디로가고잇나
FE BE 구분없이 하나의 코드셋으로 모든 곳에서 실행

javascript fatigue
많은 가이드들은 몇가지만 설치/설정하면 쉽다(out of the box)고 말한다. 수많은 플러그인과 설정 등을 접하다보면 쉬운거맞어ㅓ?
우리는 무엇을 알아야할까

How to stay: up-to-date

* Trends
    * FE Tech Mailings
    * Github Trending
* Browsers Update
    * Chrome
    * Webkit
    * MS Edge
    * Firefox
* 컨퍼런스
    * JSConf
    * Fluent
    * DotJS
    * JSKongress
    * Netflix Javascript Talks

매몰비용 오류의 함정
- 특정 도구에 투자한 노력이 많아지면 나의 선택(도구)이 합리적이었다는 것을 자신이나 다른사람들에게 설득하기 위해 노력

대체로 개발자들은 기존에 문제없이 사용하던 기술들을 뒤로하고 새롭고 반짝
'mapie developer syndrome’

TS adds sweetness, but at a price.
지속적 복잡도 증가
이미 필수적인 도구들도 넘쳐나는 상황에서 무언가를 하나 추가할때마다 비례하는 도구들의 증가

최신 업데이트 항상 정답인가?
도구들의 업데이트에 따라 코드 수정이 필요한 모순적 상황
이러한 작업은 때에 따라 많은 리소스 수반
메이저 업데이트 후 수많은 플러

각자의 사정은 모두 다르다. 무엇이 정답이라 할 수 없다.
모든 것을 다알아야 할까
누군가는 특정영역에 따라
모든것을 알수잇을까?
everything is amazing and nobody is happy

우리의 자세는?
* “expert” 로서 모든 플랫폼의 모든것을알아야한다는생각
* 모든것을 배우는것이해결책인가
* 단순하게 현재작업에 필요한것 또는 끌리는것에 집중

결국은 적당한 밸런스
너무 많은 것을 알려고하지않아도된다. 그러나 적당한호기심은가져야하며 지속적인 꾸준함은필요
세상은할게너무많다
