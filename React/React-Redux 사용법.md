​										**React-Redux 사용법**

------

1. 필요한 libraries

   a. react-redux

   b. redux 

   c. redux-thunk

2. 구조

a. 구조는 크게 components, container, store로 나뉜다. container는 store(redux)로 부터 state, function 등을 전달 받는다. 그리고 이 전달 받은 내용들은 components들에게 뿌려준다. 

b. components는 예를 들어 components/NavigationBar/NavigationItems… 이런식으로 만들 수 있다.

c. container는 store의 바로 아래이 있으므로 예를 들어 container/Login/Login.js 이정도로 간단하게 된다.

d. store는 store/actions || store/reducers로 크게 나눌 수 있다. 

store/actions(type, param 전달) 안에는 actionTypes.js(Constant들을 담아놓는 파일), object1.js, object2.js .. index.js(모든 action들을 모아서 export 하는 파일)으로 나눌 수 있다.

store/reducer(실제 기능 구현) 안에는 마찬가지로 object1.js, object2.js로 나눌 수 있지만 exporte되지 않기 때문에 index.js는 필요 없다. 전달 받은 param은 action.param 으로 사용할 수 있음 

3. 연결 방법 

   a. index.js에서 다음과 같이 만든다.

   ```
   import React from 'react';
   import ReactDOM from 'react-dom';
   import { Provider } from 'react-redux';
   import { BrowserRouter } from 'react-router-dom';
   import { createStore, applyMiddleware, compose, combineReducers } from 'redux';
   import thunk from 'redux-thunk';
   
   import './index.css';
   import App from './App';
   import * as serviceWorker from './serviceWorker';
   import burgerBuilderReducer from './store/reducers/burgerBuilder';
   import orderReducer from './store/reducers/order';
   
   const composeEnhancers = window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__ || compose;
   
   const rootReducer = combineReducers({
     burgerBuilder: burgerBuilderReducer,
     order: orderReducer
   });
   
   const store = createStore(rootReducer, composeEnhancers(
     applyMiddleware(thunk)
   ));
   
   const app = (
     <Provider store={store}>
       <BrowserRouter>
         <App />
       </BrowserRouter>
     </Provider>
   );
   
   ReactDOM.render(app, document.getElementById('root'));
   serviceWorker.unregister();
   
   ```

4. 구현 

 /store/action에서 다음과 같이 전달한 param과 type을 정해준다. 

```
export const purchaseBurgerSuccess = (id, orderData) => {
  return {
    type: actionTypes.PURCHASE_BURGER_SUCCESS,
    orderId: id,
    orderData: orderData
  };
};
```

/store/reducer에서 전달 받은 파람을 action.param으로 사용하며 실제 구현한다. 

```
case actionTypes.PURCHASE_BURGER_SUCCESS:
	  const newOrder = { ...action.orderData, id: action.orderId } 
	  return { 
          ...state, 
          purchase: true, 
          loading: false, 
          orders: state.orders.concat(newOrder),
	  }
```



5. 사용 방법 

1. Container에 계층에 속한 js파일에 간다 .
2. 다음을 import한다 

```
import React, { Component } from 'react';
import { connect } from 'react-redux';
```

3. Class 바깥에 다음으로 store와 container를 연결한다. mapStateToProps는 store에 있는 state를 container에 props로 제공해 주며, mapDispatchToProps의 함수들을 사용해서 변경할 수 있고 실시간으로 업데이트 된다.

```
const mapStateToProps = state => {
  return {
    orders: state.order.orders,
    loading: state.order.loading,
  }
};

const mapDispatchToProps = dispatch => {
  return {
    onFetchOrders: () => dispatch(actions.fetchOrders())
  };
};

export default connect(mapStateToProps, mapDispatchToProps)(BurgerBuilder);
```

4. 사용 예시  - componentDidMount() 안에서 this.props.function으로 사용될 수 있다.

1. ```
   componentDidMount () {
       console.log(this.props);
       this.props.onInitIngredients();
   }
   ```

   