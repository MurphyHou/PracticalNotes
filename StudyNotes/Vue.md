## 父子组件通信 
- 子组件
```
<template>
  <div>
    子组件:<span>{{childValue}}</span>
    <!-- 定义一个子组件传值的方法 -->
    <input type="button" value="点击触发" @click="childClick">
  </div>
</template>
<script>
  export default {
    data () {
      return {
        childValue: '我是子组件的数据'
      }
    },
    methods: {
      childClick () {
        // childByValue是在父组件on监听的方法
        // 第二个参数this.childValue是需要传的值
        this.$emit('childByValue', this.childValue)
      }
    }
  }
</script>
```
- 父组件
```
<template>
  <div>
    父组件: <span>{{name}}</span>
    <!-- 引入子组件 定义一个on的方法监听子组件的状态-->
    <child :childByValue="childByValue"></child>
  </div>
</template>
<script>
  import child from './child'
  export default {
    components: {
      child
    },
    data () {
      return {
        name: ''
      }
    },
    methods: {
      childByValue('childByValue',childValue=> {
        // childValue就是子组件传过来的值
        this.name = childValue
      })
    }
  }
</script>
```
- $Children 实例 property 已从 Vue 3.0 中移除，不再支持。
- $Parent 
  ```
  子组件接收:
  this.$parents.msg     //这个msg是父组件的msg
  ```
- $Refs 获取子组件的data和methods
  ```
  子组件 :
   data(){
       return {
            name:"我是子组件"
        }
    },
    methods:{
        show(){
            console.log(子组件方法')
        }
    }

   父组件 :
   methods:{
       test(){
            this.$refs.childComponent.name  //这个name是子组件的name
            this.$refs.childComponent.show()  
       }
     }
     ```
- 依赖注入（Vue3.0）
    > Vue3.0组合式 API 中使用 provide/inject,两者都只能在当前活动实例的 setup() 期间调用  
    > >通过父组件提供给后代组件曝露的属性和方法  
    ```
    父组件:
    data(){
        return{
              name:"父亲的名字"
            }
    },
    provide:function(){
        return {
              getName: this.name
            }
        }
    
    子组件接收:
        inject:["getName"]
    ```

