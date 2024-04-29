# 컴포넌트에 props 전달하기

React 컴포넌트는 props를 이용해 서로 통신합니다.  
모든 부모 컴포넌트는 props를 줌으로써 몇몇의 정보를 자식 컴포넌트에게 전달할 수 있습니다.  
props는 HTML 속성(attribute)을 생각나게 할 수도 있지만,  
객체, 배열, 함수를 포함한 모든 JavaScript 값을 전달할 수 있습니다.

## 학습 내용

- 컴포넌트에 props를 전달하는 방법
- 컴포넌트에서 props를 읽는 방법
- props의 기본값을 지정하는 방법
- 컴포넌트에 JSX를 전달하는 방법
- 시간에 따라 props가 변하는 방식

<br>

## 친숙한 props

props는 JSX 태그에 전달하는 정보입니다.
예를 들어,  
`className`, `src`, `alt`, `width`, `height` 는 `<img>` 태그에 전달할 수 있습니다:

```javascript
function Avatar() {
  return (
    <img
      className="avatar"
      src="https://i.imgur.com/1bX5QH6.jpg"
      alt="Lin Lanying"
      width={100}
      height={100}
    />
  );
}

export default function Profile() {
  return <Avatar />;
}
```

![alt text](./image/image-31.png)

`<img>`태그에 전달할 수 있는 props는 미리 정의되어 있습니다. (ReactDOM는 HTML 표준을 준수합니다.)  
자신이 생성한 `<Avatar>`와 같은 어떤 컴포넌트든 props를 전달할 수 있습니다. 방법은 다음과 같습니다.

## 컴포넌트에 props 전달하기

아래 코드에서 `Profile` 컴포넌트는 자식 컴포넌트인 `Avatar`에 어떠한 props도 전달하지 않습니다:

```javascript
export default function Profile() {
  return <Avatar />;
}
```

다음 두 단계에 걸쳐 Avatar에 props를 전달할 수 있습니다.

## 자식 컴포넌트에 props 전달하기

먼저, `Avatar` 에 몇몇 props를 전달합니다.  
예를 들어, `person` (객체)와 `size` (숫자)를 전달해 보겠습니다:

```javascript
export default function Profile() {
  return (
    <Avatar person={{ name: "Lin Lanying", imageId: "1bX5QH6" }} size={100} />
  );
}
```

<br>

### Note

만약 person= 뒤에 있는 이중 괄호가 혼란스럽다면,  
JSX 중괄호 안의 객체라고 기억하시면 됩니다.

이제 `Avatar` 컴포넌트 내 props를 읽을 수 있습니다.

## 자식 컴포넌트 내부에서 props 읽기

이러한 props들은 function Avatar 바로 뒤에 있는 ({ 와 }) 안에
그들의 이름인 person, size 등을 쉼표로 구분함으로써  
읽을 수 있습니다.  
이렇게 하면 Avatar 코드 내에서 변수를 사용하는 것처럼 사용할 수 있습니다.

```javascript
function Avatar({ person, size }) {
  // person and size are available here
}
```

`Avatar`에 렌더링을 위해 `person` 과 `size` props를 사용하는 로직을 추가하면 끝입니다.

이제 `Avatar`를 다른 props를 이용해 다양한 방식으로 렌더링하도록 구성할 수 있습니다. 값을 조정해보세요!

```javascript
import { getImageUrl } from "./utils.js";

function Avatar({ person, size }) {
  return (
    <img
      className="avatar"
      src={getImageUrl(person)}
      alt={person.name}
      width={size}
      height={size}
    />
  );
}

export default function Profile() {
  return (
    <div>
      <Avatar
        size={100}
        person={{
          name: "Katsuko Saruhashi",
          imageId: "YfeOqp2",
        }}
      />
      <Avatar
        size={80}
        person={{
          name: "Aklilu Lemma",
          imageId: "OKS67lh",
        }}
      />
      <Avatar
        size={50}
        person={{
          name: "Lin Lanying",
          imageId: "1bX5QH6",
        }}
      />
    </div>
  );
}
```

![alt text](./image/image-32.png)

props를 사용하면 부모 컴포넌트와 자식 컴포넌트를 독립적으로 생각할 수 있습니다.  
예를 들어, Avatar 가 props들을 어떻게 사용하는지 생각할 필요없이 Profile의 person 또는 size props를 수정할 수 있습니다.  
마찬가지로 Profile을 보지 않고도 Avatar가 props를 사용하는 방식을 바꿀 수 있습니다.

props는 조절할 수 있는 “손잡이(볼륨 다이얼같은 느낌)“라고 생각하면 됩니다.  
props는 함수의 인수와 동일한 역할을 합니다.  
사실 props는 컴포넌트에 대한 유일한 인자입니다!  
React 컴포넌트 함수는 하나의 인자, 즉,props 객체를 받습니다:

```javascript
function Avatar(props) {
  let person = props.person;
  let size = props.size;
  // ...
}
```

보통은 전체 `props` 자체를 필요로 하지는 않기에, 개별 props로 구조분해 합니다.

### Pitfall | 함정

props를 선언할 때 ( 및 ) 안에 { 및 } 쌍을 놓치지 마세요:

```javascript
function Avatar({ person, size }) {
  // ...
}
```

이 구문을 `“구조 분해 할당”`이라고 부르며 함수 매개 변수의 속성과 동등합니다.

```javascript
function Avatar(props) {
  let person = props.person;
  let size = props.size;
  // ...
}
```

## prop의 기본값 지정하기

값이 지정되지 않았을 때, prop에 기본값을 주길 원한다면,  
변수 바로 뒤에 `=` 과 함께 기본값을 넣어 구조 분해 할당을 해줄 수 있습니다.

```javascript
function Avatar({ person, size = 100 }) {
  // ...
}
```

이제, `<Avatar person={...} />`가 size prop이 없이 렌더링된다면, size는 100으로 설정됩니다.

이 기본값은 size prop이 없거나 `size={undefined}` 로 전달될 때 사용됩니다.  
그러나 만약 `size={null}` 또는 `size={0}`으로 전달된다면,  
기본값은 사용되지 않습니다.

## JSX 전개 구문으로 props 전달하기

때때로 전달되는 props들은 반복적입니다:

```javascript
function Profile({ person, size, isSepia, thickBorder }) {
  return (
    <div className="card">
      <Avatar
        person={person}
        size={size}
        isSepia={isSepia}
        thickBorder={thickBorder}
      />
    </div>
  );
}
```

반복적인 코드는 가독성을 높일 수 있다는 점에서 잘못된 것은 아닙니다.  
하지만 때로는 간결함이 중요할 때도 있습니다.  
Profile 컴포넌트가 Avatar 컴포넌트에게 그런 것처럼,  
일부 컴포넌트는 그들의 모든 props를 자식 컴포넌트에 전달합니다.  
<br>
이 경우 Profile 컴포넌트는 props를 직접적으로 사용하지 않기 때문에,  
보다 간결한 “전개(spread)” 구문을 사용하는 것이 합리적일 수 있습니다:

```javascript
function Profile(props) {
  return (
    <div className="card">
      <Avatar {...props} />
    </div>
  );
}
```

이렇게 하면 Profile의 모든 props를 각각의 이름을 나열하지 않고 Avatar로 전달합니다.

전개 구문은 제한적으로 사용하세요.  
다른 모든 컴포넌트에 이 구문을 사용한다면 문제가 있는 것입니다.  
이는 종종 컴포넌트들을 분할하여 자식을 JSX로 전달해야 함을 나타냅니다.  
더 자세히 알아봅시다!

## 자식을 JSX로 전달하기

브라우저 빌트인 태그는 중첩하는 것이 일반적입니다:

```JSX
<div>
  <img />
</div>
```

때로는 만든 컴포넌트들끼리 중첩하고 싶을 수도 있습니다:

```JSX
<Card>
  <Avatar />
</Card>
```

JSX 태그 내에 콘텐츠를 중첩하면,  
부모 컴포넌트는 해당 컨텐츠를 `children` 이라는 prop으로 받을 것입니다.  
예를 들어,  
아래의 `Card` 컴포넌트는 `<Avatar />` 로 설정된 `children` prop을 받아  
이를 감싸는 div에 렌더링할 것입니다

```JSX
import Avatar from './Avatar.js';

function Card({ children }) {
  return (
    <div className="card">
      {children}
    </div>
  );
}

export default function Profile() {
  return (
    <Card>
      <Avatar
        size={100}
        person={{
          name: 'Katsuko Saruhashi',
          imageId: 'YfeOqp2'
        }}
      />
    </Card>
  );
}

```

![alt text](./image/image-33.png)

`<Card>` 내부의 `<Avatar>`를 텍스트로 바꾸어 `<Card>` 컴포넌트가 중첩된 콘텐츠를 어떻게 감싸는지 확인해 보세요.

`<Card>`는 children 내부에서 무엇이 렌더링되는지 “알아야 할” 필요가 없습니다.  
이 유연한 패턴은 많은 곳에서 볼 수 있습니다.

`children` prop을 가지고 있는 컴포넌트는  
부모 컴포넌트가 임의의 JSX로 “채울” 수 있는 “구멍”을 가진 것이라고 생각할 수 있습니다.  
패널, 그리드 등의 시각적 래퍼에 종종 `children` prop를 사용합니다.

![alt text](./image/image-34.png)

## 시간에 따라 props가 변하는 방식

아래의 `Clock` 컴포넌트는 부모 컴포넌트로부터  
`color` 와 `time` 이라는 두 가지 props를 받습니다.  
(부모 컴포넌트의 코드는 아직 자세히 다루지 않을 state를 사용하기 때문에 생략합니다).

아래 select box의 색상을 바꿔보세요:

```JSX
export default function Clock({ color, time }) {
  return (
    <h1 style={{ color: color }}>
      {time}
    </h1>
  );
}
```

![alt text](./image/image-35.png)

이 예시는 컴포넌트가 시간에 따라 다른 props를 받을 수 있음을 보여줍니다.  
Props는 항상 고정되어 있지 않습니다!  
여기서 time prop은 매초마다 변경되고,  
color prop은 다른 색상을 선택하면 변경됩니다.  
Props는 컴포넌트의 데이터를 처음에만 반영하는 것이 아니라 모든 시점에 반영합니다.

<br>
그러나 props는 불변으로, 컴퓨터 과학에서 “변경할 수 없다”는 뜻의 용어입니다.  
컴포넌트가 props를 변경해야 하는 경우  
(예: 사용자의 상호작용이나 새로운 데이터에 대한 응답으로)  
부모 컴포넌트에 다른 props, 즉,새로운 객체를 전달하도록 “요청”해야 합니다!  
그러면 이전의 props는 버려지고(참조를 끊는다),  
결국 JavaScript 엔진은 기존 props가 차지했던 메모리를 회수(가비지 컬렉팅. GC) 하게 됩니다.

<br>
“props 변경”을 시도하지 마세요.  
선택한 색을 변경하는 등 사용자 입력에 반응해야 하는 경우에는  
State: 컴포넌트의 메모리에서 배울 “set state”가 필요할 것입니다.

<br>

## 요약

- Props를 전달하려면 HTML 속성 사용할 때와 마찬가지로 JSX에 props를 추가합니다.
- Props를 읽으려면 `function Avatar({ person, size })` 구조 분해 구문을 사용합니다.
- `size = 100` 과 같은 기본값을 지정할 수 있으며, 이는 누락되거나 `undefined` 인 props에 사용됩니다.
- 모든 props를 `<Avatar {...props} />` JSX 전개 구문을 사용할 수 있지만, 과도하게 사용하지 마세요.
- `<Card><Avatar /></Card>` 와 같이 중첩된 JSX는 Card컴포넌트의 `children` prop로 표시됩니다.
- Props는 읽기 전용 스냅샷으로, 렌더링할 때마다 새로운 버전의 props를 받습니다.
- Props는 변경할 수 없습니다. 상호작용이 필요한 경우 state를 설정해야 합니다.
