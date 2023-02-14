## 제너릭

여기 들어오는 input 타입에 따라 반환되는 return 의 타입이 달라지는 함수가 있다.


```typescript
function passage(input) {
    return input
}

passage(123)
passage('qqq')

```

이 경우 input 타입과 return 타입간의 관계를 말할 수 있는 방법이 필요고 타입스크립트는 제네릭(generic)을 사용해 타입 간의 관계를 알아낼 수 있다.

타입 매개변수는 전형적으로 T나 U 같은 단일 문자 이름 또는 Key 와 Value 같은 파스칼 케이스 이름을 갖는다.


```typescript
function passage<T>(input: T) {
    return input
}

passage(123) //타입 123
passage('qqq') // 타입 'qqq'



// 화살표 함수에서 제너릭

const  passage = <T>(iput: T) => input;
passage(123) // type: 123
```

| 제너릭 화살표 함수 구문은 .tsx 파일에서 jsx 구문과 충돌가능성이 있다!