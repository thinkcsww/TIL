​																			Angular Pipe

------

템플릿에서 사용자에게 보여주기전에 데이터에 간단한 가공을 할 수 있게 해주는 역할

1. ng g p <이름>으로 생성
2. 생성하면 app.module.ts에 추가되고 <이름>.pipe.ts로 파일이 생성된다.

3. PipeTransform interface를 사용한다.

4. Annotation prop에 pure를 false로 하면 pipe가 변경될 때 마다 랜더링을 다시한다 -> 성능에 문제가 될 수 있으므로 필요할 때만 사용한다.

5. 받는 parameter의 개수 제한은 없고 템플릿에서 다음과 같이 사용한다. 

   <pipe이름>:param1:param2… 

```
{{ server.started | date:'fullDate' | uppercase:list:box:hi  }}
```





```
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'filter',
  pure: false
})
export class FilterPipe implements PipeTransform {

  transform(value: any, filterString: string, propName: string): any {
    if (value.length === 0) {
      return value;
    }
    const resultArray = [];
    for (const item of value) {
      if (item[propName] === filterString) {
        resultArray.push(item);
      }
    }
    return resultArray;
  }

}

```

