 



# Vue的学习

## 一：什么是vue？

1. 构建用户界面 
   1. 使用vue在html中填充数据
2. 框架
   1. 框架是一个现成的解决方案，程序员可以只能遵守框架里面的内容

## 二：vue的两个特性

1. 数据驱动视图 

   1. 数据的变换会自动驱动视图的更新（程序员只管把数据维护好）
   2. <img src="C:\Users\FeiMao\AppData\Roaming\Typora\typora-user-images\image-20220703170004920.png" alt="image-20220703170004920" style="zoom: 150%;" />
   3. 上方这张图是数据的（单向的数据绑定）

2. 数据双向绑定

   > ​	在网页中有form表单这些控件可以采集数据，当我们使用vue绑定了这些表单如果表单或者数据源发生了变化那么就会自动更新数据 
   >
   > ![](C:\Users\FeiMao\AppData\Roaming\Typora\typora-user-images\image-20220703171103814.png)c

   

## 三：MVVM思想理解

+ M是指modue泫然页面时的数据（Model数据源）
+ V是指当前渲染页面的Dom结构（View视图）
+ vm是指vue的实例，是MVVm的核心（ViewModel  vue的视图模型）



## 四：vue的初体验

+ 导入vue的文件

+ 在页面中声明一个需要被vue控制的区域

+ 实例化一个vue对象

  关系图

  ![image-20220703175849409](C:\Users\FeiMao\AppData\Roaming\Typora\typora-user-images\image-20220703175849409.png)

______



## 五：指令

+ **指令是vue提供给我们给渲染dom元素中的文本内容（比较简单）**

  **内容渲染指令**
  
  + **{{   }}** :	不会覆盖标签里面的内容  
  + **v-txt**：会覆盖原本标签里面的内容
  + **v-html**：可以渲染html标签
  + 可以在插值表达式中进行一定的运算
  
  **属性绑定指令** 
  
  + **v-bind** :可以用于绑定比如input  src等自定义属性
  + 可以简写为 ：
  
  **事件绑定指令**
  
  + **v-on:click="Usersubmit**：方法一
  
  + **@click="Usersubmit（$event）**：方法二 这里面有一个事件对象e
  
  + 事件函数需要定义在methods 对象中
  
  
  
  ​	事件修饰符
  
  1. **prevent**:组织默认行为
  2. **stop**：阻止事件的冒泡‘
  
  1. 按键修饰符
     1. **@keyup.enter="submit"：**可以设置按下某些案件自动执行函数
  
  **双向绑定指令**
  
  + **v-model** ：这个指令是数据的双向绑定，只可以在input控件中使用（v-bind是一个单向的数据绑定）
    + 双向绑定的事件修饰符
      + .**number**  将字符串转换成数值类
      + .**trim** 在失去焦点的时候去除头尾的空格
      + .**lazy** 在失去焦点的时候更新数据而非在获取焦点的时候更新数据
  
  **条件渲染指令**
  
  + ````html
    <!-- v-if 是需要显示就渲染出来不需要显示出来就会重新渲染 -->
    <h1 v-if="count == 0">我是肥猫我要冲冲冲</h1>
    
    <!-- v-show 是使用display:node进行隐藏元素 -->
    <h2 v-show="count ==0">我是FeiMao@100我要冲冲冲</h2>
    ````
  
  + v-if :页面刚刚开始创建的时候会自动渲染 如果需要进入页面不需要展示的话那么 v-if 性能会更好
  
    + v-if多重判断指令的使用
  
    + ````html
      <h1 v-if="count == 0">我是肥猫我要冲冲冲</h1>
      <h2 v-else-if="count == 1">A</h2>
      <h2 v-else>B</h2>
              
      ````
  
      
  
  **循环渲染指令**
  
  +   **v-for="(item,index) in brand" :key="item.id"**
    + 渲染指令里面参数有两个 有一个index是可选参数    当然每次循环的时候需要设置一个key 参数（id需要为数值或者字符类型） 否在后续的模块中会报错
  
  
  
  
  
## 六：过滤器filter

 

  + 过滤器就是处理文本内容,将前面的值传给后面的过滤器，然后由后面的过滤器再次处理
  
  + 过滤器后面就是一个管道 | 将值传过去的时候就会进行过滤函数的执行，可以进行多次的过滤函数的执行
  
    
  
  + 局部过滤器
  
    + ````
        <p>{{ count | Apps | getapp }}</p> 
      //过滤器
         filters: {
            getapp(value) {
               return value.toLowerCase()
            },
            Apps(value) {
              return value.toUpperCase()
                  }
              }
      
      ````
    
  + 全局过滤器(必须写在vue创建vue实例的前面)
  
    + ````
      Vue.filter("mmt", function (value) {
              return value.substring(0, 3)
          })
      ````
    
    + 上面两个过滤器 如果发生重名的问题那么会**优先读取局部的过滤器** 而不是读取全局的过滤器
    
      
    
    + 问：全局过滤器在什么时候使用呢?
    
    + 答：在多个vue实例对象的时候需要使用同一个方法的时候便可以使用全局过滤器
    
      
    
      
## 七：侦听器Watch



+ 侦听器就是可以用于进行监听data中的数据并返回某些值

+ **Watch 侦听局部的数据变化(应用场景一般是判读是否有重名的像现)**

+ ```html
  <body>
      <div id="app">
          <p>{{ username }}</p>
          <input type="text" v-model="username">
      </div>
  </body>
  
  </html>
  <script>
      let vm = new Vue({
          el: "#app",
          data: {
              username: "FeiMao@110",
              count: "abcdefg",
              abc: "123",
          },
          watch: {
              //这里面有两个参数第一个是修改后的值
              //第二个是未修改的值
              username: function (newvalue, oldvalue) {
                  console.log('我变化了');
                  console.log(valuea)
                  console.log(valueb)
              }
          }
  
      })
  </script>
  ```

  

+ 进入页面自动执行一次 （对象格式的侦听器）   **immediate参数**

+ ```javascript
  
  <body>
      <div id="app">
          <p>{{ username }}</p>
          <input type="text" v-model="username">
      </div>
  </body>
  
  </html>
  <script>
      let vm = new Vue({
          el: "#app",
          data: {
              username: "FeiMao@110",
          },
          watch: {
              username: {
                  //表示自动监听如果被修改了值那么会自动变化
                  handler(newvalue, oldvalue) {
                      console.log(newvalue, oldvalue);
                  },
                  //表示一进入网页就会自动执行一次
                  immediate: true,
              }
          }
  
      })
  </script>
  ```



+ **需要监听深度对象数据/deep**

+ ```javascript
   watch: {
              username: {
                  //表示自动监听如果被修改了值那么会自动变化
                  handler(newvalue, oldvalue) {
                      console.log(newvalue, oldvalue);
                  },
                  //表示一进入网页就会自动执行一次
                  immediate: true,
              }
          }



+ 总结：

  + immediate：进入页面的时候自动执行
  + deef：监听深度的对象数据
  + handler：监听





##  八： 计算属性

+ computed计算属性就是可以将在处理数据的一些逻辑抽离出进行计算 这样可以使得模板简介易懂

  + 计算属性会将计算的结果缓存，如果多次调用的话会自动从缓存中读取数据

````js
<body>

      <div id="app">
          <h1>{{  splicin }}</h1>
          <h1>{{  splicin }}</h1>
          <h1>{{  splicin }}</h1>
          <h1>{{  splicin }}</h1>
          <hr>
      </div>

  </body>

  </html>

  <script>
      let vm = new Vue({
          el: "#app",
          data: {
              objs: [{
                  username: "FeiMao@110",
                  age: 20,
                  sex: "♂",
                  interest: "骑自行车"
              }]
          },
          computed: {
              splicin(a) {
                  let str = ""
                  //将数据拼接起来
                  this.objs.forEach(element => {
                      for(let k in element){
                          str += element[k] + "|"
                      }
                  });
                  return str;
              }
          }
      })
  </script>


````


+ 计算属性通常用于数据的计算





## 九：Vue-cli工具

+ **什么是单页面程序?**
   1. 单页面应用程序简称 “SPA” 顾名思义，就是在一个web网站中只有一个页面，所有的功能和交互都在这一个页面中完成  列如“网易云音乐”就是单页面应用程序   ，复杂度比较高
   
+	 **什么是Vue-cli**
   
   1. vue-cli是vue.js开发的标准工具。它简化了程序员基于webpack 创建工程化的Vue项目的过程
   1. 这样程序呀可以专注于编写应用程序，而不必花上好几天去纠结webpack配置的问题
   
+	**安装Vue-cli**
   
   1. vue-cli 是npm上的一个全局包，使用npm install命令，即可方便把它安装到自己的电脑上
      1. 使用 ：npm install -g @vue/cli 
      
   2. 创建工程化文件（在需要生成项目的目录敲命令）
      1. vue create 项目名称
      
   3. 命令行中的选择：
   
      1. ![](C:\Users\FeiMao\AppData\Roaming\Typora\typora-user-images\image-20220705203731659.png)
      
      2. ![image-20220705213238839](C:\Users\FeiMao\AppData\Roaming\Typora\typora-user-images\image-20220705213238839.png)
      
      3. ![image-20220705213329824](C:\Users\FeiMao\AppData\Roaming\Typora\typora-user-images\image-20220705213329824.png)
      
      4. ![image-20220705213418592](C:\Users\FeiMao\AppData\Roaming\Typora\typora-user-images\image-20220705213418592.png)
      
      5. ![image-20220705213714021](C:\Users\FeiMao\AppData\Roaming\Typora\typora-user-images\image-20220705213714021.png)
      
      6. ![image-20220705213910502](C:\Users\FeiMao\AppData\Roaming\Typora\typora-user-images\image-20220705213910502.png)
      
      7. ![image-20220705213959575](C:\Users\FeiMao\AppData\Roaming\Typora\typora-user-images\image-20220705213959575.png)
      
      8. ![image-20220705214219167](C:\Users\FeiMao\AppData\Roaming\Typora\typora-user-images\image-20220705214219167.png)
      
         如果发生了暂停下载那么就只需要选中这个窗口然后按一下 CTRL+ C
      
      10. ![image-20220705214518142](C:\Users\FeiMao\AppData\Roaming\Typora\typora-user-images\image-20220705214518142.png)
      
      安装完成
      
      
   
+ **如何使用vue-cli **

   1. 进入项目根目录（cd 项目名称）

      ![image-20220705215012651](C:\Users\FeiMao\AppData\Roaming\Typora\typora-user-images\image-20220705215012651.png)

   2. 运行项目（npm run serve）

      ![image-20220705215146893](C:\Users\FeiMao\AppData\Roaming\Typora\typora-user-images\image-20220705215146893.png)

   3. 运行效果

      ![image-20220705215238110](C:\Users\FeiMao\AppData\Roaming\Typora\typora-user-images\image-20220705215238110.png)

   4. 文件夹介绍![image-20220705221301235](C:\Users\FeiMao\AppData\Roaming\Typora\typora-user-images\image-20220705221301235.png)





+ **vue的工作流程**

   + 在工程化中 vue做的事情很简单只需要将main.js把app.js的文件渲染到指定的区域、

   + 组件的组成结构：

      + ````javascript
        	 
         <template>
           <div id="app">
             <h1>{{ name }}</h1>
           </div>
         </template>
         
         <script>
         export default {
           el: "#app",
           data() {
             return {
               name: "Feimao@110",
             };
           },
         };
         </script>
         
         
         <style>
         h1 {
           background: red;
         }
         </style>
         ````

   注意事项

   1. 组件中的数据源 data 必须要设置为一个函数返回出去
   2. 组件中只能有一个根节点
   3. 组件中的this只指向当前的组件的实例对象 
   4. 组件中只能有一个根节点 



less的启动语法

+ 在style 上面添加一个lang=“less”属性

````html
<style lang="less">
div {
  background: pink;
  h1 {
    background: red;
  }
}
</style>
````



____



	## 十：组件的使用及注册

组件在使用的时候才会产生关系



**使用组件的三个步骤**

1. 导入组件

2. 注册组件  **(通过component 注册的组件都是私有的组件)**

3. 使用组件

   1. ```javascript
      template>
        <div id="app">
          <h1>别来无恙</h1>
          <!-- 使用组件 -->
          <div class="box">
            <Left></Left>
            <Rigth></Rigth>
          </div>
        </div>
      </template>
      
      <script>
      //01: 导入需要的组件
      import Left from "../src/components/Left.vue";
      import Rigth from "../src/components/Right.vue";
      
      //02：注册组件
      export default {
        components: {
          Left,
          Rigth,
        },
      };
      </script>
      ```

      

​		**如何注册全局组件	**

+ 在main.js写入以下代码

+ ````js
  import Vue from 'vue'
  import App from './App.vue'
  
  //01 导入组件名称
  import Count from './components/Count.vue'
  
  //02 注册组件 
  Vue.component('MyCount',Count)
  
  
  Vue.config.productionTip = false
  
  new Vue({
    render: h => h(App),
  }).$mount('#app')
  
  ````

+ 使用的的时候就像标签一样使用（当然不可以将全局的组件使用在注册的组件中 ，这样会自己调用自己）



![image-20220713101116659](C:\Users\FeiMao\AppData\Roaming\Typora\typora-user-images\image-20220713101116659.png)

## 十一：自定义组件参数

+ props中的模板数据是可以在模板字符串中解释出来的

+ porps 的数值是只读的，所以我们需要在data中声明一个数据接收一下

+ 父组件传递的参数是可以设置动态的数据传递给子组件中

  

+ **如何使用Props 自定义组件**

  + 在公共的组件中写入props 里面是一个数组，填入需要自定义的名称、

  + ````js
     //props是组件的自定义属性，在封装通用的组件的时候，合理的使用 props 可以极大的提高组件的复用性
      //props只能读而不可以修改
      props: {
        val:{
           type:Number,//设置一下类型
         },
     
         //这里如果选了必填和设置了默认值那么还是需要传递数值，不然会报错
         max:{
           type:[Number,String],//传递的数据类型可以为数组里面的类型
           required:true,//必填的选项
           default:100,//设置默认值
         },
         os:{
           default:'1',
           //这里是自定义的属性，设置值必须是数组里面的元素
           validator:function(value){
             return ['1','2','3'].indexOf(value) != -1;
           }
         }
       },
     ````
     
  + **如何传值**（使用的时候就在调用的组件中填写(由于传入的值的类型返回的是一个字符串 所以我们使用v-bind进行类型的修改)）
  
  + ```html
    <template>
      <div id="Left">
        <h1>Left</h1>
        <MyCount :init="10"></MyCount>
      </div>
    </template>
    ```
  
  + **组件中的几个参数**
  
    + default ：默认值（如果没有传入值那么就会使用默认值）
    + type      ：值类型
    + required：必填项（必须传入值否则报错）









## 十二：组件之间的样式冲突

+ 在单页面程序中，会有很多的模块组合在一起，拥有不同样式的模块就会产生样式冲突

  

+ 解决方法

  + 在每一个模块中的样式标签 添加一个scoped 标签添加这个属性后当前模块的样式只会作用于当前模块而不会影响其他的模块



+ 父改子样式
  + /deep/ h2 这样做的话就可以在父级修改子集模块的样式
+ 小插曲
  + 在vue渲染的页面上都先编译在注入道页面上的







## 十三：生命周期

+ 生命周期 是指一个组件从   创建- 运行->销毁的整个阶段，强调的是一个时间段
+ 生命周期图解
  + ![image-20220714100701121](C:\Users\FeiMao\AppData\Roaming\Typora\typora-user-images\image-20220714100701121.png)

+ **创建阶段的函数**
  + **beforeCreate**：
    + 这个函数中不可以访问 props/data/methods 函数
  + **created**：
    + 可以访问到 props/data/methods 等配置方法 ，一般用于发送Ajax请求数据保存在data中,不可以获取Dom元素
  + **beforeMount**：
    + 将内存中渲染好的Dom结构编译出来，但是还未渲染到页面上，此时还不能获取Dom结构
  + **mounted**：
    + 此时已经将Dom结构渲染到页面上了，可以获取Dom结构了



+ 组件的运行阶段
  + **beforeUpdate**：
    + 此时页面是旧的但是数据是新的，页面的Dom结构还未更新
  + **update**：
    + 此时数据和页面都同步一致都为最新的数据了（需要获取最新的数据和DOM结构那么就在这个阶段去做）



+ 组件的销毁
  + **beforeDestroy**：
    + 将要销毁组件，但是组件还在运行阶段
  + **Destroy**：
    + 成功销毁组件，此时DOM结构已经完全移除掉了





+ 常用的阶段函数
  + **created**：组件初始化数据的时候
  + **mounted**：组件渲染到页面上的时候
  + **update**：页面和数据都是最新的数据了













## 十四：数据的共享



+ **父级传子**
  + props：自定义属性
  
+ **子传父级**

  + 自定义事件
    + ![image-20220714164425369](C:\Users\FeiMao\AppData\Roaming\Typora\typora-user-images\image-20220714164425369.png)

+ **兄弟之间**

  + EventBus

    + ![image-20220714164918272](C:\Users\FeiMao\AppData\Roaming\Typora\typora-user-images\image-20220714164918272.png)	

    + ![image-20220714170427204](C:\Users\FeiMao\AppData\Roaming\Typora\typora-user-images\image-20220714170427204.png)






###	14.0.1ref引用

 + 我们需要操作Dom的时候就可以设置一个ref属性方便我们操作dom元素

 + 只要给元素添加了一个ref属性那么这个元素就会存在于ref中

   + ref是一个对象，里面包含了我们设置的多个元素

   + 如何设置ref属性

     + ```html
        <h3 ref="abcd">ref 引用</h3>
       ```

   + 如何获取ref元素

     + ```js
         this.$refs.abcd.style.color = 'red'
         
       ```

   + ref 可以用于获取不同组件中的方法，比如我需要清空子组件中的数据那么就可以将子组件添加一个ref 然后再点出来

   + Ref 可以用于传输数据给父级或者子集（嘿嘿 很方便）

​	

​	





## 十五：component 动态组件

+ ​	动态组件就是通过一个参数来控制组件显示与隐藏

+ **component**的使用

  + **keep-alive**：用于缓存数据（比如一个组件中需要保留数据那么就可以使用这个）

  + **component :is：**用于判断展示组件的名称

  + **include="Left,Rigth"**  ：用于需要缓存数据的组件 ，多个组件使用英文,分隔开、

  +  **exclude="Rigth"**：用于排除掉这元素的缓存数据

  + ````js
    <template>
      <div id="app">
        <button  @click="coName = 'Left'">Left</button>
        <button @click="coName = 'Rigth'" >Right</button>
    
        <!-- 动态组件的渲染 -->
        <keep-alive include="Left,Rigth">
          <component :is="coName"></component>
        </keep-alive>
    
      </div>
    </template>
    
    <script>
            
     //组件的导入
    import Left from "@/components/Left.vue";
    import Rigth from "@/components/Rigth.vue";
    
    
    export default {
     //声明一个数据来控制
      data(){
        return {
          coName:"Left"
        }
      },
    
      //注册组件
      components: {
        Left,
        Rigth,
      },
    };
    ````

		### 15.0.1：组件的name名称

 +	当我们组件中设置了一个name属性那么组件的名称就为这个，否则就为注册的时候的名称

```js
export default {
 //组件的name名称  
 name: "A",
 data() {
  return {
   count: 0,
  };
 },
```









_______________________









## 十六：插槽

+ **插槽：**就是让用户自定义数据

  **插槽默认**：是default 只要使用插槽的方向未给定参数那么就会将内容渲染到默认的插槽是

  **具名插槽**：设置了name值 

   **后备内容**： 只要设置了具体的名字但是未使用插槽那么就会将插槽里面默认的内容自动填入

  **v-slot**：这个属性只能使用在template 和 compoent 标签

  **子传父级**：可以在插槽中设置一个属性，然后在使用的时候就可以获取这个对象数据默认是一个空对象

+ **插槽在component的使用**
+ ![image-20220721185912687](C:\Users\FeiMao\AppData\Roaming\Typora\typora-user-images\image-20220721185912687.png)



+ **插槽在template 中的使用**
+ ![image-20220721190850750](C:\Users\FeiMao\AppData\Roaming\Typora\typora-user-images\image-20220721190850750.png)











____________________

## 十七：自定义指令

+ **自定义指令**

  

  + **私有自定义指令（只能在当前的组件中使用）**

    

    + **directives**：是声明自定义指令的节点\
    + **bind**：参数只会在调用的时候执行一次

    ````javascript
    
     //自定义指令的节点
      directives: {
        color: {
          //当color指令被绑定的时候就会触发bind指令函数
          //我们也可以传入值过来
          //使用一个形参接收
          bind(e,binding) {
            console.log(binding);
            //当指令被绑定的时候会自动触发绑定的Dom元素
             setTimeout(()=>{
               e.style.background = binding.value;
             },2000)
          },
        },
      },
    ````

    ````html
    //自定义指令的使用
    //如果只想传入值进去那么就需要设置一下 一个单引号  反之就不用
    <Rigth v-color="'red'">
    </Rigth>
    ````

  + **update**函数

    + **update**函数可以在**Dom**变化的时候执

    + ````javascript
       directives: {
          color: {
            //  //当color指令被绑定的时候就会触发bind指令函数
            bind(e, binding) {
              console.log(binding);
              setTimeout(() => {
                e.style.background = binding.value;
              }, 2000);
            },
        
            //当指令被绑定的时候会自动触发绑定的Dom元素
            update(e, binding) {
              console.log(binding);
              setTimeout(() => {
                e.style.background = binding.value;
              }, 2000);
            },
          },
        },
      ````

  + **bind和update中的函数指令都一致**那么就可以直接将指令设置为一个函数

    + ````javascript
       
          //如果bind和update 中的函数是一致的话那么就可以定义为一个函数
          color(e, binding) {
              e.style.background = binding.value;
          },
      ````

  

  + **全局自定义指令**

    + 全局自定义组件定义在main.js中无论在那个模块中都可以使用这个全局自定义属性

    + 语法

      + ```js
        
        Vue.directive('colors',function(e,binding){
          e.style.color = binding.value
        })
        ```

## 十八：Eslint

​	Eslint是一个javascript的规范工具

​	官方：https://eslint.bootcss.com/docs/rules/



默认的规则 

![image-20220722213803064](C:\Users\FeiMao\AppData\Roaming\Typora\typora-user-images\image-20220722213803064.png)

​	如果你需要修改默认的规则那么就可以在eslitrc.js中修改了

<img src="C:\Users\FeiMao\AppData\Roaming\Typora\typora-user-images\image-20220722212026818.png" alt="image-20220722212026818" style="zoom: 80%;" />

（建议别用，太害人了，呜呜呜）









_____________







## 十九：Axios 中的一些问题



+ 存在的问题

  + 在每一个模块中如果都需要请求数据那么就需要在每一个模块中引入axios模块并发送请求

    + 解决方法：将axios 挂载到vue的原型中   vue.prototype.axios = axios 

    

  + 因为请求的数据是一个数据接口，后端如果修改了接口名称那么，所有的模块请求的接口都需要修改，太麻烦了需要确定一个接口

    + 解决方法：在挂载到原型之前设置  axios.defaults.baseURL='http://localhost:8080'

    

+ 以上的解决方法，还是会出现问题，接口的复用性不高，比如很多个地方需要请求同样的数据那么就需要每一个地方都需要请求数据









## 二十：路由（router）

路由：Hash 哈希地址与组件之间的对应关系

哈希地址：不会跳转页面，只会在当前的页面进行变化，但是会产生历史记录

前端路由的工作方式：![image-20220725092527442](C:\Users\FeiMao\AppData\Roaming\Typora\typora-user-images\image-20220725092527442.png)



![image-20220725092857824](C:\Users\FeiMao\AppData\Roaming\Typora\typora-user-images\image-20220725092857824.png)









### 安装和配置路由

+ 安装 vue-router路由包

  + npm install vue-router@3.5.2  -S

+ 使用：

  + 再src目录下新建一个文件夹 叫 router   再里面新建一个index.js 文件

  + 然后在里面添加这些代码

  + ````javascript
    //导入模块
    import Vue from "vue";
    import VueRouter from "vue-router";
    
    
    
    //导入,模块
    import home from '../components/home.vue'
    import move from '../components/move.vue'
    import personal from '../components/personal.vue'
    
    import tab1 from '../components/tab1.vue'
    import tab2 from '../com{ponents/tab2.vue'
    
    
    
    //给vue装插件
    Vue.use(VueRouter);
    
    
    //实例化对象
    let router = new VueRouter({
      //配置好路由地址 , 及显示的模块
      routes: [
    
        //路由重定向redirect
        { path: '/', redirect: '/home' },
        { path: '/home', component: home },
        { path: '/move', component: move },
    
        //嵌套路由
        {
          path: '/pre',
          component: personal,
          // 这里是为了 重定向到 tab1 让其默认显示
          // redirect: '/pre/tab1',
          children: [
    
            //默认子路由,某个path 默认为 空那么就可以设置需要显示的组件了
            { path: '', component: tab1 },
            { path: 'tab1', component: tab1 },
            { path: 'tab2', component: tab2 },
          ]
        },
      ]
    });
    
    
    //导出
    export default router 
    ````

  + App2.js

    + ````html
      <template>
        <div id="app">
          <h1>路由展示</h1>
          <ul>
            <!-- 路由的地址 -->
            <!-- <li><a href="#/home">首页</a></li>
            <li><a href="#/move">电影</a></li>
            <li><a href="#/pre">个人</a></li> -->
      
            <!-- 我们可以使用 route-link 用来替换a链接 -->
            <router-link to="/home">首页</router-link>
            <router-link to="/move">电影</router-link>
            <router-link to="/pre">个人</router-link>
          </ul>
            
          <hr />
          <!-- 一个模块的占位符 -->
          <router-view></router-view>
            
            
        </div>
      </template>
      
      <script>
      export default {};
      </script>
      
      </style>
      ````





###  路由的动态



+ **如何实现动态的路由传参数：index.js中 添加一个 英文的 ：符号**

```js
 {
      //通过id 
      path: '/move/:id',
      component: move,
  },
```



+ **路由的另一种传参**

```js
index.js 中 
  {
      //通过id 
      path: '/move/:id',
      component: move,
     //这里是开放窗口将 id传给组件
      props: true
  },
      
   
  当然在被显示的组件中需要设置 props :["id"] 这个属性  
```





+ **如何获路由 问号？后面的内容**

```javascript
   console.log(this.$route.query);
   console.log(this.$route.fullPath);

    query:是一个对象格式的参数
    fullpath：是一个完整的路径包括参数
    path ：只是一个路径不包括查询参数
```





+ **导航方式**

  + 声明式导航：比如点击 a链接和 vue中的 <router-linkj>标签都属于声明式导航

    

  + 编程式导航：在浏览器中调用API方法实现的导航方式都为编程式导航，例如 location.href 跳转到新的页面的方式属于编程式导航

    + vue-router 中提供了几个常用的编程式导航方式

      + |                       方法                       | 特点                                     |
        | :----------------------------------------------: | :--------------------------------------- |
        |         this.$router.push('hash 地址');          | 会产生新的历史记录可以返回               |
        |        this.$router.replace('hash 地址');        | 替换当前的历史记录                       |
        |               this.$router.go(-1);               | 可以控制前进或者后退  go方法一般用于后退 |
        |  <button @click="$router.back()">后退</button>   | 后退简化的写法                           |
        | <button @click="$router.forward()">前进</button> | 前进的简化写法                           |



+ **导航守卫  *（还有更多的守卫需要去学习）**

  + 全局前置守卫

  + ````javascript
    //只要发生了路由的跳转那么就会 触发beforEach 指定的回调函数
    router.beforeEach(function (to, from, next) {
    
      //to 表示将要访问的路由信息
      console.log(to)
    
      //from :表示将要离开的路由信息
      console.log(from)
    
      // next(true) :表示放行的意思通过Boolean值来控制
      next()
    
    })
    ````

    ![image-20220726180843110](C:\Users\FeiMao\AppData\Roaming\Typora\typora-user-images\image-20220726180843110.png)







_________________









## 二十一 ：vant 一个优秀的移动端组件库

官网：http://vant-contrib.gitee.io/vant/#/zh-CN/quickstart

+ ​	安装
  + 因为目前我们使用的vue 2.0 所以呢 就使用 这个命令安装    npm i vant@latest-v2
  
  + 
  
  + 
  
    











## 二十二：ES6模块化

+ 在ES6模块化之前有：AMD，CMD，CommonJS等模块化规范，但是这些模块化规范不一致导致增加了学习成本和开发成本，因此大一统的ES6 模块化规范诞生了，因此大一统的ES6 模块化规范诞生了
+ ES6的定义
  + 每一个js文件都是一个模块
  + 导入对象使用 **import** 关键字
  + 导出对象使用 **export** 关键字



+ 几种导出方式



+ **默认导出**

  + 导出元素

  + ```js
    
    let a = 10;
    function Show(value1, value2) {
      return value1 + value2;
    }
    
    
    
    //导出 
    export default {
      a: a,
      Show: Show,
    }
    ```

  + 导入元素

  + ```js
    //使用from 
    import A from './A.js'
    
    console.log(A.a);  //{ a: 10, Show: [Function: Show] }
    console.log(A.Show(10, 20));
    ```

  + 默认导出：只能导出一次

  + 默认导入：接收的名称可以随意只需要合法就可以 

    

+ **按需导出**

  + 导出元素

  + ```js
    export let a = 10;
    export let b = 20;
    export function show() {
      return a + b
    }
    ```

  + 导入元素

  + ````js
    //按需导出需要名称一致  但是可以通过 as 进行修改
    //可以配置默认导出来操作，默认导出的不在花括号内，按需导出的是在花括号内的
    import infot, { a as c, b, show } from './A.js'
    
    console.log(c);
    console.log(b);
    console.log(show());
    
    
    console.log(infot)
    ````

    导出：导出的时候可以多次导出

    导入：导入的时候名称必须要和导出的名称一致   可以通过 as 进行修改









## 二十三：Promise 

![image-20220805163725017](C:\Users\FeiMao\AppData\Roaming\Typora\typora-user-images\image-20220805163725017.png)

+ **为了解决回调地狱的问题	ES6推出了 promise 来解决这个问题**

  + promise 是一个构造函数

  + 我们可以创建 promise 的实例 const p = new Promise

  + new 出来的一个 实例就是一个异步操作对象

    

+ **基础的 promise 使用**

  + ```js
    let a = 1;
    
      //创建Promise 实例对象
      //resolve ：成功的回调函数
      //reject 失败的回调函数
      let p1 = new Promise(function (resolve, reject) {
        if (a == 1) {
          resolve(a);
        } else {
          reject("err");
        }
      })
      //.then 是用于成功的回调函数（必须要的）
      //.catch 是用于失败的回调函数（可选的）
      p1.then(value => {
        console.log(value);
      }).catch(err => {
        console.log(err)
      })
    ```

  

+ **.then 和.catch 的使用 解决回调地狱**

  + 在比如获取多个数据的情况下，如果平级的使用promise对象那么会发生一些特殊情况  读取的顺序可能会不一样

    

  + 这就需要使用到.then 的新特性了  **使用 .then 的新特性**

    

    +  **如果上一个promise对象返回的是一个 promise对象那么可以交给下一个 .then 进行处理**
    + **.catch 可以获取 到全部的错误，如果没有捕获到错误那么就后面的代码都不会执行，所以可以在.then后面添加catch**

  + ```javascript
    
      //封装的一个 返回promise对象的一个函数
      function addPromise(val) {
        return new Promise((resolve, reject) => {
          if (val == val) {
            resolve(`成功0${val}`);
          } else {
            reject("失败01");
          }
        })
      }


      //如果上一个promise对象返回的是一个 promise对象那么可以交给下一个对象进行处理
      addPromise(1).then(value => {
        console.log(value);
        //返回一个promise对象给下一个 .then函数进行处理
        return addPromise(2)
      }).then(value => {
        console.log(value);
        //返回一个promise对象给下一个 .then函数进行处理
        return addPromise(3)
      }).then(value => {
        console.log(value)
        
        //而 cathc 可以只写一个，会捕获上面的所有的错误
      }).catch(error => {
        console.log(error);
      })


​    


    ```

___

  

+ Promise.all

  + 返回的数据是一个接收数据的一个数组，数组中的顺序是什么，那么返回的数据顺序也是这样的

  + ```javascript
    //Promise.All 
      function addPromise(val) {
        return new Promise((resolve, reject) => {
          if (val == val) {
            resolve(`成功0${val}`);
          } else {
            reject("失败01");
          }
        })
      }
    
    
      //数组中分贝为三个返回promise的对象
      let arrs = [addPromise(1), addPromise(3), addPromise(3)];
    
    
      //使用promise.all 可以一次性返回多个数据
      Promise.all(arrs).then(value => {
        console.log(value);
        // /['成功01', '成功03', '成功03']
      }).catch(errs => {
        console.log(errs)
      })
    ```

  

+ Promise.race

  + race是一个赛跑机制,谁先返回就先返回谁的数据

  + ```javascript
    
      //Promise.All 
      function addPromise(val) {
        return new Promise((resolve, reject) => {
          if (val == val) {
            resolve(`成功0${val}`);
          } else {
            reject("失败01");
          }
        })
      }
  
  
      //数组中分贝为三个返回promise的对象
      let arrs = [addPromise(1), addPromise(3), addPromise(3)];
        
      //使用promise.race 谁返回的速度快就.then 
      Promise.race(arrs).then(value => {
        console.log(value);
        //"成功01"
      }).catch(errs => {
        console.log(errs)
      })
    ```
  
  + 









## 二十四：大型购物车项目总结

+ 写了大概25天左右的这个购物商城项目，对我来说学到了很多东西，庆幸我可以坚持写完这个项目.
+ 以下是我对于这个项目的总结



### 一：使用技术栈

+ **Vue.js** /是一个流行的前端框架
+ **Javascript** /是一个脚本语言
+  **Vue-cli** /vue的脚手架
+  **axios** /网络请求服务模块
+  **npm** /包管理工具
+  **git** / 版本控制工具
+ **elemtnUi** /饿了么团队开发的框架
+  **mock** / 模拟的虚拟数据





### 二：项目结构

+ 模块介绍
  + **public** ：放置公共的资源
  + **src**：放置需要我们常用的模块
    + **api** ：请求的API接口
    + **assets**：公共资源
    + **commpoents**：公共的资源比如说 头部模块和底部模块
    + **mork** ：模拟的假数据
    + **page**：里面放各个模块
    + **router**：路由模块
    + **store：Vuex**仓库
    + **utlis**：公共的API
  + **App.vue**：渲染的路口文件
  + **main.js**：渲染的主要文件
  + **package.json** ：表示安装的第三方包存储目录
  + **vue.config.js** 用于配置vue







## 三：知识点

### **一：eslint**

+ 关闭eslint校验工具
  创建vue.config.js文件：需要对外暴露
  module.exports = {
     lintOnSave:false,
  }



### 二：设置使用@替代src 

+ 3.3 src文件夹的别名的设置 因为项目大的时候src（源代码文件夹）：里面目录会很多，找文件不方便，

+ 设置src文件夹的别名的好处，找文件会方便一些 创建jsconfig.json文件

+ ```js
  {
   "compilerOptions": {
    "target": "es5",
    "module": "esnext",
    "baseUrl": "./",
    "moduleResolution": "node",
    "paths": {
     "@/*": [
  ​    "src/*"
     ]
  }
  ```

+ 

  

### 三：vue-router 路由

+ 

+ 
  安装vue-router ：npm install  vue-router@2.5.2 
  + 路由其实就是BOM中的哈希值通过判断哈希值来进行跳转页面

  + 路由中的配置参数

    + { path: '/shopcart', name: 'shopcart', component: ShopCart, meta: { show: true } },//购物车页面
      + pathc ：是路由模块
      +  name ：是路由名称
      + component：模块
      + meta：传递的参数（通常我们可以配置这个参数进行再某些模块不显示什么东西呢）

  + **使用步骤**

    + 导入vue-router
    + 导入模块
    + 创建路由实例
    + 模块挂载到路由上
    + 路由守卫（后期看情况是否添加守卫）

    + **路由的参数**
    + **params** :这个参数需要占位，不然会报错，如果没有传递参数那么需要添加以一个问好？
    + **query**：路由不需要占位，写法类似于ajax当中query参数  
      + 两个参数的面试题
        + **路由传递参数先关面试题**
          + **路由传递参数（对象写法）path是否可以结	合params参数一起使用?**
            + 不可以：不能这样书写，程序会崩掉
          + **如何指定params参数可传可不传?** 
            + 使用问号？
          + **params参数可以传递也可以不传递，但是如果传递是空串，如何解决？**
            + 判断并添加一个undefined
          +  **路由组件能不能传递props数据?**
            + 可以直接传





### 四：编程式导航与声明式导航

+ $router:进行编程式导航的路由跳转

  + this.$router.push|this.$router.replace

+ $route:可以获取路由的信息|参数

  + this.$route.path 
  + this.$route.params|query
  + this.$route.meta

+ 程式导航路由跳转到当前路由(参数不变), 多次执行会抛出NavigationDuplicated的警告错误

  + 注意:编程式导航（push|replace）才会有这种情况的异常，声明式导航是没有这种问题，因为声明式导航内部已经解决这种问题。
    这种异常，对于程序没有任何影响的。
    为什么会出现这种现象:

  + 由于vue-router最新版本3.5.2，引入了promise，当传递参数多次且重复，会抛出异常，因此出现上面现象,第一种解决方案：是给push函数，传入相应的成功的回调与失败的回调

  + 第一种解决方案可以暂时解决当前问题，但是以后再用push|replace还是会出现类似现象，因此我们需要从‘根’治病；

    + 在router中添加以下代码

    + ```js
      //解决 :vue-router报错Uncaught (in promise)
      const originalPush = VueRouter.prototype.push
      VueRouter.prototype.push = function push(location, onResolve, onReject) {
        if (onResolve || onReject) return originalPush.call(this, location, onResolve, onReject)
        return originalPush.call(this, location).catch(err => err)
      }
      
      ```

      



+ ##   五：axios二次封装
  + 由于原生的axios对于我们来说我们需要进行以下配置
    + 需要配置基础的路径
    + 需要配置请求超时的时间
    + 需要配置响应拦截器
      + 主要配置返回什么数据给我
    + 需要配置请求拦截器
      + 配置请求头是什么
  + 请求进度条
    +  nprogress.start()  ：进度条的第三方包
    + 开始： nprogress.start()
    + 结束： nprogress.done()





### 六：vuex

+ 当项目比较大，组件通信数据比较复杂，这种情况在使用vuexVuex是插件，通过vuex仓库进行存储项目的数据

+ vuex模块式开发【modules】

+ 由于项目体积比较大，你向服务器发请求的接口过多，服务器返回的数据也会很多，如果还用以前的方式存储数据，导致vuex中的state数据格式比较复杂。

+ 采用vuex模块式管理数据。

+ Vuex核心概念:

  + state、数据仓库

  + mutations、存数据

  + actions、请求数据需要结合 上面封装好的API

  + getters、如果数据量过大可以进行分包

    

    



### 七：防抖与节流

+ 正常：事件触发非常频繁，而且每一次的触发，回调函数都要去执行（如果时间很短，而回调函数内部有计算，那么很可能出现浏览器卡顿）

+ 防抖：前面的所有的触发都被取消，最后一次执行在规定的时间之后才会触发，也就是说如果连续快速的触发,只会执行最后一次

+ 节流：在规定的间隔时间范围内不会重复触发回调，只有大于这个时间间隔才会触发回调，把频繁触发变为少量触发

  





###	八：monk数据

+ 用于模拟数据 比如说后端的接口还没有写好那么就可以模拟以下虚假的数据

+ 第一步：在mock文件夹中创建一个index.js文件注意：在server.js文件当中对于banner.json||floor.json的数据没有暴露，但是可以在server模块中使用。对于webpack当中一些模块：图片、json，不需要对外暴露，因为默认就是对外暴露。


  第二步：通过mock模块模拟出数据

  第三步：回到入口文件，引入serve.js
  mock需要的数据|相关mock代码页书写完毕，关于mock当中serve.js需要执行一次，
  如果不执行，和你没有书写一样的。

  第四步：步:在API文件夹中创建mockRequest【axios实例：baseURL:'/mock'】
  专门获取模拟数据用的axios实例。

  在开发项目的时候：切记，单元测试，某一个功能完毕，一定要测试是否OK









### 九：swiper轮播图插件

+ swiper基本的使用

+ swiper可以在移动端使用？还是PC端使用？

  + 答：swiper移动端可以使用，pc端也可以使用。

+ swiper常用于哪些场景？

  + 答：常用的场景即为轮播图----【carousel:轮播图】
  + swiper最新版本为7版本的，项目当中使用的是5版本

+ https://www.swiper.com.cn/ 官网地址

  





### 十：组件之间的通信
+ 插槽:父子
+ 自定义事件:子父
+ 全局事件总线$bus:万能
+ pubsub:万能
+ Vuex:万能
+ $ref:父子通信
+ 为什么在Floor组件的mounted中初始化SWiper实例轮播图可以使用.
  因为父组件的mounted发请求获取Floor组件，当父组件的mounted执行的时候。
  Floor组件结构可能没有完整，但是服务器的数据回来以后Floor组件结构就一定是完成的了
  因此v-for在遍历来自于服务器的数据，如果服务器的数据有了，Floor结构一定的完整的。
  否则，你都看不见Floor组件
+ 这里有一个$**nextTick**方法
  + 这个方法在一些需要获取页面元素但是，页面还没渲染完成的时候调用 





### 十一：分页器

````html
分页器封装业务分析:
封装分页器组件的时候：需要知道哪些条件？
假如你知道条件1、条件2：知道一共多少页 100/3
1:分页器组件需要知道我一共展示多少条数据 ----total【100条数据】

2:每一个需要展示几条数据------pageSize【每一页3条数据】

3:需要知道当前在第几页-------pageNo[当前在第几页]

4:需要知道连续页码数【起始数字、结束数字：连续页码数市场当中一般5、7、9】奇数，对称好看 continues

已经条件: total=【99】  pageSize =【3】  pageNo=6    continues 5 

4 5 6 7 8

已经条件: total=【99】  pageSize =【3】  pageNo= 1    continues 5 

错误:-1 0 1 2 3
正确: 1 2 3 4 5

已经条件: total=【99】  pageSize =【3】  pageNo= 2    continues 5 

错误: 0 1 2 3 4 
正确：1 2 3 4 5 

已经条件: total=【99】  pageSize =【3】  pageNo= 33    continues 5 

错误: 31 32  33 34 35
正确：29 30  31 32 33 


已经条件: total=【99】  pageSize =【3】  pageNo= 32    continues 5 

错误：30 31 32 33 34 
正确: 29 30  31 32 33 


3)分页器封装
3.1进行单元测试

连续页码5: 8   [6,7,8,9,10] 
连续页码7: 8   [5,6,7,8,9,10,11]

连续页码5:  8   [6,7,8,9,10]
连续页码7:  8   [5,6,7,8,9,10,11]


````





### 十二：放大镜

+ 放大镜功能
+ 获取节点（DOM：必须要定位），通过JS动态修改left|top、定位元素才有left、top属性

```js
  //计算出设置的
    Updata(e) {
      //这里是计算出当前鼠标距离 设置移动事件的坐标  然后需要减去 遮罩盒子的一半
      let x = e.offsetX - this.$refs.mask.offsetWidth / 2;
      let y = e.offsetY - this.$refs.mask.offsetHeight / 2;

      //判断左右边界 设置范围
      if (x <= 0) {
        x = 0;
      } else if (
        x >=
        this.$refs.boxMax.offsetWidth - this.$refs.mask.offsetWidth
      ) {
        x = this.$refs.boxMax.offsetWidth - this.$refs.mask.offsetWidth;
      }
      //判断上下边界 设置范围
      if (y <= 0) {
        y = 0;
      } else if (
        y >=
        this.$refs.boxMax.offsetHeight - this.$refs.mask.offsetHeight
      ) {
        y = this.$refs.boxMax.offsetHeight - this.$refs.mask.offsetHeight;
      }

      //赋值
      this.$refs.mask.style.left = x + "px";
      this.$refs.mask.style.top = y + "px";

      //设置被放大元素的 位置属性
      this.$refs.big.style.left = -2 * x + "px";
      this.$refs.big.style.top = -2 * y + "px";
    },
```









###  十三加入购物车的业务

+ 购物车项目第二个重要地方
+ 购物车：每一个人都有属于自己的购物车，那为什么不同用户登录自己账号，可以看见属于自己产品
  一定是用户点击加入购物车，把你的产品信息提交给服务器进行保存，当你下次在进入购物车的时候，
  需要向服务器发请求，获取你购物车里面的信息展示
+ 项目：点击加入购物车按钮的时候，以前经常进行路由跳转【调到另外一个路由】，
  但是你要注意，点击加入购物车这个按钮的时候，将用户选择产品，提交给服务器进行存储，如果服务器存储成功，
  之后在进行路由跳转







### 十四：用户虚拟UUID

+ 举例子:用户是淘宝平台的用户。

+ 为什么目前我们获取不到自己购物车的数据，你没有给我分配一个用户id

+ 张三:奶粉、鞋子、手机

+ 李四:羽绒服

+ 3.1问题1：用哪个技术可以生成用户id【身份】----uuid

  + uuid 会随机生成一个id

+ 3.2问题2:用户身份如何给后台专递过去？

+ 3.3临时身份只需要执行一次

  + 这里我们判断本地是否有uuid 如果有那么就不在生成如果没有那么就生成这样就是一个单例模式

  + ````js
    //导入uuid包
    
    import { v4 as uuidv4 } from 'uuid';
    
    //导出生成uuid 函数
    export let getUUID = () => {
      //获取uuid 数据
      let uuid = localStorage.getItem('UUID');
      //判断如果没有uuid那么就生成临时身份
      if (!uuid) {
        localStorage.setItem('UUID', uuidv4());
      }
      //返回id数据
      return uuid;
    }
    
    // 单例
    ````

    

+ 3.4临时身份数据持久化

  + 本地存储

+ 3.5会创建一个utils（工具）文件：把常用的代码片段放到这个文件夹里面

+ 3.6配置一些文件[JS]，不能操作仓库

+ 3.7配置文件不限执行，没办法运行项目【配置文件很少碰仓库】







### 十五：token

+ token翻译过来是令牌的意思，只要有这个token那么就代表你登录了，你有权限去操作其他的一些方法

+ token是后端生成过来的会过期

+ 我们一般是将token存储在本地中，然后登录的时候 请求的时候判断是否本地中有token 如果有那么就携带token进入网站并且返回数据

+ 身份凭证：

  + 以后登录：
  + TOKEN身份为大
  + UUID生成的临时省份
  + 用户（注册与登录）token【正式身份】

  





### 十六：导航守卫
+ 守卫条件判断
+ 导航:表示路由正在变。
  守卫:古代的守门的士兵'守卫'，守卫可以通过条件判断路由能不能进行跳转。
+ 三大守卫:
  + 全局守卫：
  + 项目当中任何路由变化都可以检测到，通过条件判断可不可以进行路由跳转。
  + 前置守卫：路由跳转之前可以做一些事情。
  + 后置守卫：路由跳转已经完成在执行。
  + [后置守卫:在路由跳转完毕之后才会执行一次]
    router.afterEach(()=>{
         console.log('守卫:路由跳转完毕才会执行一次')
    })
  + 用户已经登录了，不应该在访问login？【通过什么条件能判断用户登录、未登录】
    路由独享守卫：
    针对某一个路由的守卫
  + 组件内守卫：
    也是负责某一个路由守卫







### 十七：element UI

+ element-ui官方UI组件库（插件）？
+ react框架:
+ UI组件库antd【蚂蚁金服旗下PC端UI组件库】
+ antd-mobile【蚂蚁金服旗下的移动端UI组件库】
+ Vue框架:
  element-UI【饿了吗旗下的UI组件库，官方承认的PC组件库插件】
  vant【Vue官方提供移动端UI组件库】
+ 官网地址:https://element.eleme.cn/#/zh-CN
  官网地址：https://youzan.github.io/vant/#/zh-CN/
+ 第一步：项目中安装element-ui组件库 [2.15.6版本：Vue2]
+ 第二步：在入口文件引入elementUI组件库
+ 第一种：全部引入【不采用：因为项目中只是用到一个组件，没必要全都引入进来】
+ 第二种：按需引入【按照开发需求引入相应的组件，并非全部组件引入】
+ 第三步：按需引入，安装相应的插件
  cnpm install babel-plugin-component -D
  文档中说的.babelrc文件，即为babel.config.js文件
  修改完babel.config.js配置文件以后，项目重启
+ 第四部：按照需求引入相应的组件即可‘
+ Vue.component();
  Vue.prototype.$xxx = xxx;









### 十八：微信支付

+ 支付业务【微信支付】
+  this.$alert('<strong>这是 <i>HTML</i> 片段</strong>', 'HTML 片段', {dangerouslyUseHTMLString: true});
+ 使用messageBox显示弹框
+ 展示二维码----qrcode插件
+ 通过qrCode.toDataUrl方法，将字符串转换为加密的在线二维码链接，通过图片进行展示。
  moment.js
  swiper.js
  nprogress.js
  qrcode.js
+ GET|POST：短轮询，请求发一次，服务器响应一次，完事。
+ 第一种做法:前端开启定时器，一直找服务器要用户支付信息【定时器】
+ 第二种做法:项目务必要上线 + 和后台紧密配合
  当用户支付成功以后，需要后台重定向到项目某一个路由中，将支付情况通过URL参数形式传给前端，
  前端获取到服务器返回的参数，就可以判断了。









### 十九：路由懒加载
+ 面试【高频的面试】:项目的性能优化手段有哪些？

+ v-if|v-show:尽可能采用v-show

+ 按需引入【lodash、elementUI】

+ 防抖与节流

+ 路由懒加载：当用户访问的时候，加载对应组件进行展示。

+  我们如何使用路由

  + 打包小插曲
    + 在vue.config.js文件中使用添加这个命令可以使用 productionSourceMap:false,

  + 路由懒加载实际上就是相当于只有用户进入到这个路由的时候才会加载出路由
    + ()=>import('@/pages/Home')  将这个写在component里








### 二十：图片懒加载

+ 图片懒加载
+ vue-lazyload:图片懒加载
+ 图片：比用用户网络不好，服务器的数据没有回来，
+ 总不可能让用户看白色，至少有一个默认图片在展示。













一些知识点

+ 组件之间通信的一些方式

  + 第一种：props
    + 适用于的场景在父子通行
    + 书写的方式一般有三种 【"todos"】,{type:Arry},{type:Array,default:[]}
    + 书写形式有波尔值，对象，函数形式

  + 第二种：自定义事件
    + 适用于场景：子组件给父组件传递数据
    + $on与$emit
  + 第三种：全局事件总线
    + 适用于场景 "万能"
    + Vue.prototype.$bus = this; 定义在main.js 文件中的Vue实例上面
  + 第四种：pubsub-js 
    + 适用场景：万能
    + 常用于react中使用 发布与订阅
  + 第五种：Vuex
    + 适用于场景：万能
  + 第六种：插槽
    + 适用于父组件通信，一般的结构





+ 事件的深入
  + 自定义组件需要定义系统的事件比如click 或者其他事件等等，那么需要添加一个事件修饰符（native） 事件修饰符
  + 给原生的组件比如button 绑定自定义事件是没有任何意义的：因为触发不了$emit 函数，所以总结下来，如果给组件
  + 添加一个自定义事件那么就需要在组件内部中进行调用 ，否则就触发不了，如果需要使用系统的事件，那么就需要使用native修饰符
+ v-model的深入学习
  +   <input type="text" :value="msg" @input="msg = $event.target.value" /> 这个代码可以实现v-model的实现原理
  + v-model 放在组件中也是可以实现数据的双向绑定
  + v-model的实现原理就是 value 和 @input 事件的结合

+ 





总结就目前就这么多啦~



继续加油，向前看**@FeiMao~**        

2022-9-1-23：30                                                                                                    















VueX=》=》路由=》过渡动画=》自定义事件=》









##  二十五：VueX

+ 什么是vuex   
  + vuex是一个数据状态管理工具，用于管理数据和状态
  
+ 什么时候使用vuex 
  + 在多个模块需要使用数据
  + 或者来自不同组件需要修改数据的情况
  
+ 原理图
  + ![image-20220908155623971](C:\Users\FeiMao\AppData\Roaming\Typora\typora-user-images\image-20220908155623971.png)
    

+ action：常用于处理业务逻辑发送ajax请求的模块  

+ mutations：用于修改state中的数据

+ satte：保存仓库的数据和状态

+ getters:是当数据需要加工的时候可以使用这样的方法进行加工数据

+ 下面是一个基础的例子

+ 

  + 在store中的index.js 文件中的代码

  + 导入包和装插件

  + ```js
    import Vue from 'vue'
    import Vuex from 'vuex'
    
    //这里的vuex装插件需要提前装，否则会报错，如果在main.js中装那么就会报错因为import 会先获取
    Vue.use(Vuex);
    
    ```
    
  + 四个对象(的作用)

  + ```js
    //存储数据
    let state = {
      num: 100,
    };
    
    //修改保存数据
    let mutations = {
      // 第一个参数其实就是state 数据仓库
      // 第二个参数就是传递过来的值
      JIA(state, value) {
        state.num += value
      },
    };
    
    //一些数据的逻辑在这里进行判断，如果可以的话调用commit执行mutation
    let actions = {
      //第一个参数是青春版的store   里面有commit dispatch
      //第二个参数是调用方法传递过来的参数
      getNum(context, value) {
        // return this.state.num;
        context.commit('JIA', value);
      },
    };
    
    //这个相当于处理数据，然后获取的时候比较方便
    let getters = {
      numMax (state){
        return state.num * 10;
      }
    }
    ```
    
    
    
  + 导出对象

  + ```js
    //导出对象
    export default new Vuex.Store({
      state,
      mutations,
      actions,
      getters
    })
    ```

    

    

  + 组件获取store中的数据

  + VueX中提供了两个获取数据的API  分别是mapState 和 mapGetters 中两个方法、

  + mapState用于帮助我们映射state中的数据

  + mapGetters用于帮助我们映射getters中的数据

  + 下面是两个方法获取数据的实例

    + count组件中获取数据的方法实例

    + 

    + 首先在vuex中结构出 **mapState** 和 **mapGetters** 两个方法

    + ```javascript
      import { mapState, mapGetters } from "vuex";
      ```

      

    + 一般我们会从store中获取的数据定义在computed中

    + **mapState中获取数据**

    + ```javascript
        //获取数据state中的数据 以下有四种方式进行获取
        //在以往我们获取数据需要this.$store.satte.xxx 这样获取数据，这样获取数据逻辑不是很清晰，所以vuex提供了mapState这个方法
            num() {
              return this.$store.state.num;
            },
        
          // _________对象_______________
            // 01:使用mapState中的对象写法({第一个个参数是你需要将获取的数据给的名称，第二个参数是你需要从state中获取的数据名称})
            // 01_1由于返回的是一个包含方法的一个对象所以需要结构出来
            ...mapState({ he: "num", xuexiao: "shool", xueke: "subject" }), 
        
          // _________数组________________
            // 02:mapState中的数组的写法 (比如我们使用的数据名称和获取的数据名称是一致的那么我们可以使用数组的方式进行获取，这样就不需要重新赋值给       一个新的名称)
            //02_2:当然返回的也是一个包含你获取数据的方法在一个对象中，那么我们需要结构出来
            ...mapState(["num", "shool", "subject"]),
        
              
            //_________函数and对象______________
            // 03：mapState中也是有函数中写法，这样我们可以通过这种方式进一步处理数据
            // 03_1:由于返回的数据还是一个对象中的数据，所以还需要结构出来
            ...mapState({
              num: (state) => {
                return state.num + "元";
              },
              shool: (state) => {
                return state.shool + "尚硅谷";
              },
            }),
      ```
      
        
      
    + mapGetter 中获取数据(也是写在computed 计算属性中)
    
    + 这个API可以支持二种获取数据的方法 
    
    + ```javascript
          ...mapGetters({numMax:'numMax'}),对象写法
          ...mapGetters(['numMax'])：数组写法
          console.log(this.$store.satte.getters)
      ```
    
        
    
        
    
    + mapMutations：这个方法常用于，不需要经过action 处理业务逻辑的模块，直接调用commit模块
    
    + 案例
    
    + ```javascript
        count 组件
        //在组件中需要将值传递过去，不然传递的参数是一个event
            <button @click="add(n)">+</button>
            <button @click="rem(n)">-</button>
        
        
         // 基础的调用commit
            // 参数设置：第一个参数是 store数据仓库中的action中的方法，第二个参数是传递的数据
            // 原因：由于下面两个方法修改的数据不需要经过 action 处理业务逻辑 所以可以直接经过 commit 修改数据
            // 因此 vuex 提供了我们一个不需要重复写这种计算属性的方法mapMutations
            add() {
              this.$store.commit("JIA", this.n);
            },
            rem() {
              this.$store.commit("JIAN", this.n);
            },
        
            // 01:mapMutations (对象写法) 用于执行 this.$store.commit("xxx", xxx);
            // 参数设置：第一参数是调用的名称|| 第二参数是调用的commit中的方法
            // 传递参数：在调用的时候进行传递(不传递参数那么commit中获取的是一个event)
            ...mapMutations({ add: "JIA", rem: "JIAN" }),
        
            //01：mapMutations(数组的写法)
            // 参数设置：里面的名称需要写commit中的函数名
            // 参数传递：在调用的时候传递参数
            ...mapMutations(["JIA", "JIAN"]),
        
        ```
    
        
    
        
    
    + mapActions：这个方法常用于，批量的调用action 处理业务逻辑的模块
    
    + 案例
    
    + ```javascript
            //下面两个计算属性是需要经过action中处理业务逻辑的，所以vuex提供了mapActions 方法 用于 执行 this.$store.dispatch("xxx", xxx);
        
            //基础的写法调用action
            addEve() {
              this.$store.dispatch("getOdd", this.n);
            },
            addSim() {
              this.$store.dispatch("getTime", this.n);
            },
        
            // 02：mapActions(对象的写法)
            // 02：参数传递：在调用的时候传递
            ...mapActions({ addEve: "JIANODD", addSim: "JIANTime" }),
        
            // 02:mapActions(数组的写法)
            // 02：参数传递：在调用的时候传递
            ...mapActions(["JIANODD", "JIANTime"]),
        ```
    
    + 
    
    + 
    
    + 命名空间：比如有A,B,C 三个模块，这三个模块中的数据如果全部集中在主要的仓库中，那么如果项目一大那么就很混乱，并且书写的业务逻辑会与其他的模块产生冲突，因此vuex可以让我们以模块化的形式添加管理数据仓库
    
    + 主要的步骤其实就是开启命名空间： namespaced: true,  这个参数默认为false 需要修改成true
    
    + 开启命名空间后获取数据与调用方法都是需要在调用的时候填写注册的数据仓库
    
        
    
    
    
  + ```javascript
     总结
      
     vuex 中提供了
      
     调用action中的方法: this.$store.dispathc("action模块中的函数名称","传递的参数");
     调用Mutation中方法：this.$store.commit("mutation模块中的函数名称"，"传递的参数");
     mapState :获取vue仓库中的数据
     maGetters：获取getters中的数据
     mapMutation：调用mutation中的方法
     mapAction：调用action中的方法
     
     //对比（以map开头的AIP都是需要...结构出来）
     01：获取数据
     this.$store.state.num;
     ...mapState('A',{num:'num'}) 
     
     02：获取getters中的数据
     this.$store.state.getters.num
     ...mapGetters('A',{max:max})
     
     03：获取commit中的方法
     this.$store.commt('ADD',this.sex)
     ...mapMutations('A',{add:'ADD'}) 调用的时候传递参数
     
     04：调用action中的方法
     this.$store.dispatch('add',this.name)
     ...mapActions('A',{add:'add'})  调用的时候传递参数
     
     
     以外知识点： Nano ID是一个小巧、安全、URL友好、唯一的 JavaScript 字符串ID生成器。
  
   
  
  











## 	二十六：router 路由



+ 路由其实就是一组key 和router的对应关系 

+ 多组路由需要一个路由器进行管理

+ SPA 单页面应用程序
  + 整个应用只有一个完整的页面
  + 点击页面上的导航链接不会刷新页面，只会做页面的局部更新
  
+ 基础的使用

+ 导入组件进行注册路由

  + ```javascript
    import vue from 'vue'
    import VueRouter from 'vue-router'
    vue.use(VueRouter);//装插件
    
    import about from '@/pages/about'
    import home from '@/pages/home'
    
    
    //设置路由
    export default new VueRouter({
      routes: [
        { path: '/About', component: about },
        { path: '/Home', component: home },
      ]
    })
    ```

  + 使用router-link设置点击到哪里的路由

    + ```html
       <li>
           <router-link to="/About" active-class="active">Aobut</router-link>
       </li>
      ```

  + 使用router-view设置显示的组件

    + ```HTML
       <div class="box-right">
          <router-view></router-view>
       </div>
      ```

  + 几个注意点

    1. 路由组件通常放在src 下面的pages 目录，一般组件通常存放在compoents文件夹中
    2. 通过切换，“隐藏的路由组件”，默认是被销毁掉的，需要的时候再去挂载
    3. 每一个组件都有自己的$route,里面存储了路由的信息
    4. 整个APP中只有一个router，我们一般通过整个来跳转路由

+ 设置多级路由

  + 使用childer

  + ```javascript
    
    export default new VueRouter({
        { path: '/about', component: about },
        {
          path: '/home',
          component: home,
          //设置二级children 设置子路由
          children: [
            {
              path: 'news',
              component: news
            },
            {
              path: 'message',
              component: message,
              //设置三级子路由
              children: [
                {
                  path: 'detale',
                  component: detale,
                }
              ]
            }
          ]
        },
      ]
    })
    ```

+ 携带query参数跳转路由

  + 使用路径拼接的形式（1种方法）

  + ```html
    <router-link :to="`/home/message/detale?id=${m.id}&title=${m.title}`">//一般我们会使用模板字符串
        {{ m.title }}
    </router-link>
    ```

  + 使用对象形式携带query参数（2种方法）

  + ```html
     <router-link
       :to= "{
       path: '/home/message/detale',
       query: {
       id: m.id,
       title: m.title,
         },
       }" >
         {{ m.title }}
    </router-link>
    ```

+ 携带params参数跳转路由

  + 使用路径形式拼接（1种方法）

  + ```html
     <!-- 使用路径拼接的方式 -->
    <router-link :to="`/home/message/detale/${m.id}/${m.title}`">
     {{ m.title }}
    </router-link>
    ```

  + 使用对象的形式(2种方式)

  + (注意点)：这里如果使用to的对象的写法那么不能使用path属性只能使用name属性

  + ```html
      <router-link
        :to="{
        name: 'duoji',
        params: {
        id: m.id,
        title: m.title,
         },
        }" >
        {{ m.title }}
      </router-link>
    ```

  + 



  + **命名路由**

    + 简而言之就是给router设置一个名称然后可以通过name中的名称进行跳转

    + 定义

      + ```js
         { path: '/about', component: about, name: 'duoji' },
        ```

    + 使用

      + ```html
         <router-link
           :to= "{
           name: 'duoji',
           query: {
           id: m.id,
           title: m.title,
             },
           }" >
          {{ m.title }}
        </router-link>
        ```

         

​	

+ **路由中的props中的配置**

+ ```javascript
     {
      name: 'duoji',
      path: 'detale/:id?/:title?',
      component: detale,
  
      // 01 props的第一种写法 对象的写法  一般不常用(固定值)  将对象中的参数通过props传递到 组件中
      props: {
          a: '111',
          b: '2222',
      },
  
      // 02 props的第二种写法 波尔值写法 比较常用(只用于接收params参数) 将路由所有收到的params参数都通过props传递给 组件中,
      //这个写法需要在path中配置一下params的值 写了[?] 表示可传可不传
      props: true,
     
     
      //03 props的第三种写法 函数写法 比较常用(用于接收query和params参数) 该对象返回的参数都会通过props传递给 组件中
       props: function ($router) {
               return { id: $router.params.id, title: $router.params.title }
         },
      }
  ```



+ **<router-link>中的replace属性**

  1. 作用：控制路由跳转操作浏览器历史记录的模式

  2. 浏览器的历史纪录有两种写入方式，分别为 【push】追加模式 和【replace】替换模式，，路由默认的模式是push模式

  3. 开启`replace`模式  

     1. ```html
         <router-link :replace="true" to="/About" active-class="active">Aobut</router-link>
        ```

        

+ **编程式导航**

+ 编程式导航可以处理一些需要写逻辑并且传递参数比较复杂的情况下进行使用

  +  push 会产生历史记录

  + ```js
      pushShow(m) {
          console.log(this.$router);
          this.$router.push({
            name: "duoji",
            params: {
              id: m.id,
              title: m.title,
            },
          });
        },
    ```

    

  +   replace 不会产生历史记录

  + ```javascript
    //repalce 路由跳转
        replaceShow(m) {
          this.$router.replace({
            name: "duoji",
            params: {
              id: m.id,
              title: m.title,
            },
          });
        },
    ```

    

    

  + 前进，后退，自定义

  + ```javascript
    //后退
    back() {
       this.$router.back();
    },
        
    //前进
    forward() {
      this.$router.forward();
    },
        
    //这个是通过参数进行控制的 如果是-1那么就后退一步，如果是2那就前进2步
    go() {
      this.$router.forward(-1);
    },
    ```

  + 

+ 

+ **缓存组件**

  + keep-alive 用于缓存组件 

  + include ：配置项用于设置需要缓存哪个组件（不写默认展示所有组件）

  + ```javascript
    //include是用于 
    <keep-alive include="News">
        <router-view></router-view>
    </keep-alive>
    
    
    
    //缓存多个组件（使用数组的形式写）
      <keep-alive :include="['News','Message']">
           <router-view></router-view>
      </keep-alive>
    ```

  + 

+ 组件的两个新的生命周期函数

  + 具体的实例比如我们在展示组件的时候启用组件的定时器，但是又想步展示组件的时候取消定时器

  + ```javascript
     //组件激活的时候
      activated() {
        console.log("激活了");
        this.time = setInterval(() => {
          console.log("定时器我一直在运行");
        });
      },
          
      //组件失活的时候
      deactivated() {
        console.log("失活了并清除定时器");
        clearInterval(this.time);
      },
    ```

  + 

路由守卫

+ meta：属性

+ 通常用于存放一些数据，进行判断

  + ```javascript
     {
        path: 'message',
        component: message,
        meta: {
          isRWS: true,
          title: '消息'
     },
    ```

  + 

+ 01：路由前置守卫  【在页面跳转之前进行守卫】

+ ```javascript
  
  router.beforeEach((to, from, next) => {
    // to: 前往跳转的路由
    // from：被跳转的路由
    // next：放行
  
  
    //路由判断判断是否是该路径，如果是那么就进一步判断
    //但是我们如果这样写的话，会产生很多路劲判断，所以路由给我们一个meat配置项
    if (to.meta.isRWS) {
      //判断权限名称是否power
      if (localStorage.getItem('power') == "肥猫") {
        next()
      } else {
        alert("你无权限")
      }
    } else {
  
      next()
    }
  })
  ```



+ 02：后置路由守卫 【在页面跳转之后进行】

+ ```javascript
  
  //02：后置路由守卫 【在页面跳转之后进行守卫】
  router.afterEach((to, from) => {
    //这里设置了路由跳转之后进行切换标题
    document.querySelector('title').innerHTML = to.meta.title || "路由测试"
  })
  ```



+ 03：前置路由独享守卫 【只针对某个路由进行守卫】

+ ```javascript
    //独享路由守卫(独享路由守卫只有独享前置路由守卫)
    beforeEnter: (to, from, next) => {
      if (to.meta.isRWS) {
        //判断权限名称是否power
        if (localStorage.getItem('power') == "肥猫") {
          next()
        } else {
          alert("你无权限001")
        }
      } else {
  
        next()
      }
    },
  ```



+ 04：组件内守卫 【规则写在组件内部】

+ ```javascript
    //通过路由规则进入组件 调用
    beforeRouteEnter(to, from, next) {
      console.log("我进来了");
      next();
    },
  
    //通过路由规则离开该组件 调用
    beforeRouteLeave(to, from, next) {
      console.log("我离开了");
      next();
    },
  ```

+ 







+ 路由器工作的两种模式
  1. 对于一个url来说，什么是hash值？ ___就是# 符号及其后面的内容
  2. hansh值不会包含在HTTP请求中，即：hash值不会带给服务器
  3. hash模式：
     1. 地址中永远带着# 号  ，看起来不美观
     2. 诺以后地址通过第三方收集app分享，诺app校验很严格，则地址会被标记为不合法
     3. 兼容性好
  4. history模式：
     1. 地址干净，美观
     2. 兼容性和hash模式略差
     3. 应用部署上线的时候需要后端人员的支持







## 二十七：Vue中的过渡动画

+ 过渡动画是指一个dom元素从出现到消失的过渡动画(通常是在又v-if 和 v-show 中才会有效果的)

  

+ 实现的方法【一】

  + HTML 文件中需1要控制一个Boolean值进行控制元素的显示隐藏，并且添加一个transition 动画标签包裹需要有过渡的元素

  + transition中有一个name属性这个属性防止多个DOM元素需要动画，所以可以设置name属性进行定义

  + ```html
      <button @click="isShow = !isShow">显示/隐藏</button>
      <transition name="boxA">
        <div class="box" v-show="isShow" :appear="true">
          <h1>BOX</h1>
        </div>
      </transition>
    ```

  + Css文件中

  + ```css
    定义以下boxA中的动画
    @keyframes boxA {
      //起始
      from {
        width: 0px;
        height: 0px;
        h1 {
          color: red;
        }
      }
      //结束
      to {
        width: 200px;
        height: 200px;
        h1 {
          color: red;
        }
      }
    }
    
    
    使用上面定义的boxA动画[这里面我们一般是写一些过渡的时间]
    //开始
    .boxA-enter-active {
      animation: boxA 1s;
    }
    //结束
    .boxA-leave-active {
      animation: boxA 1s reverse;
    }
    
    ```

  

+ 实现的方法【二】

  + HTML中

  + ```javascript
     <transition name="boxB">
       <div class="boxs" v-show="isShow" :appear="true">
         <h1>BOX2</h1>
       </div>
     </transition>
    ```

  + CSS中

  + ```css
    这里的过渡动画设置在元素中
    .boxs{
      transition:0.5s linear;
    }
    //进入的起点
    .boxB-enter {
      width: 0px;
      height: 0px;
    }
    //进入的过程
    .boxB-enter-active {
      width: 0px;
      height: 0px;
    }
    //进入的终点
    .boxB-enter-to {
      width: 100px;
      height: 200px;
    }
    
    //除了可以将过渡添加到元素上面，也可以写在这里
    .boxB-enter-active,.OPO-leave-active {
      transition: 0.5s linear;
    }
    
    //离开的起点
    .boxB-leave {
      width: 100px;
      height: 100px;
    }
    
    //离开的过程
    .boxB-enter-active {
      width: 0px;
      height: 0px;
    }
    
    //离开的终点
    .boxB-leave-to {
      width: 0px;
      height: 0px;
    }
    
    
    以上的一些动画效果有一部分是重复的我们可以合并同类项一下
    ```

  + 第三方的动画库：Animate.css







## 二十八：proxy 配置代理服务器

+ 由于不符合主机策略所以会产生跨域，需要同源：协议【https】,主机【192.168.100.1】，端口号：【8080】只要符合以上三个条件就会产生跨域

+ 在vue-cli中我们可以解决，在服务器中配置也可以解决

  

+ 方法一：

  + 添加一个这个配置项

  + ````javascript
    ##vue.config.js
    
    devServer: {
        proxy: 'http://localhost:5000'//这个代理服务器的地址填写需要请求的服务器地址
      }
    
    ````

  + 使用的时候

  + ```javascript
     async getUsr() {
         //获取的时候需要将端口填写自己的端口号 其实就相当于配置了一个代理服务器  一个中介【中介的端口号也是8080】
         let resulte = await axios.get("http://localhost:8080/user");
     },
    ```

    注意方法一的问题会导致，比如本地有和路由访问的资源路径一致那么就会只获取本地 ，从而不会去请求服务器的资源（优先匹配前端资源）

  



+ 方法二

  + ```javascript
     // 02：灵活的配置代理
      devServer:{
        proxy:{
          '/api':{
            target:'http://localhost:5000',//设置请求地址
            pathRewrite:{'^/api':''},//代理服务器发送请求给服务的时候会将请求中的开头  api 清除
            ws:true,//用于支持websocket
            changeOrigin:false,//用于欺骗服务器，
            //如果为 true 如果请求的端口号为8080， 服务器的端口号为5000，如果发送请求了，那么服务器以为来请求的端口号也是5000 从而达到欺骗服务器
            //如果为 fasle 如果请求的端口号为8080， 服务器的端口号为5000，如果发送请求了，那么就会如实交代请求的端口号是8080 
            // changeOrigin 默认值为 true
          }
        }
      }
    ```

  + 

