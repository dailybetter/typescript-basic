## 함수

### 필수 매개변수

js 에서는 인수의 수와 상관없이 함수를 호출할 수 있다. 하지만 ts 에서는 함수에 선언된 모든 매개변수가 필수라고 가정한다. 함수가 잘못된 수의 인수로 호출 되면 타입오류가 나온다.

### 선택적 매개변수

js 에서는 매개변수가 제공되지 않으면 함수 내부의 인수값이 undefined로 기본 설정 된다. ts 에서도 이와 같이 선택적으로 매개변수를 받을 수 있다.

```typescript

const tennis = (ball : string power ?: boolean) => {
  console.log(ball)
  if(power){
    console.log(power)
  }
}
```

위 예제에서 power는 boolean | undefined 타입으로 시작하여 if 문을 만나 boolean으로 타입 내로잉이 진행 된다.

> 선택적 매개변수는 맨 마지막에 나와야 한다.
> 필수 매개변수가 먼저 나오고 선택적 매개변수가 나와야 한다.

### 나머지 매개변수

js 에서는 스프레드 연산자를 활용하여 나머지 인수를 나타낼 수 있고 ts에서도 이와 유사하게 나머지 인수를 받을 수 있다.

```typescript
function lucky(time: number, ...me: string[]) {
  console.log(time);
}
```

### 명시적 반환 타입

함수에서 반환 타입을 명시적으로 선언하는 방식이 유용할 때도 있다.

- 가능한 반환값이 많은 함수가 항상 동일한 타입의 값을 반환하도록 강제할 수 있다.
- 타입스크립트는 재귀 함수의 반환 타입을 통해 타입을 유추하는 것을 거부한다.
- 수백 개 이상의 타입스크립트 파일이 있는 매우 큰 프로젝트에서 타입스크립트 타입 검사 속도를 높일 수 있다.

### 반환 타입을 지정하는 위치

- function키워드를 쓴 함수의 경우

```typescript
function lucky(time: number, ...me: string[]): srting {
  console.log(time);
}
```

- 화살표 함수의 경우

```typescript
const tennis = (ball : string power ?: boolean): string => {
  console.log(ball)
  if(power){
    console.log(power)
  }
}
```

### 함수 타입

함수의 타입을 선언하는 방법

```typescript
const input: (ball: string[], count?: number) => number;
```

위의 예제코드는 string[] 타입을 갖는 ball 인자와 number 값을 가질 수 있는 count 선택적 매개변수를 갖는 number 타입을 반환하는 함수임을 나타낸다.

### void반환 타입

함수 타입을 선언할 때 void를 사용하면 함수에서 반환되는 값이 무시된다.

### never 반환 타입

never 반환 함수는 의도적으로 항상 오류를 발생시키거나 무한 루프를 실행하는 함수를 말한다.

> nerver는 void와 다르다 void는 아무것도 변환하지 않는 함수를 위한 것이고 never 는 절대 반환하지 않는 함수를 위한 것 이다.

### 함수 오버로드
하나의 최종 구현 시그니처와 그 함수의 본문 앞에 서로 다른 버전의 함수 이름, 매개변수, 반환 타입을 여러 번 선언한다.

오버로드된 함수 호출에 대해 구문 오류를 생성할지 여부를 결정할 때 타입스크립트는 함수의 오버로드 시그니처만 확인한다.

```typescript
// 오버로드 시그니처
function createDate(time : number): Date;
function createDate(month: number, day: number, year: number): Date;

// 구현 시그니처
function createDate(second: number, day?:number, year?: number){
  if(second === day && day === year){
    console.log('binggo!')
  }
}

createDate(1234) // 됨
createDate(1,1,2023) // 됨

createDate(1,2) //안됨
```
> 함수 오버로드는 복잡하고 설명하기 어려운 함수 타입에 사용하지만 가능하면 사용하지 않는 것이 좋다.
