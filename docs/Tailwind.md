# 🌬️ Tailwind CSS 발표자료

## 1. Tailwind CSS란?

**Tailwind CSS**는 유틸리티 퍼스트(Utility-First) CSS 프레임워크입니다.  
HTML에서 직접 스타일을 조합하여 빠르고 일관된 UI를 만들 수 있습니다.

---

## 2. 주요 특징

- **유틸리티 기반 클래스**

  - 예: `bg-blue-500`, `text-xl`, `p-4`
  - CSS 파일 없이 HTML에 클래스만으로 디자인 가능

- **빠른 개발 속도**
- 복잡한 CSS 작성 없이 UI 구성

- **반응형 지원**

  - `sm:`, `md:`, `lg:` 접두어로 반응형 UI 간편 구현

- **JIT(Just-In-Time) 모드**

  - 실제 사용하는 CSS 클래스만 빌드 → 성능 최적화

- **작은 번들 사이즈**
- 사용하지 않는 스타일 제거(Purge 기능)

---

## 3. 설치 및 설정 방법

### 설치

```bash
npm install -D tailwindcss
npx tailwindcss init -p
```

## taiwind.config.js 설정

```js
module.exports = {
  content: ["./src/**/*.{js,jsx,ts,tsx}"],
  theme: {
    extend: {},
  },
  plugins: [],
};
```

## index.css에 Tailwind 지시어 추가

@tailwind base;
@tailwind components;
@tailwind utilities;

### 예제코드

```jsx
<button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
  클릭하세요
</button>
```

- bg-blue-500 → 배경색

- hover:bg-blue-700 → 마우스 올렸을 때 색 변경

- text-white → 글자색 흰색

- py-2 px-4 → 안쪽 여백

- rounded → 모서리 둥글게

## 반응형 디자인

```jsx
<h1 class="text-base md:text-lg lg:text-2xl">반응형 텍스트입니다.</h1>
```

text-base → 기본 크기

md:text-lg → 중간 화면 이상에서 크기 변경

lg:text-2xl → 더 큰 화면에서 더 크게

### tailwindcss 와 기존 css의 차이점

| 항목        | Tailwind CSS         | 기존 CSS 방식              |
| ----------- | -------------------- | -------------------------- |
| 스타일 방식 | 유틸리티 클래스 조합 | CSS 클래스 선언/사용       |
| 유지보수    | 중복 적고 명확       | 클래스 많아질수록 복잡해짐 |
| 속도        | 빠름                 | 상대적으로 느림            |
| 코드 위치   | HTML 안에 스타일     | HTML + CSS 따로 관리       |
