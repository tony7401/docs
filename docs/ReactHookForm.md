# React Hook Form 소개

- React에서 폼(form)을 쉽게 관리하기 위한 라이브러리
- 성능 최적화, UX & 개발자 경험(DX)을 고려해 만들어짐
- 기본 HTML 폼 유효성 검사 지원
- Yup, Zod 등 다양한 유효성 검사 라이브러리와 연동 가능

---

# 주요 특징

## 1.성능이 좋다

- 렌더링을 최소화한다
- 입력값이 바뀌어도 전체 폼이 다시 렌더링되지 않아서 속도가 빠르다
- 내부적으로 상태를 숨겨진 방식으로 관리해서 성능이 좋다

## 2. 기본 HTML 폼 유효성 검사도 쓸 수 있다

- input required /> 같은 기본 브라우저 검사를 그대로 쓸 수 있다
- 그외에도 minLength, pattern 같은 속성도 인식한다

## 3. UI라이브러리랑 바로 연결 가능하다

- MUI, Ant Design, Chakra UI같은 컴포넌트 라이브러리와 쉽게 연동된다
- Controller 라는 걸 쓰면, 외부 UI컴포넌트도 react-hook-form에서 제어 가능하다

## 4. 작고 가볍다

- 다른 라이브러리처럼 큰 종속성이 없다 ( 다른 라이브러리를 설치할 필요가 없다)
- 전체 라이브러리 크기도 매우 작아서 프로젝트 전체에 부담을 주지 않는다

## 5. 다양한 유효성 검사 라이브러리와 호환된다

---

# react-hook-form 훅에서 사용하는 기본적인 도구들

- register : input을 등록해서 값을 추적하는 것
- handleSubmit : 제출시 유효성 검사 + onSubmit 실행
- formState.errors : 유효성 검사 실패시 나타내는 에러 정보
- watch : input을 실시간으로 감지
- reset : form을 초기 값으로 리셋
- setValue : 특정 필드 값을 수동 설정
- getValues : 현재 모든 필드 값 가져오기

# react-hook-form 훅에서 사용하는 심화 도구들

- control : controller와 함께 쓰는 제어 컴포넌트용
- trigger : 특정 필드 유효성 검사 수동 실행
- setError : 수동으로 에러 메세지 실행
- clearErrors : 에러메세지 제거
- resetField : 특정필드 초기화
- unregister : 특정필드 초기화 중지

## control

- control은 React Hook Form에서 외부 UI같은 컴포넌트와 연동할 때 필수적으로 사용하는 객체다
  MUI, React Select, Date Picker 같은 컴포넌트는 ref를 직접 지원하지 않는다. register 대신 control + controller를 사용해 연결한다
- field는 value, onChange, onBlur, name, ref 속성을 포함

# 기본 사용법 예제

```jsx
import React from "react";
import { useForm } from "react-hook-form";

const FormExample = () => {
  const {
    register,
    handleSubmit,
    formState: { errors },
  } = useForm();

  const onSubmit = (data) => {
    console.log("제출 성공:", data);
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input
        {...register("name", {
          required: "이름은 필수입니다.",
          minLength: { value: 2, message: "최소 2자 이상 입력해주세요." },
        })}
        placeholder="이름"
      />
      {errors.name && <p style={{ color: "red" }}>{errors.name.message}</p>}

      <input
        {...register("email", {
          required: "이메일은 필수입니다.",
          pattern: {
            value: /^[^\s@]+@[^\s@]+\.[^\s@]+$/,
            message: "유효한 이메일을 입력하세요.",
          },
        })}
        placeholder="이메일"
      />
      {errors.email && <p style={{ color: "red" }}>{errors.email.message}</p>}

      <button type="submit">제출</button>
    </form>
  );
};

export default FormExample;
```

# control 사용법 예제

```jsx
import { useForm, Controller } from "react-hook-form";
import Select from "react-select";

const MyForm = () => {
  const { control, handleSubmit } = useForm();

  const onSubmit = (data) => console.log(data);

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <Controller
        name="fruit"
        control={control}
        rules={{ required: true }}
        render={({ field }) => (
          <Select
            {...field}
            options={[
              { value: "apple", label: "Apple" },
              { value: "banana", label: "Banana" },
            ]}
          />
        )}
      />
      <button type="submit">제출</button>
    </form>
  );
};
```
