​																**Angular 2개의 Api 끝내고 로딩 없애기**

------

api를 2개 이상 쓰면 하나가 늦게 끝날지 모르기 때문에 Loading을 제거하기 애매하다. 

하지만 async await를 쓰면 다 마무리 된 후 처리할 수 있다.

```

const initial = async () => {
      await this.catalogService.getTreeCatalogs();
      await this._initialMetadataList();
    };

     initial().then(() => {
        this.loadingHide();
      }).catch(error => this.commonExceptionHandler(error));


```

