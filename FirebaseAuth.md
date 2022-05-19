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
