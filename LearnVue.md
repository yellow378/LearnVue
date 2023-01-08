# LearnVue
## DOM文本插值{{}}
```js
    <div id="root">
        <p>
            {{a}}
        </p>
    </div>
    <script type="text/javascript">
        var vue = new Vue({
            el:"#app2",
            data:{
                a:'aaa' 
            }
        })
    </script>
```
### v-once 一次性插值
### v-html v-text
### 插值内容可以是JavaScript表达式
## 绑定attribute v-bind
```js
    <div id="app2">
        <span v-bind:title="a">
            悬停几秒
        </span>
    </div>
    <script type="text/javascript">
        var vue = new Vue({
            el:"#app2",
            data:{
                a:'页面加载于'+ new Date().toLocaleDateString() 
            }
        })
    </script>
```
### v-bind:缩写 :
## 条件 v-if
```js
    <div id="app3">
        <p v-if="seen">现在你看到我了</p>
    </div>
    <script type="text/javascript">
        var vue = new Vue({
            el:"#app3",
            data:{
                seen:true 
            }
        })
    </script>
```

## 循环 v-for
```js
    <div id = "app4">
        <ol>
            <li v-for="todo in todos">
                {{todo.text}}
            </li>
        </ol>
    </div>
    <script type="text/javascript">
        var vue = new Vue({
            el:"#app4",
            data:{
                todos:[
                    {
                        text:'学习JavaScript'
                    },
                    {
                        text:'学习Vue'
                    },
                    {
                        text:'整个牛项目'
                    }
                ] 
            }
        })
    </script>
```
```js
vue.todos.push({text:'学习python'})
```

## 处理用户输
### 事件v-on
```js
    <div id="app5">
        <p>{{message}}</p>
        <button v-on:click="reverseMessage">点击反转</button>
    </div>
    <script type="text/javascript">
        var vue = new Vue({
            el:"#app5",
            data:{
                message:"Hello vue js!"
            },
            methods:{
                reverseMessage:function (){
                    this.message = this.message.split(' ').reverse().join(' ')
                }
            }

        })
    </script>
```
### 事件v-on:缩写 @
### 双向绑定 v-model
```js
    <div id="app6">
        <p>{{message}}</p>
        <input v-model="message">
    </div>
    <script type="text/javascript">
        var vue = new Vue({
            el:"#app6",
            data:{
                message:"Hello vue js!"
            }
        })
    </script>
```

## 组件化应用构建
```js
    <div id="app7">
        <ol>
            <todo-item
                v-for="item in list"
                v-bind:todo="item"
                v-bind:key="item.id"
            ></todo-item>
        </ol>
    </div>
    <script type="text/javascript">
        Vue.component(
            'todo-item',
            {
                props:['todo'],
                template:'<li>{{todo.text}}</li>'
            }
        )
        var vue = new Vue({
            el:"#app7",
            data:{
                list:[
                    {id:0,text:'蔬菜'},
                    {id:1,text:'水果'},
                    {id:2,text:'麻花'}
                ]
            }
        })
    </script>
```

## 生命周期钩子 详见API
```js
create
destroyed
mounted 
update
<script type="text/javascript">
    var vm = new Vue({
        //选项
        //MVVM模型 viewmodel vm
        //挂在点
        el:'#app1',
        //数据,data是一个类
        data:{
            a:'flafjlasjflasjflasjdlfasjfoeuipruwqo',
            url:"https://www.baidu.com"
        },
        create:function(){
            console.log('a is:'+this.a)
        },
        updated:function(){
            console.log('a = '+this.a)
        },
        methods:{
            urlclick:function(){
                window.alert("即将跳转到"+this.url)
            }
        }
    });
</script>
```

## 计算属性
```js
    <div id="app2">
        <p>Original message:{{message}}</p>
        <p>Computed reversed message:{{reversedMessage}}</p>
    </div>
    <!--创建一个Vue实例-->
    <script type="text/javascript">
        var vm = new Vue({
            //选项
            //MVVM模型 viewmodel vm
            //挂在点
            el:'#app2',
            //数据,data是一个类
            data:{
                message:"hello vue js!"
            },
            computed: {
                reversedMessage:function(){
                    return this.message.split(' ').reverse().join(' ')
                }
            }
        });
    </script>
```
## 计算属性 VS 方法
### 计算属性和方法可以相互代替
```js
    <div id="app3">
        <p>Date:{{date1}}</p>
        <p>Date:{{date2()}}</p>
    </div>
    <!--创建一个Vue实例-->
    <script type="text/javascript">
        var vm = new Vue({
            //选项
            //MVVM模型 viewmodel vm
            //挂在点
            el:'#app3',
            //数据,data是一个类
            data:{
                message:"hello vue js!"
            },
            methods:{
                date2:function(){
                    return Date.now()
                }
            },
            computed: {
                reversedMessage:function(){
                    return this.message.split(' ').reverse().join(' ')
                },
                date1:function(){
                    return Date.now()
                }
            }
        });
    </script>
```

## 监听属性
```js
watch:{
    firstName:function(val){
        this.fullNmae = val + ' ' + lastName
    }
}
<!--用计算属性代替-->
computed:{
    fullName:function(){
        return this.firstName + " "+ lastName
    }
}
```
## 计算属性的setter
```js
computed:{
    get:function(){
        return this.firstName + " " + lastName
    }
    set:function(newValue){
        var names = newValue.split(' ')
        this.firstName = names[0]
        this.lastName = names[1]
    }
}
```
### 计算属性computed VS 监听属性watch VS 方法methods
