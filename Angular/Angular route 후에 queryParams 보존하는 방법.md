​									Angular route 후에 queryParams 보존하는 방법 

------

다음과 같이 queryParamsHandling을 추가해준다.

```
this.router.navigate(['edit'], {relativeTo: this.route, queryParamsHandling: 'merge'})
```

