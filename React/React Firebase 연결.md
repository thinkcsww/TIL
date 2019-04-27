​										**React Firebase 연결**

------



1. npm install firebase
2. /component/Firebase 폴더 생성
3. /component/Firebase/context.js 생성

```
import React from 'react';

const FirebaseContext = React.createContext(null);

export default FirebaseContext;
```

4. /component/Firebase/firebase.js 생성

```
import app from 'firebase/app';

const config = {
  apiKey: "AIzaSyBauCJ2tLMXBZaa_vSE_KCVRwaGVkzqm_8",
  authDomain: "capstone-d26ae.firebaseapp.com",
  databaseURL: "https://capstone-d26ae.firebaseio.com",
  projectId: "capstone-d26ae",
  storageBucket: "capstone-d26ae.appspot.com",
  messagingSenderId: "337200690244"
};

class Firebase {
  constructor() {
    app.initializeApp(config);
  }
}

export default Firebase;
```

5. /component/Firebase/index.js 생성

```
import FirebaseContext from './context';
import Firebase from './firebase';

export default Firebase;

export { FirebaseContext };
```

6. Index.js에서 

```
import Firebase, { FirebaseContext } from './components/Firebase';

const app = (
  <Provider store={store}>
    <BrowserRouter>
      <FirebaseContext.Provider value={new Firebase()}>
      <App />
      </FirebaseContext.Provider>
    </BrowserRouter>
  </Provider>
);
```

