### Configure Firebase
```javascript
import { initializeApp } from 'firebase/app';

const firebaseConfig = {
    apiKey: "AIzaSyAQwgM_CXLk9GSgPje7Mxv2ewKpboialpg",
    authDomain: "iltpwebsite.firebaseapp.com",
    projectId: "iltpwebsite",
    storageBucket: "iltpwebsite.appspot.com",
    messagingSenderId: "1039258363296",
    appId: "1:1039258363296:web:f237621cc287de4712b0c5",
    measurementId: "G-PQSL1Y881Q",
};

export const app = initializeApp(firebaseConfig);
```

### Sign Up
```javascript
import { app } from './firebase-config'
import { getAuth, createUserWithEmailAndPassword } from 'firebase/auth'

const handleAction = () => {
  const authentication = getAuth(app);  
  createUserWithEmailAndPassword(authentication, emailInput, passwordInput)
    .then((response) => {
      navigate('/home')
      sessionStorage.setItem('Auth Token', response._tokenResponse.refreshToken)
    })  
    .catch((err) => {
      const errorCode = err.code
      const errorMessage = err.message
    })
}
```

### Log in
```javascript
import { app } from './firebase-config'
import { getAuth, signInWithEmailAndPassword } from 'firebase/auth'

const handleAction = () => {
  const authentication = getAuth(app);  
  signInWithEmailAndPassword(authentication, email, password)
      .then((response) => {
        navigate('/home')
        sessionStorage.setItem('Auth Token', response._tokenResponse.refreshToken)
      })
      .catch((err) => {
        const errorCode = err.code
        const errorMessage = err.message
      })
}
```

### Log out
```javascript
const handleLogout = () => {
    // destroy token
    sessionStorage.removeItem('Auth Token')
    navigate('/')
}
```

### Private Route Functionality
> You just basically navigate to the private page only if token exists
```javascript
// make sure to add this to both protected page and login/signup.
// just to prevent users from going back to login, when sessionStorage still exists
useEffect(() => {
  let authToken = sessionStorage.getItem('Auth Token')
  if (authToken) {
      navigate('/home')
  } else {
    navigate('/login')
  }
}, [])
```


### Get Email
```javascript
getAuth()
    .getUser(uid)
    .then((userRecord) => {
    // See the UserRecord reference doc for the contents of userRecord.
    console.log(`Successfully fetched user data: ${userRecord.toJSON()}`);
    })
    .catch((error) => {
    console.log('Error fetching user data:', error);
    });
```
