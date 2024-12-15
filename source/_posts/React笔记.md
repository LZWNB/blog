---
title: React学习笔记
date: 2023年4月 --> 2023年6月
category: React 笔记
tags: React 笔记
---

# **Day01**
> jsx语法

* 插值符号 ： {} ； 在标签中可以嵌套Jsx语法<br>
1. 在插值符号里面可以写的内容如下：
    * 表达式
    * 数组
    * 字符串
    * 即时函数
    * 布尔值
    * 三目表达式
2. jsx语法多行注释：
    ``` jsx
    {/*
        这是多行注释
    */}
    ```
    > ！ 注意 ！在写React的时候要区分哪部分是写Js的区块，哪部分是写Jsx的区块！！

3. jsx渲染json数据
    ``` js
    let json = {
        "name":"张三",
        "age":"18",
        "job":"学生"，
        "state":true,
    }
     
     let element = <div>
        <h4>{json.name}</h4>
        <h4>{json.age}</h4>
        <h4>{json.job}</h4>
        <h4>{json.state}</h4> /* 不会直接渲染出字符状态的布尔值 */
     </div>

     ReactDom.render(
        elment,
        document.getElementById("app")
     )
    ```
4. jsx数组遍历
    ``` jsx
    {
    <ul>
        {
            arr.map( (item, idx , self ) => {
                console.log(item)
                return <li key={idx}>  {item} </li>
            })
        }
    </ul>
    }
    ```
    > ！ 注意 ！在遍历的时候，需要加上key；这个key值在开发中最后不要用idx，因为后期会出现diff算法比较的问题！！


 
> 样式处理
1. 行内样式处理
    ``` jsx
        const Element = <div>
            {/* 使用单标签的时候也需要记得闭合标签，且在写样式的时候，键值对的键需要遵循驼峰命名 */}
            <h3 style={{"backgroundColor":"#f90"}}> Hello React </h3>
        </div>

        ReactDom.render(
            Element,
            document.getElementById('app')
        )
    ```
2. 内链样式处理
    ``` jsx
        let style = {"backgroundColor":"#f90",width:"50px",height:"50px"}
        let style2 = {
            s1:{
                "backgroundColor":"#ffo",
                width:"50px",
                height:"50px",
                color:"pink"
                },

            s2:{"backgroundColor":"#0f0",
                width:"50px",
                height:"50px",
                color:"blue"
                }
        }

        const Element = <div>
            <h3 style={style}> Hello React1 </h3>
            <h3 style={style2.s1}> Hello React2 </h3>
            <h3 style={style2.s2}> Hello React3 </h3>
        </div>

        ReactDom.render(
            Element,
            document.getElementById('app')
        )
    ```


> 事件处理

1. 在jsx中引用js的 <kbd>变量</kbd>、<kbd>函数</kbd>、<kbd>对象</kbd>,以及组件的正常写法
    ``` jsx
    <button
        onClick = {function(){alert(123)}}
        > 点击事件1
    </button>
    ```

- - -

# **Day02**

> 复习面向对象
1. 构造函数(es5)
    ``` js
        function Person( name, age, sex ){
            this.name = name;
            this.age = age;
            this.sex = sex; 
        }

        var per1 = Person( "张三" ， 18 ， "男")    // 实例化对象
        var per2 = Person( "李四" ， 19  ， "男")   // 实例化对象
        console.log( per1 )
        console.log( per2 )
    ```
2. 原型共享(es5)
    ``` js
    Person.prototype = fn.prototype
    Person.prototype.sex = "男"

    function Person( name, age, sex ){
            this.name = name;
            this.age = age;
            this.sex = sex; 
        }
    
    function fn(){}
        

        var per1 = Person( "张三" ， 18 ， "男")    
        var per2 = Person( "李四" ， 19  ， "男")   
        var fn1 = new fn(); 
        console.log( per1 )
        console.log( per2 )
    ```

3. 构造函数(es6)
    ``` js
    class Person{
        constructor( name age , sex ){ // 构造器
            this.name = name;*
            this.age = age;
            this.sex = sex; 
        }
    }

    var per1 = new Person( "王五" ， 20 ， "男" );


    console.log( per1 )
    ```
> 组件基础
1. 组件的核心理论概念：
    * 以技能竞赛为例子，三个人合作写项目，每个人负责不同的模块，最好再把各自的模块拼在一起，形成最终的作品，但是考虑到兼容性，编码习惯，往往整合模块这里非常费时间，每个人写的js，css，DOM结构都大不相同
    * 要避免冲突，防止1+1 = -1的情况出现，每个人都有一个自己名字的文件夹，文件夹里面包括<kbd>html</kbd>、<kbd>css</kbd>、<kbd>js</kbd>、三个人合作，就有三个不同名字，模块不同的文件夹，而这三个文件夹，就可以理解为一个独立的<kbd>组件</kbd>，所以，可以简单的理解为，组件就是拥有自己独立的<kbd>html</kbd>、<kbd>css</kbd>、<kbd>js</kbd>的一个模块，通过React，让组件与组件之间可以相互兼容，封装好的组件可以反复多次调用，即插即用
    * React中，有<kbd>函数组件</kbd>渲染静态内容，由<kbd>类组件</kbd>渲染动态内容，以达到页面的最佳性能，是否使用类组件，取决于组件中是否要进行数据管理，<kbd>组件</kbd>负责统一渲染DOM，<kbd>state</kbd>负责统一控制数据。

2. React的核心就是组件，DOM结构交给组件渲染 
    ```jsx
    //组件的常见写法：

    function Sec() {
        return (
            <section>
            <div className="sidebar"> 我是侧边栏 </div>
            <div className="banner"> 我是轮播图 </div>
        </section>
        )
    }


    let Element = <div>
        <h1>这里是组件的内容</h1>
        <header>我是头部组件</header>
        <Sec></Sec>
        <footer> 我是底部组件 </footer>

    </div>

    ReactDom.render(
        Element,
        document.getElementById("app")
    )
    ```
> 有状态组件

 