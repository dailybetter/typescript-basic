## Fuction Overloading

함수에 대한 다양한 시그니처(signature)를 정의하여 동일한 이름을 가진 함수가 다른 매개변수를 사용하여 호출될 수 있도록 하는 기능

쉽게 생각하면 함수에 들어오는 인자에 따라 시그니처(매개변수와 반환값의 유형)을 달리 해주는 것이다.

```typescript
function add(x: number, y: number): number;
function add(x: string, y: string): string;

function add(x: number | string, y: number | string): number | string {
  if (typeof x === "number" && typeof y === "number") {
    return x + y;
  } else {
    return x.toString() + y.toString();
  }
}
```

- function 키워드로만 함수 오버로딩을 작성 할 수 있고 arrowfunction으로는 오버로딩 할 수 없다.

- 함수의 이름은 같아야한다.
- 매개변수의 개수가 다를 때 그 순서를 지켜줘야 한다.
