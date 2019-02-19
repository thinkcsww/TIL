									**Bloc Provider Inherited Widget**

------

<h3>Bloc Provider Inherited 이해하기</h3>

<h6>전체 코드</h6>

```
import 'package:flutter/material.dart';
import 'bloc.dart';

class Provider extends InheritedWidget {
  final bloc = Bloc();

  @override
  bool updateShouldNotify(InheritedWidget oldWidget) => true;

  static Bloc of(BuildContext context) { 
    return (context.inheritFromWidgetOfExactType(Provider) as Provider).bloc;
  }
}
```

1. static Bloc of(BuildContext context)에서 Bloc은 return type, of는 함수 이름
2. Inherited Widget이 무엇인가?  
   Widget tree가 커지면 하단 부분의 위젯이 상단 부분 위젯의 property를 가져오려면 상당히 복잡한데, 
   Inherited Widget을 쓰면 최상단 부모 위젯의 property에  직접 접근할 수 있다.
3. (context.inheritFromWidgetOfExactType(Provider) as Provider).bloc 설명

```

1. context.inheritFromWidgetOfExactType(Provider)는 모든 parent context(parent의 parent들 까지)에서 InheritedWidget인 Provider라는 Exact한 Type의 클래스를 inherit 받는 것 as Provider class으로..
2. .bloc은 Provider class의 bloc 멤버를 가져오는 것
```

4. 사용방법
   MaterialApp의 HOC로 붙이기

1. ```
   import 'package:flutter/material.dart';
   import 'screens/login_screen.dart';
   import 'blocs/provider.dart';
   
   class App extends StatelessWidget {
     @override
     Widget build(BuildContext context) {
       return Provider(
         child: MaterialApp(
           title: 'Log Me In',
           home: Scaffold(
             body: LoginScreen(),
           ),
         ),
       );
     }
   }
   
   ```

   각 화면에서 사용법

   ```
   final bloc = Provider.of(context);
   ```

   