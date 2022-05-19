### Private Route Functionality
> You just basically navigate only if token exists
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
