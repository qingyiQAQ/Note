# Vue3

## 官网

https://cn.vuejs.org

## 快捷键

ctrl+?快捷注释

alt+shift+f快捷格式化代码

## html模板代码

可以通过打html实现快速构建

![image-20231212220323241](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231212220323241.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    
</body>
</html>
```

## js导入导出

### 导出

在每个方法前加export关键字导出

```js
//简单的展示信息
export function simpleMessage(msg){
    console.log(msg);
}

//复杂的展示信息
export function complexMessage(msg){
    console.log(new Date()+":  "+msg);
}
```

批量导出

```js
//批量导出
export {simpleMessage,complexMessage}
```

默认导出

```js
export default {simpleMessage,complexMessage}
```

### 导入

import关键字导入后面的type必须是module

document.getElementById获取按钮元素

然后onclick设置其点击方法

```html
	<body>
        <div id="app">
            <button id="btn">点我展示信息</button>
        </div>

        <script type="module">
            import {complexMessage} from './showMessage.js';
            document.getElementById("btn").onclick=function(){
                complexMessage("我被点击了")
            }
        </script>
    </body>
```

可以通过as关机键给导入的方法起别名

```html
import {complexMessage as cm} from './showMessage.js';
```

后续使用该方法全都要用别名，导出同理

默认导出对应的导入

```html
<script type="module">
            import messageMethods from './showMessage.js';
            document.getElementById("btn").onclick=function(){
                messageMethods.simpleMessage("我被点击了")
            }
        </script>
```

## 快速创建vue实例(入门)

1.导入vue官方提供的方法createApp

2.使用createApp({})在花括号中直接传参数

3.参数使用data(){}在花括号里面直接返回

4.createApp方法后加一个.mount("#app")其中app与上面的div模块对应，代表这个模块由vue接管

5.定义一个id为app的div模块，里面使用双花括号里面放参数名即可拿到参数

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div id="app">
        <h1>
            {{msg}}
        </h1>
    </div>

    <!--引入vue模块-->
    <script type="module">
        import {createApp} from 'https://unpkg.com/vue@3/dist/vue.esm-browser.js';
        //创建vue的应用实例
        createApp({
            data(){
                return{
                    //定义数据
                    msg: 'hello vue3'
                }
            }

        }).mount("#app");
    </script>
</body>
</html>
```

## 常用指令

![image-20231212222019755](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231212222019755.png)

### v-for

![image-20231212222152371](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231212222152371.png)

实例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>

    <div id="app">
        <table border="1 solid" colspa="0" cellspacing="0">
            <tr>
                <th>文章标题</th>
                <th>分类</th>
                <th>发表时间</th>
                <th>状态</th>
                <th>操作</th>
            </tr>
            <!--哪个元素要出现多次，v-for指令就添加到那个元素上-->
            <tr v-for="(article,index) in articleList">
                <td>{{article.title}}</td>
                <td>{{article.category}}</td>
                <td>{{article.time}}</td>
                <td>{{article.state}}</td>
                <td>
                    <button>编辑</button>
                    <button>删除</button>
                </td>
            </tr>
        </table>
    </div>

    <script type="module">
        //导入vue模块
        import { createApp} from 
                'https://unpkg.com/vue@3/dist/vue.esm-browser.js'
        //创建应用实例
        createApp({
            data() {
                return {
                    //定义数据
                    articleList:[
                        {
                            title:"医疗反腐绝非砍医护收入",
                            category:"时事",
                            time:"2023-09-5",
                            state:"已发布"
                        },
                        {
                            title:"中国男篮缘何一败涂地？",
                            category:"篮球",
                            time:"2023-09-5",
                            state:"草稿"
                        },
                        {
                            title:"华山景区已受大风影响阵风达7-8级，未来24小时将持续",
                            category:"旅游",
                            time:"2023-09-5",
                            state:"已发布"
                        }
                    ]
                }
            }
        }).mount("#app")//控制页面元素
    </script>
</body>
</html>
```

### v-bind

![image-20231213150520376](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231213150520376.png)

![image-20231213150602652](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231213150602652.png)

实例

```html
    <div id="app">
        <a v-bind:href="url">黑马官网</a>
    </div>

    <script type="module">
        //引入vue模块
        import { createApp} from 
                'https://unpkg.com/vue@3/dist/vue.esm-browser.js'
        //创建vue应用实例
        createApp({
            data() {
                return {
                    url: 'https://www.itheima.com'
                }
            }
        }).mount("#app")//控制html元素
     </script>
```

### v-if&v-show

![image-20231213152714044](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231213152714044.png)

实例

```html
    <div id="app">

        手链价格为:  
        <span v-if="customer.level>=0 && customer.level<=1">9.9</span>  
        <span v-else-if="customer.level>=2 && customer.level<=4">19.9</span> 
        <span v-else>29.9</span>

        <br/>

        手链价格为:  
        <span v-show="customer.level>=0 && customer.level<=1">9.9</span>  
        <span v-show="customer.level>=2 && customer.level<=4">19.9</span> 
        <span v-show="customer.level>=5">29.9</span>

    </div>

    <script type="module">
        //导入vue模块
        import { createApp} from 'https://unpkg.com/vue@3/dist/vue.esm-browser.js'

        //创建vue应用实例
        createApp({
            data() {
                return {
                    customer:{
                        name: "zhangsan",
                        level: 3
                    }
                }
            }
        }).mount("#app")//控制html元素
    </script>
```

### v-on

![image-20231213152957346](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231213152957346.png)

实例

主义用到的方法需要定义在methods中

```html
    <div id="app">
        <button v-on:click="money">点我有惊喜</button> &nbsp;
        <button @click="love">再点更惊喜</button>
    </div>

    <script type="module">
        //导入vue模块
        import { createApp} from 'https://unpkg.com/vue@3/dist/vue.esm-browser.js'

        //创建vue应用实例
        createApp({
            data() {
                return {
                    //定义数据
                }
            },
            methods:{
                money: function(){
                    alert('送你钱100')
                },
                love: function(){
                    alert('爱你一万年')
                }
            }
        }).mount("#app");//控制html元素
    </script>
```

### v-model

![image-20231213153939662](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231213153939662.png)

实例

```html
    <div id="app">

        文章分类: <input type="text" v-model="searchConditions.category"/> <span>{{searchConditions.category}}</span>

        发布状态: <input type="text" v-model="searchConditions.state"/> <span>{{searchConditions.state}}</span>

        <button>搜索</button>
        <button v-on:click="clear">重置</button>

        <br />
        <br />
        <table border="1 solid" colspa="0" cellspacing="0">
            <tr>
                <th>文章标题</th>
                <th>分类</th>
                <th>发表时间</th>
                <th>状态</th>
                <th>操作</th>
            </tr>
            <tr v-for="(article,index) in articleList">
                <td>{{article.title}}</td>
                <td>{{article.category}}</td>
                <td>{{article.time}}</td>
                <td>{{article.state}}</td>
                <td>
                    <button>编辑</button>
                    <button>删除</button>
                </td>
            </tr>
        </table>
    </div>
    <script type="module">
        //导入vue模块
        import { createApp } from 'https://unpkg.com/vue@3/dist/vue.esm-browser.js'
        //创建vue应用实例
        createApp({
            data() {
                return {
                    //定义数据
                    searchConditions:{
                        category:'',
                        state:''
                    },

                    articleList: [{
                        title: "医疗反腐绝非砍医护收入",
                        category: "时事",
                        time: "2023-09-5",
                        state: "已发布"
                    },
                    {
                        title: "中国男篮缘何一败涂地？",
                        category: "篮球",
                        time: "2023-09-5",
                        state: "草稿"
                    },
                    {
                        title: "华山景区已受大风影响阵风达7-8级，未来24小时将持续",
                        category: "旅游",
                        time: "2023-09-5",
                        state: "已发布"
                    }]
                }
            },
            methods:{
                clear:function(){
                    //清空category以及state的数据
                    //在methods对应的方法里面，使用this就代表的是vue实例
                    //可以使用this获取到vue实例中准备的数据
                    this.searchConditions.category='';
                    this.searchConditions.state='';
                }
            }
        }).mount("#app")//控制html元素
    </script>
```

## vue生命周期

![image-20231213194922100](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231213194922100.png)

## Axios

使用步骤

引入Axios的js文件

```html
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
```

使用Axios发送请求，并获取相应结果

```js
		axios({
            method:'get',
            url:'http://localhost:8080/article/getAll'
            //data:这个是可选参数
        }).then(result=>{
            //成功的回调
            //result代表服务器响应的所有数据，包含了相应头响应体，result.data代表接口响应的核心数据
            console.log(result.data);
        }).catch(err=>{
            //失败的回调
            console.log(err);
        })
```

或者以别名的方式发送请求

使用axios中的get,post等方法

```js
axios.get('http://localhost:8080/article/getAll').then(result=>{
            console.log(result.data);
        }).catch(err=>{
            console.log(err);
        });
```

## 综合项目实例

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <div id="app">

        文章分类: <input type="text" v-model="searchConditions.category">

        发布状态: <input type="text" v-model="searchConditions.state">

        <button v-on:click="search">搜索</button>

        <br />
        <br />
        <table border="1 solid" colspa="0" cellspacing="0">
            <tr>
                <th>文章标题</th>
                <th>分类</th>
                <th>发表时间</th>
                <th>状态</th>
                <th>操作</th>
            </tr>
            <tr v-for="(article,index) in articleList">
                <td>{{article.title}}</td>
                <td>{{article.category}}</td>
                <td>{{article.time}}</td>
                <td>{{article.state}}</td>
                <td>
                    <button>编辑</button>
                    <button>删除</button>
                </td>
            </tr>
        </table>
    </div>
    <!--导入axios的js文件-->
    <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
    <script type="module">
        //导入vue模块
        import { createApp } from 'https://unpkg.com/vue@3/dist/vue.esm-browser.js'
        //创建vue应用实例
        createApp({
            data(){
                return {
                    articleList:[],
                    searchConditions:{
                        category:'',
                        state:''
                    }
                }
            },
            methods:{
                //声明方法
                search:function(){
                    //发送请求，完成搜索，携带搜索条件
                    axios.get('http://localhost:8080/article/search?category='+this.searchConditions.category+'&state='+this.searchConditions.state)
                    .then(result=>{
                        //把得到的数据赋值给articleList
                        this.articleList=result.data;
                    }).catch(err=>{
                        console.log(err);
                    });
                }
            },
            //钩子函数mounted中获取所有数据
            mounted:function(){
                //发送异步请求  axios
                axios.get('http://localhost:8080/article/getAll').then(result=>{
                    //成功回调
                    //console.log(result.data);
                    this.articleList=result.data;
                }).catch(err=>{
                    //失败回调
                    console.log(err);
                })
            }
        }).mount("#app")//控制html元素
    </script>
</body>

</html>
```

## 创建Vue工程项目

进入需要创建该项目的目录，打开cmd

运行命令

```
npm init vue@latest
```

进入项目所在位置

```
cd vue-project
```

安装需要的依赖

```
npm install
```

## Vue项目结构

![image-20231213221906238](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231213221906238.png)

重点在App.vue的编写

## App.vue结构

![image-20231213222001090](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231213222001090.png)

## Vue的两种Api风格

![image-20231213223137688](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231213223137688.png)

![image-20231213223243013](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231213223243013.png)

我们推荐使用后者（组合式api）

```vue
<script setup>
    import {ref,onMounted} from 'vue';
    //声明响应式数据    ref 响应式对象有一个内部的属性value
    const count = ref(0);//在组合式api中一班需要把数据定义为响应式数据

    //声明函数
    function increment(){
        count.value++;
    }

    //声明钩子函数 onMounted
    onMounted(()=>{
        console.log('vue已经挂载完毕了');
    })
</script>

<template>
    <!--写html元素-->
    <button @click="increment">count: {{ count }}</button>
</template>
```

## 导入Axios依赖

控制台输入

```
npm install axios
```

## 导入Sass依赖

```
npm install sass -D
```



## Api请求的封装

封装到src/api/内的.js文件中

![image-20231214150210981](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231214150210981.png)

```js
export async function articleGetAllService(){
    //发送异步请求获取所有数据
    //同步等待服务器响应的结果，并返回，async，await
    return await axios.get('http://localhost:8080/article/getAll')
    .then(result=>{
        return result.data;
    }).catch(err=>{
        console.log(err);
    });
}
```

需要async关键字异步获取数据

需要await关键字同步等待结果

背模板就好

调用的时候也需要定义异步函数async并同步等待await

导入（@表示src目录）

```js
import {articleGetAllService,articleSearchService} from '@/api/article.js'
```

使用

```js
    const getAllArticle = async function(){
        let data = await articleGetAllService();
        articleList.value = data;
    }
```

## baseURL

为了不用重复写url，和后续修改url方便

定义一个变量，记录公共的前缀

```js
const baseURL = 'http://localhost:8080';
const instance = axios.create({baseURL});
```

后续获得请求时使用instance调用方法即可，不需要前缀

```js
return await instance.get('/article/getAll')
	.then(result=>{
        return result.data;
    }).catch(err=>{
        console.log(err);
    });
```

## 拦截器

![image-20231214151406563](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231214151406563.png)

封装到src/util中，作为request.js

```js
//定制请求示例

//导入axios npm install axios
import axios from 'axios';
//定义一个变量，记录公共的前缀
const baseURL = 'http://localhost:8080';
const instance = axios.create({baseURL});

//添加请求拦截器
instance.interceptors.request.use(
    (config)=>{
        //请求前的回调
        //添加token
        const tokenStore = useTokenStore();
        //判断有没有token
        if(tokenStore.token){
            config.headers.Authorization = tokenStore.token
        }
        return config;
    },
    (err)=>{
        //请求错误的回调
        Promise.reject(err);
    }
)

//添加响应拦截器
instance.interceptors.response.use(
    result=>{
        return result.data;
    },
    err=>{
        alert("服务异常");
        return Promise.reject(err);//异步状态转化为失败的状态
    }
)

export default instance;
```

有了响应拦截器后，在api请求函数中就不需要.then和.catch对结果进行处理

一样先导入

```js
import request from '@/util/request.js';
```

后使用

```js
return request.get('/article/getAll');
```

注意此时api请求函数中的async和await都可以去除了

```js
export function articleGetAllService(){
    return request.get('/article/getAll');
}
```

## Element Plus

提供一些常用的组件（主要是为了好看）

官网

https://element-plus.gitee.io/zh-CN/

安装Element Plus组件库

```
npm install element-plus --save
```

引入依赖

直接把下面这个整个替换掉main.js就行

```js
// main.ts
import { createApp } from 'vue'
import ElementPlus from 'element-plus'
import 'element-plus/dist/index.css'
import App from './App.vue'

const app = createApp(App)

app.use(ElementPlus)
app.mount('#app')
```

如果需要导入中文依赖

```js
// main.ts
import { createApp } from 'vue'//导入vue
import ElementPlus from 'element-plus'//导入element-plus
import 'element-plus/dist/index.css'//导入element-plus的样式
import App from './App.vue'//导入app.vue
import locale from 'element-plus/dist/locale/zh-cn.js'//导入中文包

const app = createApp(App)//创建应用实例

app.use(ElementPlus,{locale})//使用element-plus
app.mount('#app')//控制html元素
```

## 借助URLSearchParams传递

```js
export const userRegisterService = (registerData)=>{
    //借助于urlSearchParams完成传递
    const params = new URLSearchParams();
    for(let key in registerData){
        params.append(key,registerData[key]);
    }

    return request.post('/user/register',params);
}
```

## 解决跨域问题

![image-20231215104807749](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231215104807749.png)

## Vue-Router路由

![image-20231215172038611](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231215172038611.png)

使用方法

1.导入

```js
import {useRouter} from 'vue-router'
const router = useRouter();
```

2.跳转

```js
router.push('/');
```

## 子路由

![image-20231215173854888](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231215173854888.png)

可以使用redirect选择默认展示的路径

```js
const routes = [
    { path: '/login', component: LoginVue },
    {
        path: '/',
        component: LayoutVue,
        redirect:'/article/manage',
        children: [
            {path:'/article/category',component:ArticleCategoryVue},
            {path:'/article/manage',component:ArticleManageVue},
            {path:'/user/info',component:UserInfoVue},
            {path:'/user/avatar',component:UserAvatarVue},
            {path:'/user/resetPassword',component:UserResetPasswordVue},
        ]
    },
]
```

将需要展示的地方更换为router-view

```html
		   <el-main>
                <router-view></router-view>
            </el-main>
```

## Pinia

![image-20231215181235913](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231215181235913.png)

token.js

```js
//定义store
import { defineStore } from "pinia";
import { ref } from "vue";
/*
    第一个参数：名字，唯一性
    第二个参数：函数，函数的内部可以定义状态的所有内容

    返回值：函数
*/
export const useTokenStore = defineStore('token',()=>{
    //定义状态的内容

    //1.响应式变量
    const token = ref('')

    //2.定义一个函数，修改token的值
    const setToken = (newToken)=>{
        token.value = newToken
    }

    //3.函数，移除token的值
    const removeToken = ()=>{
        token.value = ''
    }

    return {
        token,setToken,removeToken
    }
});
```

Pinia持久化插件persisit

Pinia默认是内存存储，刷新浏览器的时候会丢失数据

Persist插件可以将pinia中的数据持久化存储

![image-20240125152327292](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20240125152327292.png)

## 未登录统一处理

![image-20240125153127918](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20240125153127918.png)

## 分页条导入中文语言包

在main.js中添加

```js
import local from 'element-plus/dist/locale/zh-cn.js'
app.use(ElementPlus,{local})
```

## 富文本编辑器

Quill

官网：https://vueup.github.io/vue-quill/

安装

```
npm install npm install @vueup/vue-quill@latest --save
```

**安装：**

```js
npm install @vueup/vue-quill@latest --save
```

**导入组件和样式：**

```js
import { QuillEditor } from '@vueup/vue-quill'
import '@vueup/vue-quill/dist/vue-quill.snow.css'
```

**页面长使用quill组件：**

```html
<quill-editor
              theme="snow"
              v-model:content="articleModel.content"
              contentType="html"
              >
</quill-editor>

```

**样式美化：**

```css
.editor {
  width: 100%;
  :deep(.ql-editor) {
    min-height: 200px;
  }
}
```

