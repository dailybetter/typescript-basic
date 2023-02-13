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

### keyof 연산자

keyof 연산자는 객체 유형을 사용하여 문자열 또는 숫자 키의 리터럴 조합을 생성한다. 즉 객체의 키값만 따로 빼서 가져다 쓰고싶을 때 사용하는 연산자 라고 볼 수 있다.
아래 예시를 보면 keyof 연산자를 사용하지 않을 때 key 값에 일일이 유니언타입으로 타입을 지정해줘야하지만 keyof 연산자를 사용하면 더 간편하게 타입지정이 가능하다.


```typescript
const ratings: Ratings = {dog: 100 , cat: 100}

function pet(rating: V key: 'dog' | 'cat'): number {
    return rating[key]
}
function Puppy(rating: V, key: keyof Ratings): number {
    return ratings[key]
}

```


### typeof 연산자

typeof는 js 에서 값이 어떤 타입인지 반환할 때 사용되지만 ts 에서는 값의 타입을 반환하는 용도로 쓰인다.
js typeof와 달리 컴파일된 js 에서 나타나지 않는다.



### keyof & typeof 연산자

```typescript

const puppy = {
    dog: 'bow',
    cat: 'miow'
};

function pickoneOfThem(key: keyof typeof puppy){
    console.log(key)
}

pickoneOfThem('cat') // OK
pickoneOfThem('hamster') // Error: Argument of type 'hamster' is not assignable
```

### 타입어서션(type assertion)

타입 주장? 단언?

**as** 키워드를 사용하면 타입 어셔선을 사용하여 타입을 지정해 줄 수 있다. 예를 들어 JSON.parse의 경우 의도적으로 any타입을 반환하는데 이 때 타입 어서션을 통해 반환된 값의 타입을 지정해 줄 수 있다.

```typescript

JSON.parse('king'); // type: any

JSON.parse('hyunwoo') as string // type: string

JSON.parse('ME') as string[] // type: string[]

```

| 이전 라이브러리나 코드로 작업한는 경우 item as type 대신 <type>item 같은 캐스팅 구문을 볼 수 있으나 이 구문은 jsx 구문과 호환되지 않고, .tsx파일에서도 작동하지 않기 때문에 권장하지 않는다.



### non-null 어서션

null 또는 undefined 가 아니다 라는 표현을 사용 할 때 non-null  어서션을 사용할 수 있으며 ! 로 대체  가능하다.

```typescript

let random = Math.random() > 0.5 ? undefined : 1

random as number // number로 간주 됨
random!; // undefined 가 아니라고 간주됨.
```
non-null 어서션은 undefined 값을 반환할 가능성이 있는 api 등에서 유용하게 쓰일 수 있다


### 어서션 사용시 주의 사항

타입 어서션은 타입스크립트에 타입 검사 중 일부를 건너뛰도록 명시적으로 지시하기 때문에 타입 어서션을 많이 사용하는 것 보다 타입 애너테이션을 사용하여 변수 타입을 선언하는 것이 더 바람직하다.


### const 어서션

const 어서션은 배열, 원시 타입, 값, 별칭 등 모든 값을 상수로 취급해야 함을 나타내는 데 사용한다. 특히 as const는 수신하는 모든 타입에 다음 세 가지 규칙을 적용한다.

- 배열은 가변 배열이 아니라 읽기 전용 튜플로 취급 된다.
- 리터럴은 일반적인 원시 타입과 동등하지 않고 리터럴로 취급된다.
- 객체의 속성은 읽기 전용으로 간주 된다.

```typescript

// 리터럴 예시

const Myfriend = () => 'dog'; // type: string

const Myfriday = () => 'honey' as const //type: 'honey'

```