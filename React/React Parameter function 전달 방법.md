​									React Parameter 전달 방법

------

state = {

​    email: '',

​    password: '',

  }



// 나는 onChange 함수에서 2개의 Parameter를 받아서 사용하고 싶다. 이것을 받으려면 어떻게 해야 할까?

onChange = (event, thing) **=>** {

​    this.setState({ [event.target.name]: event.target.value });

​    console.log(thing);

  };



// onChange는 event를 기본으로 생성시키므로 추가로 무언가 보내려면 event를 첫번째 param으로 사용하고 다른 것을 사용해야 하는 것 같다.

<input type="text" onChange={(event) **=>** this.onChange(event, "hi")}  value={this.state.email} name="email" id="login-email" placeholder="example@example.com"/>