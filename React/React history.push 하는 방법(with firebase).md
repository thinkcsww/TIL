​									**React history.push 하는 방법**

------

Firebase 사용시 

/Component/Firebase/context.js에 withFirebase를 export 해준다

```
import React from 'react';

const FirebaseContext = React.createContext(null);

export const withFirebase = Component => props => (
  <FirebaseContext.Consumer>
    {firebase => <Component {...props} firebase={firebase} />}
  </FirebaseContext.Consumer>
);

export default FirebaseContext;
```



/Component/Firebase/index.js에서 withFirebase를 export 해준다

```
import FirebaseContext, { withFirebase } from './context';
import Firebase from './firebase';

export default Firebase;

export { FirebaseContext, withFirebase };
```



사용하고자 하는 페이지에서 withRouter와 withFirebase를 import한다

```
import React, { Component } from 'react';
import { connect } from 'react-redux';
import { NavLink, withRouter } from 'react-router-dom';

import { withFirebase } from '../../components/Firebase';
import photo from '../../assets/images/mountain1.jpg';
import classes from './Login.css';
import * as actions from '../../store/actions';

```



그리고 export할때 감싸준다 

```dart
export default connect(mapStateToProps, mapDispatchToProps)(withRouter(withFirebase(Login)));
```

세팅이 완료 되었고 

사용하고자 하는 부분에서 다음과 같이 사용한다

```
this.props.history.push('/');
```

