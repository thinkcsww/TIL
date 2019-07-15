​																		Angular BehaviorSubject

------

Behavior Subject는 맨 마지막의 Data를 stream에서 가져오는 Subject이다. 그냥 Subject는 그때 그때 쏴주고 사라지는 반면 

Behavior Subject는 마지막 값을 저장하고 있기 때문에 다시 사용할 수 있는 장점이 있다.

사용 예제 

```
return this.behaviorObservable.pipe(
	take(1)
).subscribe(
	data => {
		// Do something
	}
)
```

