## 클래스

클래스 타입은 인터페이스와 유사한 모습을 갖는다.

```typescript

class WithValue {
    immediate = 0;
    later: number;
    maybe: number | undefined;
}
```
위의 예제를 보면 maybe프로퍼티는 number 또는 undefined 타입을 갖는다.
실제로 코딩을 할 때 maybe 값이  추후에 결정되거나 maybe 값이 할당 되기 전에 클래스를 선언해야 하는 경우 undefined 값이 되므로 undefined 인 상태에서도 class 를 사용하기 위해 위와 같은 코드를 작성한 적이 있지만 책에서는 가능하면 undefinend 나 null 값은 사용하지 않는게 좋다고 한다.

그렇다면 전에 설명한 상황에서는 어떤 방식을 써야 할까?

! 어서션을 사용하면 타입스크립트의 검사를 비활성화 할 수 있다.

```typescript

class WithValue {
    immediate = 0;
    later: number;
    maybe!: number ;
}
```
이렇게 하면 maybe 프로퍼티가 사용되기 전에 undefined 값이 할당 된다.
하지만 이런 방식은 타입 안정성에 좋지 않은 영향을 준다.

### ? 어서션( 선택적 속성 )

인터페이스와 마찬가지로 선언된 프로퍼티 이름 뒤에 ?를 추가해 선택적으로 선언할 수 있다.

```typescript

class WithValue {
    immediate = 0;
    later: number;
    maybe?: string ;
}

new WithValue().maybe?.length// 가능
new WithValue().maybe.length
//Error: Object is possibly 'undefined'

```
