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
## 条件渲染 v-if
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
### v-else
### v-else-if
### 用key管理复用的元素

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
### 事件处理 v-on
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
```js
    <div id="app6">
        <button v-on:click="changeC('Green')">Green</button>
        <button v-on:click="changeC('Blue')">Blue</button>
        <button v-on:click="changeC('Red')">Red</button>
        <p v-bind:style="{color:color}">This is text!!!</p>
    </div>
    <script type="text/javascript"> 
        var vm = new Vue({
            el:'#app6',
            data:{
                color:'black'
            },
            methods:{
                changeC:function(newcolor){
                    this.color = newcolor
                }
            }
        })  
    </script>
```
### 事件v-on:缩写 @
### 传入$event
### 事件修饰符
```js
.stop
.prevent
.capture
.self
.once
.passive
```
## 按键修饰符
```js
v-on:keyup.enter='submit'
```
## 系统修饰键
### 鼠标修饰键
## 双向绑定 v-model
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
### 表单输入绑定
```
text textaea value input
checkbox radio checked change
select value change
```
```js
//文本
//多行文本
//单选框
//复选框
//单选按钮
//选择框 单选 多选
    <div id="app7">
        <input v-model="message" placeholder="edit me">
        <p>Message is {{message}}</p>
        <span>Multiline message is:</span>
        <p style="white-space: pre-line;" v-bind:style="{color:color}">{{message}}</p>
        <br>
        <textarea v-model="message" placeholder="add multiple lines"></textarea>

        <br>
        <input type="checkbox" id="checkbox" v-model="checked">
        <label for="checkbox">{{checked}}</label>

        <br>
        <input type="checkbox" id="jack" value="jack" v-model="checkNames">
        <label for="jack">jack</label>
        <input type="checkbox" id="john" value="john" v-model="checkNames">
        <label for="john">john</label>
        <input type="checkbox" id="mike" value="mike" v-model="checkNames">
        <label for="mike">mike</label>
        <br>
        <span>Checked names:{{checkNames}}</span>

        <br>
        <input type="radio" id="one" value="one" v-model="picked">
        <label for="one">One</label>
        <br>
        <input type="radio" id="two" value="two" v-model="picked">
        <label for="two">Two</label>
        <br>
        <span>picked:{{picked}}</span>

        <br>
        <select v-model="selected">
            <optioin disabled value="">请选择</optioin>
            <option>A</option>
            <option>B</option>
            <option>C</option>
        </select>
        <span>Select:{{selected}}</span>
        <br>
        <select v-model="multiselected" multiple style="width:50px">
            <option>A</option>
            <option>B</option>
            <option>C</option>
        </select>
        <br>
        <span>Selected:{{multiselected}}</span>
        <br>
        <select v-model="selected2">
            <optioin disabled value="">请选择</optioin>
            <option v-for="option in options">{{option}}</option>
        </select>
        <span>Select:{{selected2}}</span>
    </div>
    <script type="text/javascript"> 
        var vm = new Vue({
            el:'#app7',
            data:{
                color:'aqua',
                message:'',
                checked:false,
                checkNames:["jack"],
                picked:'',
                selected:'',
                multiselected:[],
                selected2:'',
                options:[1,2,3,4,5]
            },
            methods:{
                changeC:function(newcolor,event){
                    this.color = newcolor
                    window.alert(event)
                }
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

## 绑定HTML Class
```js
<div id="app1" class="static" v-bind:class="{active:isactive,'text-danger':hasError}">
    <p>app1</p>
</div>
<script type="text/javascript">
    var vm = new Vue({
        el:'#app1',
        data:{
            isactive:true,
            hasError:true
        }
    })
</script>
```
### 不必内联定义在模板内data中或者计算属性
```js
<div v-bind:class="classObject"></div>
data:{
    classObject{
        active:true,
        'text-danger':false
    }
}
//用计算属性
data:{
    isActive:true,
    error:null
},
computed:{
    classObject:function(){
        return {
            active:this.isActive && !this.error,
            'text-danger':this.error && this.error.type==='fatal'
        }
    }
}
```
#### 数组语法 v-bind:class=[' ',' ',' ']
#### 三元式
### 用在组件上
## 绑定内联样式
```js
   <div id="app1" v-bind:style="{color:activecolor,fontSize:fontsize+'px'}">
       app1
    </div>
    <script type="text/javascript">
        var vm = new Vue({
            el:'#app1',
            data:{
                activecolor:'blue',
                fontsize:30
            }
        })  
    </script>
```
## 列表渲染v-for
```js
//v-for 遍历列表
v-for="(item,index) in items"
//v-for 遍历对象
v-for="(value,name) in object"
```

# 组件
