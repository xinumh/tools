
### isAvailableEmail
``` js
function isAvailableEmail(sEmail) {
    return /^[A-Za-zd]+([-_.][A-Za-zd]+)*@([A-Za-zd]+[-.])+[A-Za-zd]{2,5}$/.test(sEmail)
}
```