# clsx란?

- 여러개의 css클래스 이름을 조건부로 깔끔하게 조합할 수 있게 도와주는 유틸리티 함수
- 동적으로 클래스명을 선정할 때 유용하다

## clsx와 classnames의 차이점

| 항목           | `clsx`                                | `classnames`                             |
| -------------- | ------------------------------------- | ---------------------------------------- |
| 목적           | 조건부로 CSS 클래스명을 깔끔하게 조합 | 동일                                     |
| 용량           | ✅ 더 작음 (0.3KB)                    | ❌ 약간 큼 (1KB 이상)                    |
| 속도           | ✅ 더 빠름 (최적화되어 있음)          | ❌ 느린 편은 아니지만 `clsx`보단 느림    |
| API 사용 방식  | `classnames`와 거의 동일              | 직관적이고 널리 사용됨                   |
| 설치           | `npm install clsx`                    | `npm install classnames`                 |
| 조건 처리 방식 | 동일 (`true/false`, 객체 등으로 가능) | 동일                                     |
| React 추천도   | ✅ Tailwind, Next.js에서 자주 사용    | 많이 쓰이긴 하지만 점점 `clsx`로 이동 중 |
| 유지보수 상태  | ✅ 더 활발함 (2024년 기준)            | 유지보수는 되지만 트렌드는 아님          |

## clsx 사용 예시

```jsx
import clsx from "clsx";

const Button = ({ isPrimary }) => {
  return (
    <button className={clsx("btn", isPrimary && "btn-primary")}>버튼</button>
  );
};
```

- isPrimary가 true일 경우 → class="btn btn-primary"
- false일 경우 → class="btn"

## 여러 조건 처리

```jsx
const isError = true;
const isDark = false;

const classes = clsx("base", isError && "error", isDark && "dark");
// 결과: "base error"
```

## 객체 방식 사용

```jsx
const classes = clsx({
  btn: true,
  "btn-primary": isPrimary,
  "btn-disabled": isDisabled,
});
```
