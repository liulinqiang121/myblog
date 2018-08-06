说一下vue和react的异同，

1 模板 
  vue采用的template，react采用的是jsx，前者像是html加入js，css,后者更像是在js里面写入html,至于是否喜欢，看个人爱好
  
2 指令
  vue是自带v-if,v-else,v-for,v-bind的这样的基本指令，可以直接用指令进入切换和循环渲染子元素，react就比较麻烦，将子元素集渲染出来作为组件再放入       父集，不过这也是更纯粹的一切都是组件的思想
  
3 组件通信
  vue和react都通过props由父组件向子组件传递数据，但是子组件向父组件传递数据时，vue采用的是子组件$emit，父组件去接收事件，react是通过props将方       法传递给子组件，子组件调用吃方法去实现
  
4 生命周期 
  vue和react都有生命周期，vue的created,mounted，beforeupdate,destoryed,reactcomponentWillMount,componentDidMount,componentWillunmount,
  等，基本上字面上就能明白
 
5 vue-router和react-router
  用法很不同，vue-router,用path,component,children进行路由嵌套，react-router要将路由要用组件包裹，
  
6 redux
  首先创建一个reducer,用过dispatch修改store,subscibe监听dispatch
