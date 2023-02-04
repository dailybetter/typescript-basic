## 배열

js 에서 배열은 매우 유연한 특징을 가지기 때문에 하나의 배열 안에 모든 타입의 값을 혼합해서 저장할 수 있다. 하지만 이런 방식으로 배열을 사용하는 것은 권장 되지 않는다. 배열을 읽을 때 혼란을 야기할 수 잇기 때문이다.

타입스크립트는 초기 배열에 어떤 데이터 타입이 있는지 기억하고, 배열이 해당 데이터 타입에서만 작동하도록 제한한다.

```typescript
const arr = ['I', 'My', 'Me', 'Mine'];

arr.push('You'); // OK

arr.push(true);
//Error: Argument of type 'boolean' is not assignable to parameter of type 'string'
```

### 배열 타입 어노태이션

```typescript
const arr: number[];
arr = [1, 2, 3, 4, 5];
```

### 배열과 함수 타입

```typescript
// 타입은 number 배열을 반환하는 함수
const arr: () => number[];
// 타입은 각각의 number를 반환하는 함수 배열
const featArr: (() => number)[];
```

### 다차원 배열 타입

```typescript
const arr: number[][];
arr = [[1, 2, 3, 4, 5]];
```

### 주의사항: 불안정한 멤버

js 에서 배열의 길이보다 큰 인덱스에 접근하면 undefined를 제공한다.
하지만 ts에서는 배열의 길이보다 큰 인덱스에 접근하더라도 타입 오류를 제공하지 않는다.

```typescript
const arr = [1, 2, 3, 4, 5];

console.log(arr[999]); // 타입 오류 없음
```
