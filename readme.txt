项目介绍
一个中小型企业的在线办公系统，用来管理日常的办公事务，可以管控的内容有
日常流程审批，新闻，通知，公告，文件信息，财务，人事，费用，资产，行政，项目，移动办公等
优点是通过软件的方式，方便管理，更加简单，扁平，高效，规范，
开发模式
前后端分离开发，Vue构建前端
主要的技术点有
Vue
Vue-cli
VueRouter
ElementUI
Axios
ES6
Webpack
WebSocket
font-awesome
js-file-download
vue-chat
主要有
登陆
职位管理
职称管理
部门管理
员工管理
工资管理
在线聊天
个人中心

搭建项目
首先下载node.js
然后安装淘宝镜像加速器cnpm
npm install cnpm -g
然后可以考虑装一下nrm，这个是npm源的管理器
可以用nrm ls 查看自己的源
接下来安装脚手架
npm install -g @vue/cli
安装完成后，我们采用windows的powershell来新建项目，首先新建一个文件夹用来存放我们的项目
然后进入该目录，使用命令进行创建项目
vue create yeb
这里我遇到了问题：因为在此系统上禁止运行脚本，解决办法：
set-ExecutionPolicy RemoteSigned 然后输入y
然后再运行vue create yeb
之后给我们一个选择，这里我们选择Manually select features
这个表示让我们自己选择我们需要用到的组件和依赖
这里我们选择了Babel，Router，然后Vuex后期会提到就没有选
然后回车，选择vue2，然后不需要router历史，然后配置信息存放到package.json里面，然后不保存为模板
然后他就开始自己创建项目
项目创建完成后，提示你进入yeb目录，然后启动项目的命令是：npm run serve
接下来我们用Hbuilder来完成前端的实现
首先简单介绍一下文件
node_modules是我们用到的依赖文件，通过npm install 就可以安装的
public公用目录，里面有一个index文件，和一个vue的图标
babel.config.js主要把es6转换成es5
package.json整个项目的配置文件
src下面的文件
assets专门放一些资源
components组件目录
router路由目录
views页面目录
main.js整个程序的入口，里面的Vue.config.productionTip=false表示关闭浏览器对于环境的提示，开发环境等
其中关于vue语法大家可以看我vue仓库里面的或者到官网了解
接下来正式开发项目
使用ElementUI
vue2
下载组件命令：npm i element-ui -S
其中 i就是install -S就是--save将模块安装到我们的项目目录下面，正式环境和开发环境
import Vue from 'vue';
import ElementUI from 'element-ui';
import 'element-ui/lib/theme-chalk/index.css';
import App from './App.vue';

Vue.use(ElementUI);

new Vue({
  el: '#app',
  render: h => h(App)
});
vue3我们需要下载element-plus
引入和使用
在main.js里面引用
import ElementPlus from 'element-plus'
import 'element-plus/dist/index.css'
Vue.use(ElementPlus)
然后我们开始创建登陆界面
删掉App.vue的代码，只保留id为app的div
删掉views里面其他的文件，components里面的文件

然后在views里面新建Login.vue文件
在index.js里面配置路由
接下来就是写简单的登陆表单，
然后写登陆检验方法，校验规则
https://element.eleme.cn/#/zh-CN/component/form
差不多后，我们开始安装axios用来进行前后端通讯
npm i axios -S
然后由于需要不断请求数据，然后判断，很麻烦，所以我们需要进行封装
为了省事
所以新建utils目录，api.js文件
里面写了拦截器，和一个json的post请求，然后检查登陆需要调用的接口，
一个登陆的接口，一个验证码的接口
然后这里我们遇到一个问题，跨域问题，8080要去调用8081接口
我们通过node.js来转发我们的请求
新建vue.config.js
主要解决完跨域问题之后，我们开始准备前端登陆之后的跳转，我们这里跳转到home，需要新建一个home.vue文件，然后在方法里写明跳转
这里有个知识点，router的push和replace的区别，replace替换，不可以退回，push可以退回，登陆成功我们选择replace
再跳转之前我们需要验证tooken，
然后我们需要一个请求拦截器，还是写在api里面，请求拦截器获取到cookie
然后我们把postrequest等操作写在api里面进行，导入到mainjs里面，这样在调用这些方法的时候就可以全局使用
之后我们进行home的布局
用到了container的布局容器
然后当我们使用了菜单布局的时候，在设置选择组件，希望点击之后展示到指定位置，而不是直接跳转页面，
原因：因为我们app里面有一个routerview，所以默认跳转到app里面
解决方法：我们在home的路由下面，加上children数组，放入我们的页面路由
但是这种方法太麻烦，所以我们将菜单和路由数据统一，将路由数据渲染到菜单上面，然后我们在menu标签上去掉select方法，加上router属性，然后在需要循环的列表外面一层submenu里面写for循环，循环的对象是路由里面的孩子
接下来我们实现菜单功能
后端数据接口传递到前端
菜单数据我们缓存到内存里，用到了vuex，所以下载
npm i vuex -S
但是我们用的是vue2，所以需要npm i vuex@3 -S
写好store之后，我们需要封装一个菜单类，用来把后端传来的字符串转化为对象，
