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
## 6.if多条件判断  
```
// 冗余
if (x === 'abc' || x === 'def' || x === 'ghi' || x ==='jkl') {}

// 简洁
if (['abc', 'def', 'ghi', 'jkl'].includes(x)) {} 

```

## 7. 判断类型集合 
```
export const checkStr = (str, type) => {
    switch (type) {
        case 'phone':   //手机号码
            return /^1[3|4|5|6|7|8|9][0-9]{9}$/.test(str);
        case 'tel':     //座机
            return /^(0\d{2,3}-\d{7,8})(-\d{1,4})?$/.test(str);
        case 'card':    //身份证
            return /(^\d{15}$)|(^\d{18}$)|(^\d{17}(\d|X|x)$)/.test(str);
        case 'pwd':     //密码以字母开头，长度在6~18之间，只能包含字母、数字和下划线
            return /^[a-zA-Z]\w{5,17}$/.test(str)
        case 'postal':  //邮政编码
            return /[1-9]\d{5}(?!\d)/.test(str);
        case 'QQ':      //QQ号
            return /^[1-9][0-9]{4,9}$/.test(str);
        case 'email':   //邮箱
            return /^[\w-]+(\.[\w-]+)*@[\w-]+(\.[\w-]+)+$/.test(str);
        case 'money':   //金额(小数点2位)
            return /^\d*(?:\.\d{0,2})?$/.test(str);
        case 'URL':     //网址
            return /(http|ftp|https):\/\/[\w\-_]+(\.[\w\-_]+)+([\w\-\.,@?^=%&:/~\+#]*[\w\-\@?^=%&/~\+#])?/.test(str)
        case 'IP':      //IP
            return /((?:(?:25[0-5]|2[0-4]\\d|[01]?\\d?\\d)\\.){3}(?:25[0-5]|2[0-4]\\d|[01]?\\d?\\d))/.test(str);
        case 'date':    //日期时间
            return /^(\d{4})\-(\d{2})\-(\d{2}) (\d{2})(?:\:\d{2}|:(\d{2}):(\d{2}))$/.test(str) || /^(\d{4})\-(\d{2})\-(\d{2})$/.test(str)
        case 'number':  //数字
            return /^[0-9]$/.test(str);
        case 'english': //英文
            return /^[a-zA-Z]+$/.test(str);
        case 'chinese': //中文
            return /^[\\u4E00-\\u9FA5]+$/.test(str);
        case 'lower':   //小写
            return /^[a-z]+$/.test(str);
        case 'upper':   //大写
            return /^[A-Z]+$/.test(str);
        case 'HTML':    //HTML标记
            return /<("[^"]*"|'[^']*'|[^'">])*>/.test(str);
        default:
            return true;
    }
}
```
