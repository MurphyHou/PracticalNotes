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
    title:  Foo,     
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
## 8. 单纯数据的非空校验 
```
function isEmpty(value) {
    if (['', null, undefined].includes(value)) {  
        return true
    }
    if (Array.prototype.isPrototypeOf(value) && value.length === 0) {  
        return true;
    } 
    if (Object.prototype.isPrototypeOf(value) && Object.keys(value).length === 0) {  
        return true;
    }  
    return false;
}
```
## 9. 用??代替||，用于判断运算符左侧的值为null或undefined时，才返回右侧的值
|| 运算符是左边是空字符串或false或0等falsy值，都会返回后侧的值。而??必须运算符左侧的值为null或undefined时，才会返回右侧的值。因此0||1的结果为1，0??1的结果为0
```
const response = {
  settings: {
    nullValue: null,
    height: 400,
    animationDuration: 0,
    headerText: '',
    showSplashScreen: false
  }
};

const undefinedValue = response.settings.undefinedValue ?? 'some other default'; // result: 'some other default'
const nullValue = response.settings.nullValue ?? 'some other default'; // result: 'some other default'
const headerText = response.settings.headerText ?? 'Hello, world!'; // result: ''
const animationDuration = response.settings.animationDuration ?? 300; // result: 0
const showSplashScreen = response.settings.showSplashScreen ?? true; // result: false
```
## 10. 使用?.简化&&和三元运算符
?.直接在链式调用的时候判断，判断左侧的对象是否为null或undefined，如果是的，就不再往下运算，返回undefined，如果不是，则返回右侧的值
```
var street = user.address && user.address.street;

var fooInput = myForm.querySelector('input[name=foo]')
var fooValue = fooInput ? fooInput.value : undefined

// 简化
var street = user.address?.street
var fooValue = myForm.querySelector('input[name=foo]')?.value
```
注：常见写法  
1. obj?.prop  对象属性  
2. obj?.[expr]  对象属性  
3. func?.(...args)  函数或对象方法的调用  
   
## 11. 使用动态导入import()实现按需加载（优化静态import）
```
import defaultExport from "module-name";
import * as name from "module-name";
```
但是静态引入的import 语句需要依赖于 type="module" 的script标签，而且有的时候我们希望可以根据条件来按需加载模块，比如以下场景：

当静态导入的模块很明显的降低了代码的加载速度且被使用的可能性很低，或者并不需要马上使用它
当静态导入的模块很明显的占用了大量系统内存且被使用的可能性很低
当被导入的模块，在加载时并不存在，需要异步获取
当被导入的模块有副作用，这些副作用只有在触发了某些条件才被需要时
这个时候我们就可以使用动态引入import()，它跟函数一样可以用于各种地方，返回的是一个 promise

基本使用如下两种形式 

```
//形式 1
import('/modules/my-module.js')
  .then((module) => {
    // Do something with the module.
  });
  
 //形式2
let module = await import('/modules/my-module.js');
```
## 12.使用顶层 await（top-level await）简化 async 函数
顶层 await 允许开发者在 async 函数外部使用 await 字段
```
let module = await import('/modules/my-module.js');
/以前
(async function () {
  await Promise.resolve(console.log('🎉'));
  // → 🎉
})();

//简化后
await Promise.resolve(console.log('🎉'));
```