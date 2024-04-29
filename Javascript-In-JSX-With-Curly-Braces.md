# JSX에서 JavaScript 사용하기

JSX를 사용하면 JavaScript 파일 내에 HTML과 유사한 마크업을 작성하여 렌더링 로직과 콘텐츠를 같은 위치에 유지할 수 있습니다.  
때로는 마크업 안에 약간의 JavaScript 로직을 추가하거나 동적 프로퍼티를 참조하고 싶을 때가 있습니다.  
이 경우 JSX에서 중괄호를 사용하여 JavaScript로 창을 열 수 있습니다.

## 학습 내용

- 따옴표로 문자열을 전달하는 방법
- 중괄호를 사용하여 JSX 내에서 JavaScript 변수를 참조하는 방법
- 중괄호를 사용하여 JSX 내에서 JavaScript 함수를 호출하는 방법
- 중괄호를 사용하여 JSX 내에서 JavaScript 객체를 사용하는 방법

### 따옴표로 문자열 전달하기

JSX에 문자열 속성을 전달하려면, 작은따옴표 또는 큰따옴표로 묶습니다:

```javascript
export default function Avatar() {
  return (
    <img
      className="avatar"
      src="https://i.imgur.com/7vQD0fPs.jpg"
      alt="Gregorio Y. Zara"
    />
  );
}
```

![alt text](./image/image-25.png)

여기서 "https://i.imgur.com/7vQD0fPs.jpg" 및 "Gregorio Y. Zara"는 문자열로 전달됩니다.

하지만 src 또는 alt 를 동적으로 지정하려면 어떻게 해야 할까요? " 및 "를 { 및 }로 대체하여 JavaScript의 값을 사용할 수 있습니다:

```javascript
export default function Avatar() {
  const avatar = "https://i.imgur.com/7vQD0fPs.jpg";
  const description = "Gregorio Y. Zara";
  return <img className="avatar" src={avatar} alt={description} />;
}
```

![alt text](./image/image-26.png)

이미지를 둥글게 만들어주는 "avatar" CSS 클래스명 className="avatar"와 아바타라는 JavaScript 변수의 값을 읽는 src={avatar}의 차이점에 주목하세요.  
중괄호를 사용하면 마크업에서 바로 JavaScript로 작업할 수 있기 때문입니다!

### 중괄호 사용하기: JavaScript 세계를 들여다보는 창

JSX는 JavaScript를 작성하는 특별한 방법입니다.  
그것은 즉, 중괄호 { } 안에서 JavaScript를 사용할 수 있다는 의미입니다.  
아래 예시에서는 먼저 과학자의 이름인 name 을 선언한 다음 `<h1>`안에 중괄호와 함께 포함시켰습니다:

```javascript
export default function TodoList() {
  const name = "Gregorio Y. Zara";
  return <h1>{name}'s To Do List</h1>;
}
```

![alt text](./image/image-27.png)

name 값을 'Gregorio Y. Zara' 에서 'Hedy Lamarr'로 변경해 보세요.  
투두리스트의 제목이 어떻게 바뀌는지 보셨나요?

중괄호 사이에는 formatDate()와 같은 함수 호출을 포함하여 모든 JavaScript 표현식이 작동합니다:

```javascript
const today = new Date();

function formatDate(date) {
  return new Intl.DateTimeFormat("en-US", { weekday: "long" }).format(date);
}

export default function TodoList() {
  return <h1>To Do List for {formatDate(today)}</h1>;
}
```

![alt text](./image/image-28.png)

### 중괄호 사용 위치

<b>JSX 내부에서는 중괄호를 두 가지 방법으로만 사용할 수 있습니다:</b>

1. JSX 태그 안에 직접 텍스트로 사용: `<h1> {name}'s To Do List </h1>` 는 작동하지만 <{tag}>Gregorio Y. Zara's To Do List</{tag}> 는 작동하지 않습니다.

2. `=`기호 바로 뒤에 오는 속성: src={avatar}는 아바타 변수를 읽지만, src="{avatar}"는 문자열 "{avatar}"를 전달합니다.

### “이중 중괄호” 사용: JSX 내에서의 CSS 및 다른 객체

문자열, 숫자 및 기타 JavaScript 표현식 외에도 JSX로 객체를 전달할 수도 있습니다.  
객체는 중괄호로 표시할 수도 있습니다 예: `{ name: "Hedy Lamarr", inventions: 5 }`  
따라서 JSX에서 JS 객체를 전달하려면 다른 중괄호 쌍으로 객체를 감싸야 합니다. `person={{ name: "Hedy Lamarr", inventions: 5 }}`

JSX의 인라인 CSS 스타일에서 이것을 볼 수 있습니다.  
React에서는 인라인 스타일을 사용할 필요가 없습니다(대부분의 경우 CSS 클래스가 잘 작동합니다).  
하지만 인라인 스타일이 필요한 경우 `style` 어트리뷰트에 객체를 전달합니다:

```javascript
export default function TodoList() {
  return (
    <ul
      style={{
        backgroundColor: "black",
        color: "pink",
      }}
    >
      <li>Improve the videophone</li>
      <li>Prepare aeronautics lectures</li>
      <li>Work on the alcohol-fuelled engine</li>
    </ul>
  );
}
```

![alt text](./image/image-29.png)

backgroundColor 와 color 의 값을 바꿔보세요.

이렇게 작성하면 중괄호 안에 JavaScript 객체가 실제로 보이는 것을 확인할 수 있습니다:

```javascript
<ul style={
  {
    backgroundColor: 'black',
    color: 'pink'
  }
}>
```

다음에 JSX에서 {{ 와 }}를 볼 때,  
이는 JSX 중괄호 내부의 객체일 뿐이라는 점을 기억하세요!

### Pitfall | 함정

인라인 style 프로퍼티는 카멜케이스로 작성됩니다.  
예를 들어,

```javascript
 <ul style="background-color: black">은 컴포넌트에서
  <ul style={{ backgroundColor: 'black' }}> 으로 작성됩니다.
```

### JavaScript 객체와 중괄호로 더 재미있게 즐기기

여러 표현식을 하나의 객체로 이동하여  
중괄호 안에 있는 JSX에서 참조할 수 있습니다:

```javascript
const person = {
  name: "Gregorio Y. Zara",
  theme: {
    backgroundColor: "black",
    color: "pink",
  },
};

export default function TodoList() {
  return (
    <div style={person.theme}>
      <h1>{person.name}'s Todos</h1>
      <img
        className="avatar"
        src="https://i.imgur.com/7vQD0fPs.jpg"
        alt="Gregorio Y. Zara"
      />
      <ul>
        <li>Improve the videophone</li>
        <li>Prepare aeronautics lectures</li>
        <li>Work on the alcohol-fuelled engine</li>
      </ul>
    </div>
  );
}
```

![alt text](./image/image-30.png)

이 예제에서 person JavaScript 객체에는  
name 문자열과 theme 객체가 포함되어 있습니다:

```javascript
const person = {
  name: "Gregorio Y. Zara",
  theme: {
    backgroundColor: "black",
    color: "pink",
  },
};
```

컴포넌트는 다음과 같이 person의 값을 사용할 수 있습니다:

```javascript
<div style={person.theme}>
  <h1>{person.name}'s Todos</h1>
```

## 요약

이제 JSX에 대한 거의 모든 것을 알게 되었습니다:

- 따옴표 안의 JSX 속성은 문자열로 전달됩니다.
- 중괄호를 사용하면 JavaScript 로직과 변수를 마크업으로 가져올 수 있습니다.
- 중괄호는 JSX 태그 콘텐츠 내부 또는 속성의 = 바로 뒤에서 작동합니다.
- {{ 와 }} 는 특별한 구문이 아니라 JSX 중괄호 안에 들어 있는 JavaScript 객체입니다.
