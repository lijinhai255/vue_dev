vue2

vue3

1. 特征
    实现

dist
    flow  ts

common   es

runtime   runtime + compiler


```js
var a=1;
```
a 1
程序运行起来之后的状态
vue ==>
1. 生命周期   event
2. 双向绑定数据  data
3. 事件  VNode
状态   runtime 运行时




compiler   编译时

teamplate   .vue  ==> js  离线编译  webpack + vue-loader  ==》js

在线运行时去分析 模板 ？？？ html vue   浏览器端运行时 在线编译  js==>vue
运行时  在线编译的库

vue ssr  vue  runtime --> 字符串

```js
new  Vue({
    template:'<div></div>'
})
```

scripts

src



script,style,template

script  ==>  bable

style   ==> postcss

template  ==> vue compiler




runtime   core
    1.  keep alive
    2.  vue 全局api  use mixin
    3.  event    lifecycle
    4.  observer  双向数据    dep

  vue2
  object.definproproperty   双向
  一开始就监听了对象上面的key   没有的key（新增）  ！！！不会
  1. 一层
  2. 多次触发 （数组）
  proxy
```js
  Object.defineProperty(obj,'a',{
    get:function(){
        console.log('get val');
        //获取数据 渲染到页面  render
        //媒介   watcher
        return a;
        //get {{times}} 添加Dep
    },
    set:function(newVal){
        console.log('set val:'+newVal);
        a=newVal;
        // 修改 -->render-->get
        //update


        // dep.notify 通知
    }
});
```
```html

    <div id="app">
      <button id="show-modal" @click="showModal = true">Show Modal</button>
      <!-- use the modal component, pass in the prop -->
      <modal v-if="showModal" @close="showModal = false">
        <!--
          you can use custom content here to overwrite
          default content
        -->

        <h3 slot="header">{{time}} header</h3>1
        <h3 slot="header">{{time}} header</h3>1
        <h3 slot="header">{{time}} header</h3>1
        <h3 slot="header">{{time}} header</h3>1
      </modal>1
    </div>
```
动态 --》指令使用


[<h3 slot="header">{{time}} header</h3>,<h3 slot="header">{{time}} header</h3>,<h3 slot="header<h3 slot="header">{{time}} header</h3>">{{time}} header</h3>,]

time 1    2
```js
function render(){ //data  ==>VNode    compoent Vnode  dom diff
  with(data){
    return {
      tag:'div'
      props:{
        id:time,
      }
    }
  }
}
```

patch  Vnode --》 真实dom

思考之前  模型先行

学习（看书）之前  问题先行




vue1 directive -->  watcher   dep []  dom diff

vue2  component render -->watcher  dep []   dom diff
vue3  component render  -->effect

//vue2 --》 component render





vue2 运行时 ？？？ watcher cb ？？？ render
vue2 编译时
keep-alive   LRU

状态
 VNode

VNode
LRU  Leetcode
vue.use()

vue --> js render



vue 编译时优化
react 运行时优化
模板 -->js
1. 分析模板     通过正则匹配 ，输出AST 描述dom结构 知道对应的节点信息
2. 构建描述模板的树  遍历节点处理成为静态节点
3. js




```js
var a=1;
var a =
// var let const b
```

```js
function render(){
    with (this) {
        return _c('div',
        {
            attrs: { "id": "app" }
        }, [_c('div', [
            (message) ? _c('h2', [_v(_s(message))]) : _e(),
             _v(" "),
            _c('button', {
                on: { "click": showName }
             }, [
                 _v("showName")
                ]),
            _v(" "),
            _m(0)]

        )]) }
}
```


1. 编译时 静态节点优化 dom diff
2. 批处理 
3. 双向数据绑定  靶向更新 ==>某一个组件


1. watcher 需要维护的响应式数据和watcher  
2. with 



react 
fiber 保存当前执行环境数据模块   并发current mode



js yeild   协程
function *(){
  yeild console.log(1)
  yeild console.log(2)
}


proxy  拦截整个对象的操作   不需要去遍历每一个key ，不需要对新增加的key 做新的拦截 
object.definproproperty 对象的key重写



```js
var data = { 
  foo: 'foo', 
//   bar: { 
//    key: 1 
//   }, 
//   ary: ['a', 'b']
};

var p = reactive(data);

function reactive(data){

  return  new Proxy(data, {
      get(target, key, receiver) {
        console.log('get value:', key)
        var res=Reflect.get(target, key, receiver);
//         if(typeof res=='object'){
//           return reactive(res)
//         }
        return res
      },
      set(target, key, value, receiver) {
        console.log('set value:', key, value)
        return Reflect.set(target, key, value, receiver)
      }
    })
}


// p.bar.key = 2
// p.ary[0]=4

```



1. vue2 编译与vue3编译优化 
2. vue3 运行时优化 
3. vue3 运行时流程 
4. vue3 diff优化 
5. vue3 生命周期及整个流程 ，setup