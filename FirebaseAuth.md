### What to import
```javascript
import { getAuth, signInWithEmailAndPassword, createUserWithEmailAndPassword } 
```

### Sign Up
```javascript
const handleAction = (id) => {
  const authentication = getAuth();  
  createUserWithEmailAndPassword(authentication, emailInput, passwordInput)
    .then((response) => {
      navigate('/home')
      sessionStorage.setItem('Auth Token', response._tokenResponse.refreshToken)
    })  
    .catch((err) => {
        console.log(err)
    })
}
```

### Log in
```javascript
const handleAction = (id) => {
  const authentication = getAuth();  
  signInWithEmailAndPassword(authentication, email, password)
      .then((response) => {
        navigate('/home')
        sessionStorage.setItem('Auth Token', response._tokenResponse.refreshToken)
      })
      .catch((err) => {
        console.log(err)
      })
}
```

### Private Route Functionality
> You just basically navigate to the private page only if token exists
```javascript
useEffect(() => {
  let authToken = sessionStorage.getItem('Auth Token')
  if (authToken) {
      navigate('/home')
  } else {
    navigate('/login')
  }
}, [])
```
