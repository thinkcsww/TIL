​									      **Paging** 

------

**Concept**

Paging은 많은 데이터가 있을 때 한번에 다 랜더링하지 않고 일정 개수 씩만 랜더링 해서 div에 append 하는 방식으로

리소스를 아낄 수 있다.



**Method**



<h3>스크롤 체크</h3>

보통 Scroll을 화면의 끝까지 내리면 다음 정보를 받아 온다.

스크롤을 끝까지 했는지는 다음 Javascript 함수로 알 수 있다.

```
if ((document.body.scrollHeight == document.documentElement.scrollTop + window.innerHeight)) {
    ajax request here! // ajax를 알맞게 해주면 된다.
}

휠을 내린 높이 (scrollTop) + 고정된 화면의 높이 (innerHeight) == 스크롤 할 수 있는 전체 높이 (scrollHeight) 가 같으면 휠을 끝까지 내린 것이다.
```

ScrollTop은 휠을 얼만큼 내렸는지를 나타낸다.

ScrollHeight는 스크롤 할 수 있는 보이지 않는 밑에 부분까지 포함한 높이를 나타낸다. 

innerHeight는 현재 보이는 부분의 높이를 나타낸다. 즉 주소창을 제외한 부분의 높이 -> 고정되어 있음



<h3>ajax에 따른 데이터 처리</h3>

필요한 변수 : 

page(현재 페이지 -> 1에서 시작),

start(몇번째 정보부터 받아와야 하는지),

num_iterations(start보다 크거나 같으면 데이터처리 시작하기 위한 변수), 

count(limit보다 크면 멈추기 위한 변수)

limit(한 번에 가져올 개수)

More_data(가져올 데이터가 더 있는지 알기 위한 Boolean)

while(mysqli_fetch_array($data_query)) 루프로 데이터가 더 없을 때 까지 진행한다.

```
while(mysqli_fetch_array($data_query))
```

1. 시작하기 전에 스크롤을 끝까지 하면 몇 개의 데이터를 가져올 것인지 limit 변수를 정한다.
2. 처음 값은 Page = 0 을 넘겨준다.
3. start = page -1 * limit으로 정하고 num_iteration < start 이면 Continue문을 쓴다.
4. Num_iteration > start 이고 count < limit 이면 계속 진행 한다.
5. count > limit 이면 limit에 도달하여 그만 데이터를 받아오지만 루프이기 때문에 더 가져올 데이터가 있다는 의미이다. 고로 page++을 하고 more_data = true를 전달해준다.
6. count < limit이면 more_data를 False로 전달해 준다.



