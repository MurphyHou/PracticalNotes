## 1.带有范围的随机数生成器  
```
function randomNumber(max = 1, min = 0) {  
  if(min >= max) {  
    return max;  
  }  
  return Math.floor(Math.random() * (max - min) + min);
}
```

## 2.深度克隆对象  
```
const deepClone = obj => {  
  let clone = obj;  
  if (obj && typeof obj === "object") {  
    clone = new obj.constructor();  
    Object.getOwnPropertyNames(obj).forEach(  
      prop => (clone[prop] = deepClone(obj[prop]))  
    );  
  }  
  return clone;  
};
```
## 3.获取当前页面的滚动位置
```
const getScrollPosition = (el = window) => ({ 
    x: el.pageXOffset !== undefined ? el.pageXOffset : el.scrollLeft, 
    y: el.pageYOffset !== undefined ? el.pageYOffset : el.scrollTop 
});
```
## 4.滚动到页面顶部
```
const scrollToTop = () => {     
    const c = document.documentElement.scrollTop || document.body.scrollTop;     
    if (c > 0) {         
        window.requestAnimationFrame(scrollToTop);         
        window.scrollTo(0, c - c / 8);     
    } 
}; 
```
## 5.封装原生Ajax(Get和Post)
```
const httpGet = (url, callback, err = console.error) => {     
    const request = new XMLHttpRequest();     
    request.open("GET", url, true);
    request.onload = () => callback(request.responseText);     
    request.onerror = () => err(request);     
    request.send(); 
}; 

httpGet(
    "https://jsonplaceholder.typicode.com/posts/1", 
    console.log
); 
// Logs: {"userId": 1, "id": 1, "title": "sample title", "body": "my text"}
```
```
const httpPost = (url, data, callback, err = console.error) => {     
    const request = new XMLHttpRequest();     
    request.open( POST , url, true);     
    request.setRequestHeader( Content-type ,  application/json; charset=utf-8 );     
    request.onload = () => callback(request.responseText);     
    request.onerror = () => err(request);     
    request.send(data); 
}; 
const newPost = {
    userId: 1, 
    id: 1337, 
    title:  Foo ,     
    body:  bar bar bar  
}; 

const data = JSON.stringify(newPost); 
httpPost(
    "https://jsonplaceholder.typicode.com/posts", 
    data,
    console.log
); 
// Logs: {"userId": 1, "id": 1337, "title": "Foo", "body": "bar bar bar"}
```
## 6.