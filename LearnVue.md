# LearnVue
## DOM{{}}
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