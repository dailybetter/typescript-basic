## 인터페이스

인터페이스는 객체 타입과 유사하지만 읽기 쉬운 오류 메시지, 더 빠른 컴파일 성능, 클래스와의 상호 운용성을 위해 더 선호 됩니다.

### 인터페이스와 객체 타입의 차이

- 인터페이스는 속성 증가를 위한 병합이 가능하다. 이 기능은 내장된 전역 인터페이스 또는 npm 패키지와 같은 외부 코드를 사용할 때 특히 유용하다.
- 인터페이스는 클래스가 선언된 구조의 타입을 확인하는 데 사용할 수 있다.
- 일반적으로 인터페이스는 타입 검사기가 더 빨리 작동한다.

### 읽기 전용 속성

인터페이스에는 readonly 키워드를 추가해 다른 값으로 설정 될 수 없음을 나타낼 수 있다.

```typescript

interface url {
  readonly text: string
}

url.text + = 'wow';
// Error: Cannot assign to 'text' becautse it is a read-only property
```

readonly 제한자는 타입시스템에만 존재하며 인터페이스에서만 사용 가능함.

### 인터페이스 확장

타입스크립트는 인터페이스가 다른 인터페이스의 모든 멤버를 복사해서 선언할 수 있는 확장된 인터페이스를 허용한다. 이 때 extands 키워드를 사용하고 확장된 두 인터페이스 모두의 멤버를 갖는다.

```typescript
interface Song {
  title: string;
}

interface Hip extends Song {
  pages: number;
}

let Sing: Hip = {
  title: 'apple',
  number: 7,
}; // OK
```
