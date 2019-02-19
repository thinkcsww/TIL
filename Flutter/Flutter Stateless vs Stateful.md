​										**Flutter Stateless vs Stateful**

------

Stateless, Stateful Widget은 멤버 변수가 변하면 Rerender가 되고 새로운 Instance를 생성한다. 그런데 두 위젯의 차이는 새로운 Instance에 State가 적용되느냐 아니냐에 차이가 있다.

1. Stateless는 말 그대로 State가 없다. -> Rerender가 되면 변수의 초기값으로 랜더링 되기 때문에 값을 바꾸어도 계속 초기값만 보여준다.
2. Stateful은 state가 있다. -> Rerender가 되면 state에 저장된 값을 할당해서 값을 계속해서 바꿀 수 있다.

