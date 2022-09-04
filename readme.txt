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
然后回车，选择vue3，然后不需要router历史，然后配置信息存放到package.json里面，然后不保存为模板
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
下载组件命令：npm i elment-ui -S
其中 i就是install -S就是--save将模块安装到我们的项目目录下面，正式环境和开发环境
这里因为我们用的是vue3所以不适配，因此我们需要下载element-plus
引入和使用
在main.js里面引用
import ElementPlus from 'element-plus'
import 'element-plus/dist/index.css'
Vue.use(ElementPlus)
然后我们开始创建登陆界面
