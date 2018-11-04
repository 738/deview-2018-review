# react-native: 웹 개발자가 한달만에 앱 출시하기

## 사례
* 페이스북
* 인스타그램
* 디스코드
* 케이크
  * 앱개발자 1명
  * 안드로이드 & iOS 개발기간 1달
  * 매달 정기 업데이트
  * 기존 앱 개발 방식이었다면 가능했을까?

## 선택의결과
* 투입한 개발 리소스 ↓ = 최종 결과물의 퀄리티 ↑
* 플랫폼간 공유 코드 ↑ = QA & 유지 보수 비용 ↓

빠른 개발 -> 코드 공유 -> 쉬운 개선

> React Native는 단 기간에 프로덕션 레벨의 크로스 플랫폼 앱을 만들어야 할 때 고려할 수 있는 여러 선택지 중 가장 가성비가 좋은 프레임워크다.

## react-native 완벽한 이해

React Component -> React Native -> Bridge -> Android, iOS

### Threading Structure

#### Bridge 특징

_1. Asynchronous_

**AS-IS** Native 동기화 호출: 완료 시점까지 Javascript 처리 대기

**TO-BE** Native 비동기 호출: 완료 시점까지 Javascript 처리 진행

_2. Serializable_

**AS-IS** 독립적으로 운영되는 두 영역 간의 데이터 공유: 많은 관리 이슈 발생

**TO-BE** 직렬화 된 메시지 교환: 간결해진 구조 대신 성능 저하 발생

_3. Batched_

**AS-IS** Native 호출마다 직렬화와 역직렬화의 과정에서 부하 발생

**TO-BE** 큐에 넣어 5ms 단위로 일괄 처리하는 방식으로 성능 개선


#### Bridge 모니터링

* MessageQueue 모니터링 방법

```javascript
import MessageQueue from 'react-native/Libraries/BatchedBridge/MessageQueue';

MessageQueue.spy(true);
MessageQueue.spy((info) => console.log("I'm spying!", info));
```

#### react-native의 발전방향

Facebook의 개선 방향

1. New Threading model
2. New async rendering capabilities
3. Faster and more lightweight bridge


## Cake 프로젝트에 얻은 노하우 & 탑

### EXPO(CRNA) 사용 자제

1. 시작만 쉽고 모든 게 어려워짐
2. 기본으로 제공하는 기능은 많지만 앱이 너무 커짐 (기본 25~30MB)
3. 추가적인 Native 모듈을 설치할 수 없음 (제일 큰 이유!)

**속 편하게 처음부터 빌드 방식(`react-native-cli`)으로 시작해라**

### 효율적인 작업 순서

기본적인 작업 (레이아웃, 데이터 연동) -> 복잡한 애니메이션 & 인터랙션 확인 -> iOS에 특화된 UX 작업

중간에 안드로이드에서 확인하지 않으면 나중에 놀랄 수 있음!

### Import 경로 지옥 탈출

상대경로 말고 절대경로를 사용하고 싶다면 `babel-plugin-root-import`를 적용

### Optional Chaining

```javascript
// AS-IS
if(data && data.items && data.items.length > 2) {
    drawList(data);
}

// TO-BE
if(data?.items?.length > 2) {
    drawList(data);
}
```

Optional chaining operator 사용으로 쉽게 Null Safety 코딩! (0.56 버전부터 가능)

### Lock dependencies

잘못된 라이브러리 업데이트는 고통을 불러옴

#### 버전 고정하는 방법

1. 설치마다 고정 버전으로 설치하기
```bash
$ npm install --save --save-exact react-native-fbsdk
$ yarn add --exact react-native-fbsdk
```

2. 전역 기본 옵션으로 설정하기
```bash
$ npm config set save-exact=true
```

### Flow는 처음부터 꼭 사용해라

Flow를 적용해서 타입을 정의하면 파라미터 타입 오류의 사전 감지가 가능
1. 코드 진단
2. 자동 완성
3. 타입 힌트
4. 빠른 함수 이동

요즘은 타입스크립트도 지원이 많이 되어서 괜찮음


### 컴파일된 번들 파일 확인

자신이 짠 코드를 babel로 어떻게 변환되는지 확인해보는 것도 의미 있음

```bash
$ npm -g install js-beautify
```

```bash
$ react-native bundle --platform android --dev false --entry-file index.js --bundle-output index.android.bundle
$ js-beautify index.android.bundle > index.android.bundle.js
```

### 성능을 고려한 정적 이미지 사용

**AS-IS** Javascript packager가 동작하는 방식: Bundle 파일 생성 -> 모듈 ID로 치환

**TO-BE** App Resources 사용하기

1. 기존 Native 개발 방식(Xcode asset catalogs / Android drawable folder)으로 추가
2. 크기 속성을 꼭 정의

### 성능을 고려한 리모트 이미지 사용

**내장 Image 컴포넌트의 문제**

1. Flickering
2. Cache misses
3. Low performances

```bash
// SDWebImage (iOS) / Glide (Android) 라이브러리 사용으로 문제점 개선
$ npm install react-native-fast-image
```

### JavaScriptCode의 동작 오류

* Remote Debug 모드는 크롬의 V8 엔진 사용 (JavaScriptCore 엔진은 Date 처리에 문제가 많으므로 moment.js 라이브러리 사용)

* 플랫폼 간에도 다르게 동작할 수 있음 (안드로이드는 오래된 버전의 JavaScriptCore 엔진 사용중임)

### 플랫폼별 컴포넌트 스타일링

* 재정의 방식으로 스타일 정의하기
```javascript
import StyleSheet from './PlatformStyleSheet';
const styles = StyleSheet.create({
    title: {
        fontSize: 16,
        ios: { fontSize: 18 },
        android: { fontSize: 17, color: 'red' }
    }
});
```

```javascript
import { Platform, StyleSheet } from 'react-native';
const PlatformStyleSheet = {
    create(styles) {
        const platformStyles = {};
        for (const key in styles) {
            const { ios, android, ...style } = styles[key];
            (ios || android) && Object.assign(style, Platform.select({ios, android}));
            platformStyles[key] = style;
        }
        return StyleSheet.create(platformStyles);
    },
}

export default PlatformStyleSheet;
```

### 편리한 Style 자동완성

* atom-react-native-style 패키지 설치

### 안드로이드 Text 위 아래 패딩 제거

* includeFontPadding 스타일 속성 끄기 (iOS와 동일하게 TextView의 ascent, descent 기준으로 출력)

### 공용 Text 컴포넌트 사용하기

```javascript
Class Text extends PureComponent {
    static defaultStyle = Platform.select({
        ios: { fontFmaily: 'AppleSDGothicNeo-Regular' },
        android: {
            fontFamily: 'sans-serif',
            includeFontPadding: false
        }
    });

    render() {
        const { children, style, ...props } = this.props;
        return <Text {...props}
                     allowFontScaling={false} style={[Text.defaultStyle, style]}>
                     {children}
                </Text>;
    }
}
```

### 터치 영역 확장하기

* hitSlop으로 최소한 44dp의 터치 영역을 보장해주세요.

```javascript
<TouchableWithourFeedback
  hitSlop={{top: 7, right: 7, bottom: 7, left: 7}}>
  <View .../>
</TouchableWithourFeedback>
```

### 놓치기 쉬운 최초 화면 렌더링

* render() 함수가 최초에 한 번 실행된다는 걸 잊기 쉬움
* render() -> componentDidMount() -> render()
* 출력 여부 상태 값으로 불필요한 초기 렌더링 제거

### 화면에 보이지 않지만 동작하는 코드

* 타이머/이벤트 리스너 사용 시 꼭 제거

### 개발자 도구

* react-native: Perf Monitor(iOS)
* Xocde: View Hierarchy Debugger
* Android Studio: Profiler

### 60 FPS 보장하기

### 효율적인 애니메이션 사용

* Javascript Driver 동작 순서

requestAnimationFrame 함수 실행 -> 값 계산 후 View.setNativeProps 함수 실행 -> Bridge로 전달 -> UI 업데이트

* Native Driver 동작 순서

메인 쓰레드에서 프레임마다 실행 -> 계산된 값으로 직접 View 업데이트 호출 -> UI 업데이트

```Javascript
Animated.timing(this._animation, {
 toValue: 1,
 duration: 1000,
 useNativeDriver: true,   // add this
}).start();
```

### 무거운 코드의 올바른 실행 시점

* 애니메이션과 인터랙션이 끝난 후로 실행 지연

반복되는 애니메이션이 있다면 등록한 코드가 실행되지 않거나 실행 시점의 문제 발생

* 다음 프레임으로 실행 지연

현재 프레임의 다른 실행을 보장해서 앱 반응성 개선

```javascript
import { InteractionManager } from 'react-native';

componentDidMount() {
  InteractionManager.runAfterInteractions(() => {
    this.doExpensiveAction();
  });
}

handleOnPress() {
  requestAnimationFrame(() => {
    this.doExpensiveAction();
  });
}
```

### FlatList 성능 개선

### 효율적인 레퍼런스 사용

### Google Play API Level 26 정책 대응

### 안드로이드 APK 최적화

### 앱 크기에 대한 걱정은 오해

### 네비게이션 모듈 선택

### 복잡한 애니메이션은 Lottie

#### 출처
* 발표자료: [링크](https://www.slideshare.net/deview/121react-native)
* 발표자: 스노우 이성민 개발자님
