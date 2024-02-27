Next.js 14 - app router ver.  
<a href="https://nextjs.org/learn/dashboard-app">https://nextjs.org/learn/dashboard-app<a>  

  아래 주제에 대해 공부한 내용을 기록합니다.

## CSS Styling
 - 전역 css를 추가하기 위해선 root 경로의 layout.tsx에 스타일을 추가.

## Optimizing Fonts and Images
 ### Optimize Fonts
 - Next.js는 next/font 모듈로 폰트 최적화를 수행한다. 빌드시 해당 폰트를 다운로드 받고 다른 정적 에셋과 함께 호스팅 하게 된다.
   이는 웹페이지 접근 후 폰트를 다운로드 하기 위한 추가적인 요청이 없다는 것을 의미한다.
   폰트를 최적화하게 되면 UX 개선이 가능해진다.
   폰트를 다운받고 적용하는 과정에서 발생하는 레이아웃 변경 현상으로 인한 서비스 오용, 깜빡임 등을 미연에 방지할 수 있게 된다.
 ### Optimize Images
 - Next.js는 또한 next/image 모듈로 이미지 최적화를 지원하고 있다. 현대 웹에서 중요하게 여겨지는 이미지 최적화 작업을 자동으로 진행한다.
   - 이미지 로드로 인한 레이아웃 변경 방지
   - 뷰포트에 맞추어 이미지 크기 조정
   - 뷰포트가 생긴 후 이미지 로드 (지연 로드)
   - WebP와 같은 최신 확장자로 이미지를 제공 (브라우저가 지원하는 경우)
 
## Creating Layouts and Pages
 ### Nested Routing
 - Next.js는 파일 시스템 라우팅을 사용한다. 폴더를 중첩하여 중첩 라우팅을 구현할 수 있다. ex) app/dashboard/invoices
 ### layout and page
 - layout.tsx와 page.tsx를 사용해 각 경로에 대한 UI를 지정할 수 있다.
 - page.tsx는 경로에 액세스 하려면 필수
 - 경로를 동작하게 만들기 위해선 폴더 내부에 page.tsx를 추가해야한다.
 - layout.tsx는 뼈대를 의미하기에 빠져서 안되고, page.tsx는 컴포넌트를 리턴하기 때문에 둘 다 존재하여야한다.
 - root 단위에 layout.tsx가 존재하면 하위 트리의 모든 페이지에서 동일한 layout을 공유한다.

## Navigating Between Pages
 ### Link component
  - 페이지를 연결하려면 일반적으로 <a/> 태그가 사용되지만 강제로 새로고침된다.
  - Next.js에선 Link 컴포넌트가 존재하며, 해당 컴포넌트가 브라우저의 뷰포트에 노출 될 때, 해당 Link 컴포넌트에 연결된 페이지를 prefetch한다.
  - Next.js는 경로 세그먼트 별로 자동으로 코드를 분할하고, Link 컴포넌트는 분할된 코드를 prefetch 한다고 이해하면 된다.

## Fetching Data
 - client Component에서 database query를 직접 호출해선 안된다. 데이터베이스의 비밀이 노출된다.
 - React Server Component에서 database query를 직접 호출해야한다.
 - 데이터 요청시 폭포 패턴은 상황에 맞게 사용해야한다. ex) 팔로워리스트 요청하기 전 사용자 정보 fetching
 - 모든 데이터 요청을 한꺼번에 실행하려면 Promise 객체의 내장 메서드인 all(), allSettled()를 사용하면 된다.
 ### RSC를 사용했을 때의 이점
  - Promise 지원
  - useEffect, useState나 데이터 패칭 라이브러리를 사용하지않아도 async/await 문법을 사용할 수 있다.
  - 서버 컴포넌트는 기본적으로 서버에서 실행되기 때문에 무거운 요청이나 로직을 서버에서 실행하고, 클라이언트에 전달해줄 수 있다. (성능상 우위)
  - api layer 없이 database query를 서버에서 직접 실행 할 수 있다.
   
## Static / Dynamic Rendering
 ### Static Rendering 
   - 정적 렌더링은 빌드(배포)시 서버에서 데이터 패칭과 렌더링이 실행되고, CDN에 배포 및 캐시될 수 있다.
   - 유저간 데이터 전송이 없는 정적 페이지에 유용하며, 블로그나 제품페이지에 맞는 방법이다.
   - 대시보드나 댓글창 등 지속적으로 리패칭해야하는 페이지같은 경우는 정적 렌더링보단 동적 렌더링이 맞는 방법이다.
 ### Dynamic Rendering
  - 동적 렌더링은 유저가 페이지에 접근했을 때, 데이터 패칭을 새로 하고, 렌더링이 새롭게 진행되고 나온 결과물을 전달해준다.
  - 유저 간 데이터 전송이 가능하고, 주기적으로 업데이트 해야하는 채팅 웹이나, 대시보드에 어울린다.
  - URL 검색 파라미터와 쿠키에 접근할 수 있다. 
### Streaming
 - Suspense 사용시 대체 UI를 제공하여 전체 로드 속도를 줄일 수 있다.
 - 데이터 패칭이 완료된 컴포넌트부터 사용자에게 제공할 수 있다.
 - 데이터를 패칭하는 부분을 스트리밍을 사용할 컴포넌트 내부로 이동시켜 Suspense 경계를 명확히 할 수 있다.

### Adding Search and Pagination
 - url parameter 사용시 북마크, 링크 공유가 가능하다.
 - 서버에서 렌더링을 진행할 때 url parameter로 초기 상태를 렌더링 할 수 있다.

### Mutating Data
 ## React Server Actions
  - 리액트 서버 액션이란, Next.js 개발시 보안을 위해 사용하는 서버 액션이다.
  - 'use server'을 함수 내에 작성함으로 활성화 시킬 수 있다.
  - <form/> 과 함께 사용시, actions 함수에 서버 액션을 활성화 함으로써 클라이언트의 자바스크립트가 비활성화 되어있어도 실행이 가능하다. (점진적 향상)
  - 서버 액션은 캐싱과도 긴밀하게 작동한다. form이 서버액션을 통해 양식을 제출하는 경우, 데이터를 변경할 수 있을 뿐만 아니라, revalidatePath, revalidateTag api를 통해 캐시를 재검증 할 수 있다.
  - revalidatePath() 함수에 url을 매개변수로 넘기면, 해당 경로에 대한 캐시를 지우고, 서버에 대한 새 요청을 트리거 한다.
[점진적 향상?]
  구형 브라우저 및 장치에서 웹사이트를 사용하는 사용자들에게 간단하지만 여전히 사용 가능한 환경을 제공하고, 사용자 경험을 개선하도록 디자인하는 설계 방법 (자바스크립트가 비활성화 되어있는 경우, 최신 브라우저에서만 동작하는 자바스크립트가 존재할 때 등의 상황에서 기능을 열어주고, 사용자 경험을 개선하는 방법 )
Handling Errors

Improving Accessibility

Adding Authentication

Adding Metadata
