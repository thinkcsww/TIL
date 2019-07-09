​											Angular Service 사용법

------

1. Service를 만든다.

```
export class AccountsService {
  accounts = [
    {
      name: 'Master Account',
      status: 'active'
    },
    {
      name: 'Testaccount',
      status: 'inactive'
    },
    {
      name: 'Hidden Account',
      status: 'unknown'
    }
  ];

  addAccount(name: string, status: string) {
    this.accounts.push({name: name, status: status});
  }

  updateStatus(id: number, status: string) {
    this.accounts[id].status = status;
  };
}

```

2. Component에서 constructor로 생성한다.

```
constructor(private loggingService: LoggingService, private accountsService: AccountsService) {}
```

3.  app.module.ts에 provider:[] 배열에 추가한다.
4. Service를 Service에 Injection하기 위해서는 인젝션 당하는 서비스에 @Injectible()을 추가한다.

4. 사용한다

```
this.accountsService.addAccount(accountName, accountStatus);
```

