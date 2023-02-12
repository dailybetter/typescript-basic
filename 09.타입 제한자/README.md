## 타입 제한자

### top 타입

top타입은 시스템에서 가능한 모든 값을 나타내는 타입이다.
모든 타입은 top타입에 할당할 수 있다.

### any 타입 다시 보기

any 타입은 console.log 처럼 모든 데이터 타입을 받는 위치에 사용 된다.
하지만 any 타입을 적용하면 타입검사를 실행하지 않기 때문에 타입스크립트의 유용성이 줄어든다는 문제점이 있다. 이와 같은 상황에서 어쩔 수 없이 any 타입을 써야한다면 unknown 타입을 고려하는 것이 좋다.

- 타입 스크립트는 unknown 타입 값의 속성에 직접 접근할 수 없다.
- unknown 타입은 top 타입이 아닌 타입에는 할당할 수 없다.

```typescript

function Happy(day: unknown){
    console.log(day.toUpperCase());
    //Error: Object is 'unknown' type
}
```
타입스크립트가 unknown 타입에 접근할 수 있는 방법은 instanceof나 typeof, 타입 어셔션을 사용하여 타입을 제한 하는 것이다.

### 타입 서술어

```typescript

//Case: A

function isNumOrStr(v: unknown){
    return['number','string'].includes(typeof v)
    // type이 number 혹은 string 값을 가지는지 boolean 값을 반환하는 함수

//Cae: B
functin isStrOrNum(v: unknown): v is number | string{
    return['number','string'].includes(typeof v)
}
// type 서술어를 통해 타입 추론이 가능하게 한다.
}
```

타입 서술어는 속성이나 값의 타입을 확인하는 것 이상을 수행해 잘못 사용하기 쉬우므로 가능하면 피하는것이 좋다.

### 타입 연산자


```typescript
function Puppy(rating: V, key: keyof Ratings)