### Axios POST request

``` javascript
axios.post('http://localhost:8000/users/', data)  
    .then(response => {  
       console.log(response) 
    }).catch(error => {  
    	console.log(error)  
})

```


### Axios GET request
``` js
axios.get('https://localhost:8080/users')  
    .then(res => {  
        console.log(res)  
    })  
    .catch(err => {  
        console.log(err)  
})

```

### useEffect GET request

``` js
useEffect(()=>{  
  
    // check session storage if id exists  
 if (sessionStorage.getItem("session_id") === null) {  
        history.push('/table_number')  
    }  
    else {  
        axios.get('https://localhost:8080/users')  
            .then(res => {  
                console.log(res)  
                setTableNumber(res.data.tableNumber)  
            })  
            .catch(err => {  
                console.log(err)  
            })  
    }  
}, [])

```

### useState REACT

```js
const [TableNumber, setTableNumber] = React.useState('Empty')

```