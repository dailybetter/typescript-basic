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

### 추상 클래스

abstract 키워드를 통해 클래스의 구현을 선언하지 않고 인터페이스 처럼 사용할 수 있다.

```typescript

abstract class School {
    readonly name: string;

    constructor(name: string) {
        this.name = name;
    }

    abstract getStudentTypes(): string[];
}

class Absence extends School {} // Error

school = new School('S'); // Error
```

### 멤버 접근성

- public(default) : 모든 곳에서 누구나 접근 가능
- protected: 클래스 내부 또는 하위 클래스에서만 접근 가능
- private: 클래스 내부에서만 접근 가능

이러한 키워드는 순수하게 타입 시스템 내에 존재합니다. 코드가 js로 컴파일 되면 다른 모든 타입 시스템 구문과 함께 키워드도 제거됩니다.

```typescript

class Base {
    isPublic = 0;
    public thisIsPublic = 1;
    protected isProtected = 2;
    private isPrivate = 3;
    #truePrivate =4;
}

class Sub extends Base {
    console.log(this.isProtected) // 접근 가능
    console.log(this.isPrivate) // 접근 불가능
    console.log(this.#truePrivate) // 접근 불가능
}

```

### 정적 필드 제한자

ts에서는 static 키워드를 단독으로 사용하거나 readonly와 접근성 키워드를 함께 사용할 수 있도록 지원한다.
함께 사용할 경우 접근성 키워드를 먼저 작성하고, 그다음 static, readonly 키워드를 쓴다.

``` typescript
class Example{
    protected static readonly answer: 'secret'
}
```
