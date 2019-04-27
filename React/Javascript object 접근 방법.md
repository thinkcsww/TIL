​									**Javascript object 접근 방법**

------

 아래와 같이 object가 있다. 

접근하는 방법은 두가지가 있다. 

6번째 줄에 type을 접근하는 것을 예시로 보이겠다.

1. state.orderForm.name.elementConfig.type
2. state.orderForm.name.elementConfig['type']

첫번째 방법은 정해진 key가 있을 때 

두번째 방법은 주로 변수로 접근할 때 쓰이는 것 같다.

```
1 var state = {
2  orderForm: {
3    name: {
4      elementType: 'input',
5      elementConfig: {
6        type: 'text',
        placeholder: 'Your Name'
      },
      value: '',
      validation: {
        required: true
      },
      valid: false,
      touched: false
    },
  }
}
```

