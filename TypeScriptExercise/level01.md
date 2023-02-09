## Exercise 01

### 내가 짠 코드 

```typescript

export type User = {name: string, age: number, occupation: string};

export const users: User[] = [
    {
        name: 'Max Mustermann',
        age: 25,
        occupation: 'Chimney sweep'
    },
    {
        name: 'Kate Müller',
        age: 23,
        occupation: 'Astronaut'
    }
];

export function logPerson(user: User) {
    console.log(` - ${user.name}, ${user.age}`);
}

console.log('Users:');
users.forEach(logPerson);
```

문제? 의 설명에 따르면 interface 를 적용해서 에러를 해결하라고 되어있었는데
초기에 제시된 코드에는 type alias 로 선언이 되어있었는데 interface로 굳이
바꿀 필요 없다고 생각되어 그대로 진행했고 문제를 해결할 수 있었다.

추가적으로 인터페이스와 type alias의 차이에 대해 공부를 해보면 좋을 것 같다.