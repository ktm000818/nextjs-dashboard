Next.js 14 - app router ver.

this project is that covers below subjects.

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
 
Creating Layouts and Pages

Navigating Between Pages

Setting Up PostgreSQL on vercel

Fetching Data

Static / Dynamic Rendering

Streaming

Adding Search and Pagination

Mutating Data

Handling Errors

Improving Accessibility

Adding Authentication

Adding Metadata
