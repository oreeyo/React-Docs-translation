## 첫번째 컴포넌트  

컴포넌트들은 리액트의 핵심 개념 중 하나이다.  

컴포넌트들은 사용자 인터페이스 (UI)를 구축하는 기초이면서,  

리액트 여행을 시작하기에 완벽한 장소로 만들어준다.  

### 배우게 될 내용  

- 컴포넌트란 무엇인가?
- 컴포넌트들은 리액트 어플리케이션에서 무슨 역할을 하는가?
- 첫번째 리액트 컴포넌트를 작성하는 방법

## 컴포넌트 : UI 빌딩 블록  

웹에서 HTML을 사용하면 h1 태그 및 li 태그와 같은 내장된 세트 태그들을    사용해서 풍부한 구조화된 문서들을 만들 수 있다.  

```jsx
<article>
  <h1>My First Component</h1>
  <ol>
    <li>Components: UI Building Blocks</li>
    <li>Defining a Component</li>
    <li>Using a Component</li>
  </ol>
</article>
```

이런 마크업은 아티클을 article 태그, 제목을 h1 태그, 그리고 축약된 목차를 순서가 지정된 목록 ol 태그로 나타낸다  

이와같이 마크업은 스타일을 위한 css, 상호작용을 위한 자바스크립트와 결합된 이러한 마크업은  
웹에서 볼 수 있는 모든 사이드바, 아바타, 모달, 드롭다운 등 ui 의 모든 부분 뒤에 있다.  

React를 사용하면 마크업, CSS 및 JavaScript를 앱의 재사용 가능한 UI 요소인 사용자 정의 "구성 요소"로 결합할 수 있습니다.   위에서 본 목차 코드는 모든 페이지에서 렌더링 될 수 있는 `<TableOfContents/>`  컴포넌트로 바뀔 수 있습니다.  

내부적으로는 여전히 같은 HTML 태그 `<article>`, `<h1>` 등을 사용합니다.  

HTML 태그와 마찬가지로 구성요소를 구성, 정렬, 밑 중첩해서 전체 페이지를 디자인 할 수 있다.  

예를 들어서, 읽고있는 문서 페이지는 리액트 컴포넌트로 구성되어져 있다.  

```jsx
<PageLayout>
  <NavigationHeader>
    <SearchBar />
    <Link to="/docs">Docs</Link>
  </NavigationHeader>
  <Sidebar />
  <PageContent>
    <TableOfContents />
    <DocumentationText />
  </PageContent>
</PageLayout>
```

프로젝트가 커지면서, 많은 디자인들이 이미 작성해서 재사용할 수 있는 컴포넌트들로 구성되어져있고,   

개발 속도를 올려줄 수 있다는 걸 알아차릴거다.  위의 목차는 <TableOfContents />를 사용하여 어떤 화면에도 추가할 수 있습니다!  

Chakra UI 및 Material UI와 같은 React 오픈 소스 커뮤니티에서 공유하는 수천 개의 구성 요소를 사용하여 프로젝트를 시작할 수도 있습니다  

## 컴포넌트 정의하기  

전통적으로 웹페이지를 만들 때, 웹 개발자는 콘텐츠를 마크업 하고 일부 자바스크립트를 뿌려서   

상호작용을 추가한다.  

이것은 웹에서 상호작용이 있으면 좋을 때, 훌륭하게 작동한다.  

이제 많은 사이트와 모든 앱에서 예상됩니다.  

React는 같은 기술을 사용하면서도 상호작용을 최우선으로 생각합니다. React 구성요소는 마크업을 뿌릴 수 있는 JavaScript 함수입니다  

그 모습은 다음과 같다. (아래 예시를 편집 할 수 있음.)  

```jsx
export default function Profile() {
  return (
    <img
      src="https://i.imgur.com/MK3eW3Am.jpg"
      alt="Katherine Johnson"
    />
  )
}

```

![alt text](./image/image-11.png)

구성요소를 작성하는 방법은 다음과 같다.  

### 스텝 1 : 컴포넌트를 내보내라  

export default 프리픽스는 표준 자바스크립트 문법이다.(리액트에 한정된게 아니라.)  

한 파일안에 메인 함수를 표시하게 해주고 메인함수를 다른 파일에서 불러올 수 있게 한다.  

(컴포넌트 가져오기와 내보내기에 대해서 더 자세히 알아보세요 !)  

### 스텝 2 : 함수 정의해라  

function Profile() {} 를 사용하면, Profile 이라는 이름을 가진 자바스크립트 함수를 정의할 수 있다.  

```jsx
함정!

**React 구성 요소는 일반 JavaScript 함수이지만** 

**이름은 대문자로 시작해야 하며 그렇지 않으면 작동하지 않습니다!**
```

### 스텝 3 : 마크업 추가하기  

컴포넌트는 src 및 alt 속성이 포함된 <img /> 태그를 반환합니다.  

<img />는 HTML처럼 작성되었지만 실제로는 JavaScript입니다!  

이 구문을 JSX라고 하며 이를 사용하면 JavaScript 내에 마크업을 삽입할 수 있습니다.  

반환문은 이 컴포넌트 처럼 한줄로 작성될 수 있습니다.  

```jsx
return <img src="https://i.imgur.com/MK3eW3As.jpg" alt="Katherine Johnson" />;
```

하지만 마크업이 모두 return 키워드와 같은 줄에 있지 않으면 이를 괄호 쌍으로 묶어야 합니다.  

```jsx
return (
  <div>
    <img src="https://i.imgur.com/MK3eW3As.jpg" alt="Katherine Johnson" />
  </div>
);
```

```jsx
함정 !
괄호가 없으면 return 이후 줄의 모든 코드는 무시됩니다!
```

## 컴포넌트 사용하기  

Profile 컴포넌트를 정의해뒀으니, 다른 컴포넌트 안에 중첩 시킬 수 있다.  

예를들어서, 여러 Profile 컴포넌트들을 사용한 Gallery 컴포넌트를 내보낼 수 있다.  

```jsx
function Profile() {
  return (
    <img
      src="https://i.imgur.com/MK3eW3As.jpg"
      alt="Katherine Johnson"
    />
  );
}

export default function Gallery() {
  return (
    <section>
      <h1>Amazing scientists</h1>
      <Profile />
      <Profile />
      <Profile />
    </section>
  );
}

```
![alt text](./image/image-12.png)

## 브라우저가 보는 것은 뭘까?  

대소문자의 차이점을 알아야한다.  

- <section> 은 소문자이고, 소문자는 리액트가 우리가 HTML 태그를 사용하는걸로 간주한다.
- <Profile /> 태그는 대문자 P로 시작하고, 리액트는 이를 우리가 Profile 이라 불리는 컴포넌트를 사용하는걸로 간주한다.

그리고 Profile에는\ 더 많은 HTML(<img />)이 포함되어 있습니다.  

결국 브라우저에는 다음과 같은 내용이 표시됩니다.  

```jsx
<section>
  <h1>Amazing scientists</h1>
  <img src="https://i.imgur.com/MK3eW3As.jpg" alt="Katherine Johnson" />
  <img src="https://i.imgur.com/MK3eW3As.jpg" alt="Katherine Johnson" />
  <img src="https://i.imgur.com/MK3eW3As.jpg" alt="Katherine Johnson" />
</section>
```

## 컴포넌트들을 중첩시키고 구성시키는 것.  

컴포넌트는 일반 JavaScript 함수이므로 동일한 파일에 여러 컴포넌트를 유지할 수 있습니다.  

이는 컴포넌트가 상대적으로 작거나 서로 밀접하게 관련되어 있는 경우 편리합니다.  

이 파일이 복잡해지면 언제든지 Profile을 별도의 파일로 이동시킬 수 있습니다.  

import에 관한 페이지에서 이 작업을 수행하는 방법을 곧 배우게 됩니다.  

Profile 컴포넌트는 갤러리 내에서 여러 번 렌더링되기 때문에   

Gallery가 부모 컴포넌트이며 각각의 Profile을 ”자식”으로 렌더링한다고 말할 수 있습니다.  

이것이 React의 마법 중 일부입니다.   

컴포넌트를 한 번 정의하면 원하는 만큼 여러 장소에서 사용할 수 있습니다.  

```jsx
## 함정 !

구성 요소는 다른 구성 요소를 렌더링할 수 있지만 정의를 중첩해서는 안 됩니다.

export default function Gallery() {
  // 🔴 Never define a component inside another component!
  function Profile() {
    // ...
  }
  // ...
}

위의 스니펫은 매우 느리고 버그를 유발합니다. 대신 최상위 수준에서 모든 구성요소를 정의하세요.

export default function Gallery() {
  // ...
}

// ✅ Declare components at the top level
function Profile() {
  // ...
}

자식 컴포넌트에 부모 컴포넌트의 일부 데이터가 필요한 경우, 중첩 정의 대신 props로 전달하세요.
```

*Deep Dive  

### 컴포넌트의 모든 것  

```bash
React 애플리케이션은 "루트" 컴포넌트에서 시작됩니다. 
일반적으로 새 프로젝트를 시작하면 자동으로 생성됩니다. 
예를 들어 CodeSandbox를 사용하거나 
Next.js 프레임워크를 사용하는 경우 
Root 컴포넌트는 pages/index.js 에 정의됩니다.

버튼과 같이 재사용 가능한 부분뿐만 아니라 
사이드바, 목록, 그리고 궁극적으로 전체 페이지와 같은 더 큰 부분에도 컴포넌트를 사용하게 됩니다! 
컴포넌트는 한 번만 사용되더라도 UI 코드와 마크업을 정리하는 편리한 방법입니다.

React 기반 프레임워크들은 이를 한 단계 더 발전시킵니다. 
빈 HTML 파일을 사용하고 React가 JavaScript로 페이지 관리를 “대행”하도록 하는 대신, 
React 컴포넌트에서 HTML을 자동으로 생성하기도 합니다. 
이를 통해 JavaScript 코드가 로드되기 전에 앱에서 일부 콘텐츠를 표시할 수 있습니다.

그렇지만 여전히 많은 웹사이트는 React를 약간의 상호작용을 추가하는 용도로만 사용합니다. 
이러한 웹사이트에는 전체 페이지에 
하나의 root 컴포넌트가 아닌 
여러 개의 root 컴포넌트가 있습니다. 
필요한 만큼 React를 많이 또는 적게 사용할 수 있습니다.
```

## 요약  

이제 막 React를 처음 사용해 보셨습니다! 몇 가지 핵심 사항을 요약해 보겠습니다.  

- 리액트를 사용하면 어플리케이션에서 재사용 가능한 UI 요소인 컴포넌트들을 만들 수 있다.
- 리액트 어플리케이션에서 모든 UI 조각들은 컴포넌트이다.
- 리액트 컴포넌트들은 일반적인 자바스크립트 함수이다. 몇가지를 제외하고.
    - 리액트 컴포넌트의 이름은 항상 대문자로 시작한다.
    - 리액트 컴포넌트는 JSX 마크업을 리턴한다.