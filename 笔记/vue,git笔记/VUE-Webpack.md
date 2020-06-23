## 模块化
### ES6
- 引入js文件加type="module"属性
- export/import
  - export{名字}
  - 导出函数，类
  - 直接导出，定义好再导出
  - export default 不明名，导入者自己定义名字。在同一模块只有一个
  - import * as 名字 from './aa.js'
### webpack
- 

### URL
- history.hash
- hash 改变url界面不刷新
- pushState、replaceState
- go、back、forward

## VUE
### 基础
- npm run serve
- 
#### Vue程序运行过程
- template-ast-render-virtual dom-真实dom
### 组件
- 生命周期函数
	- created 组件创建生命周期函数，创建组件回调次函数
	- destroyed
	- mounted 挂载模板
	- updated 页面刷新
## router
- 创建路由组件
- 配置router
  - routes里面为对象，组件和路径映射关系
    - 属性routes mode...
- 通过 router-link router-view
  - link
    - to
    - tag="button" 改变渲染标签样式
    - replace 不能返回按钮
    - active-class
- keep-alive 保持组件活着，不被频繁的创建销毁-----activated
	- 属性
	- include-字符串或者正则表达式，只有匹配的组件才会缓存
#### 路由功能
- 懒加载 component:()=>import('../views/User')
- 路由嵌套
	- 加载进子路由中
#### 导航守卫
- 监听组件跳转过程
	- router.beforeEach
- 组件属性
	- 配置组件中的属性
	- meta元数据-描述数据的数据
### 案例tabbar
- vue.app
	- 
	
### promise
```js 
new Promise((resolve,reject)=>{
	resolve(data)
	reject(err)
}).then((data)=>{
	console.log(data)
}).catch((err)=>{
	console.(err)
})
```
- promise.all([new promise(),new promise()])

## VUEX
### 属性
#### mutations
- state mutations actions modules
- 通过actions(可不用，有异步操作必须用)-mutations-修改-state
	- 可以被devtools查看
	- mutations里面定义方法修改用
	- 更新store唯一方式就是提交mutation
- mutation包括两部分
	- 事件类型type
	- 回调函数handler，第一个参数state
	- $store.commit('mutations中函数'，传过去的参数) 参数称为payload
	- $store.commit({type:'mutations中函数',count,age:18})提交一个对象过去
- push,pop,shift,unshift,sort,splice,reverse 响应式
- this.array[0]='李辉' 不是响应式
- Vue.set(info,数组索引、对象键，修改后的值)
- Vue.delete
#### actions
- 异步请求经过actions
- component-dispatch> actions -commit> state
## 对象解构
- 



