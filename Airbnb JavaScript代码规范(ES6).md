箭头函数

```javascript
//ajax
var xhttp = new XMLHttpRequest();
  xhttp.onreadystatechange = function() {
    if (this.readyState === 4 && this.status === 200) {
      console.log(this.responseText);
    }
  };
  xhttp.open("POST", "/api.json", true);
  xhttp.send();

//jQuery ajax
$.ajax('/').then(function(response){
    console.log(response)
})

//采用fetch调用json数据
fetch('/api.json')
  .then(function(response) {
  return response.json()
}).then(function(json) {
  console.log('parsed json', json)
}).catch(function(ex) {
  console.log('parsing failed', ex)
})

//使用箭头函数
fetch('/api.json')
  .then(response => response.json)
  .then(json => { console.log('parsed json', json)
  }).catch(ex => {
  console.log('parsing failed',ex)
})
```

