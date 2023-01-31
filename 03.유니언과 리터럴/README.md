## 유니언과 리터럴

### 유니언

- _유니언_ : 값에 허용된 타입을 두 개 이상의 가능한 타입으로 확장하는 것

```typescript
let randomNum = Math.random() > 0.5 ? undefined : 'String';
```

위 코드에서 randomNum 변수는 undefined 혹은 string이다.
위와 같이 두 개 이상의 가능한 타입을 유니언 타입이라고 한다.

```typescript
let thinker: string | null = null;
if (Math.random() > 0.5) {
  thinker = 'Samsung';
}
```

위와 같이 사용하면 초기값이 null로 설정된 thinker 변수에 추 후 잠재적으로 string이 될 수 있음을 알려줄 수 있다.

> 유니언 타입의 순서는 중요하지 않다.

### 유니언에서의 속성

```typescript
let randomNum = Math.random() > 0.5 ? 3 : 'String';
randomNum.toString(); // 가능

randomNum.toUpperCase(); //불가능
randomNum.toFixed(); // 불가능
```

위 예제에서 randomNum 변수는 string | number 유니온 타입을 갖는다.
유니온 타입을 가질때 그 멤버함수에 접근하려면 두 타입 모두에 포함된 멤버만 접근 할 수 있다.

### 내로잉

- _내로잉_ : 값에 허용된 타입이 하나 이상의 가능한 타입이 되지 않도록 좁히는 것

```typescript
let fixa: number | string;
fixa = 'bay';
fixa.toUpperCase();
```

위와 같이 fixa라는 변수에 string 타입을 직접 할당하면 타입스크립트는 fixa 변수가 string 타입임을 알게 되며 이 때 내로잉이 발생하게 됩니다.

### 리터럴 타입

```typescript
const milk = 'hot';
```

위 예제 코드에서 milk는 string type으로 보이고 실제로도 그러합니다.
하지만 실제 마우스를 올려보면 타입스크립트는 string 이 아닌 hot 타입의 변수라는 것을 알려줍니다. hot은 문자열 이므로 문자열 타입이 맞지만 그 보다 더 구체적인 hot이라는 타입이 지정됩니다. *특정 원시값*으로 타입을 지정하는 것 그것이 바로 리터럴 타입 입니다.

### 타입 별칭

```typescript
type many = boolean | number | string | null | undefined;

let randomType: many;
```

타입 별칭은 타입이 복잡해지거나 많아질때 사용할 수 있다.
